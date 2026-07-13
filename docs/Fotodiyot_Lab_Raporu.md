# Fotodiyot Lab Raporu

Bu dosya, [`Fotodiyot_Lab_Raporu.pdf`](../pdf/Fotodiyot_Lab_Raporu.pdf) iceriginden duzenlenmis Markdown notu olarak hazirlanmistir.

## Genel Bakis

Rapor, Thorlabs `FDS10X10` PIN fotodiyot icin onerilen olcum devresinin kurulmasini, karanlik ortam ve isik altindaki davranisinin izlenmesini, olcum sirasinda karsilasilan sorunlarin giderilmesini ve Arduino ile uretilen darbeli test sinyalinin devreye uygulanmasini anlatir.

Temel hedefler:

- datasheet'teki onerilen olcum devresini kurmak
- karanlik ortam ve isik altindaki tepkiyi gozlemlemek
- osiloskop ve breadboard kaynakli olcum sorunlarini ayiklamak
- Arduino ile tekrarlanabilir bir pulse kaynagi olusturmak

## Kullanilan Yapi ve Bilesenler

Devre, uretici tarafindan onerilen fotodiyot olcum topolojisini izler:

- fotodiyot: `Thorlabs FDS10X10`
- `R1 = 1 kOhm`
- `C1 = 0.1 uF`
- `RL = 1 MOhm`
- bias kaynagi: `5 V DC`
- osiloskop: `Tektronix TDS 2002B`
- multimetre: `HIYE HY892`
- test kaynagi: Arduino dijital cikisi

Devrede `R1 + C1` bias hattinda gurultu filtresi olarak kullanilir. Fotodiyot ters polarmada calistirilir ve cikis gerilimi `RL` uzerinden okunur.

## Deney Akisi

### 1. Devrenin Kurulmasi

Datasheet'teki onerilen devre breadboard uzerine aktarildi. Bias hattindan gelen gerilim `R1` uzerinden fotodiyotun katod tarafina verildi. `C1`, fotodiyot-bias dugumu ile `GND` arasina paralel baglandi. Fotodiyotun anot tarafi ise `RL` uzerinden `GND`'ye cekildi.

### 2. Karanlik Ortam ve Ilk Gozlem

Fotodiyot ortam isigindan olabildigince izole edildi. Ilk denemelerde osiloskopta beklenen kare dalga yerine yavas kayan bir seviye goruldu. Bu, olcum zincirinde hem baglanti hem de zaman tabani ayari tarafinda sorun olabilecegini gosterdi.

### 3. Arduino ile Pulse Uretimi

Optik uyartim yerine once tekrarlanabilir bir elektriksel test sinyali uretilerek sistem kontrol edildi. Arduino'nun dijital `pin 8` cikisi periyodik olarak `HIGH` ve `LOW` seviyeleri arasinda anahtarlandi.

Kullanilan temel test mantigi:

```cpp
const int pulsePin = 8;

void setup() {
  pinMode(pulsePin, OUTPUT);
}

void loop() {
  digitalWrite(pulsePin, HIGH);
  delay(10);
  digitalWrite(pulsePin, LOW);
  delay(10);
}
```

Bu surum teorik olarak yaklasik `50 Hz` ve `%50` gorev dongusune karsilik gelir:

```text
T = 10 ms + 10 ms = 20 ms
f = 1 / T = 50 Hz
```

### 4. Darbe Sinyalinin Devreye Uygulanmasi

Arduino cikisi ile devre arasina `2 kOhm` seri direnc eklendi. Bu direnc, cikis pinini olasi asiri akima karsi korumak icin kullanildi. Ortak referans icin Arduino `GND`, breadboard `GND` ve osiloskop `GND` birlikte baglandi.

Baglanti mantigi:

- Arduino `pin 8` -> `2 kOhm` seri direnc -> devrenin bias girisi
- Arduino `GND` -> ortak `GND` rayi
- osiloskop probu -> `Vo`
- osiloskop toprak klipsi -> ortak `GND`

## Sonuclar

Osiloskop `DC coupling` moduna alindiktan ve zaman tabani uygun sekilde ayarlandiktan sonra, hem Arduino cikisinda hem de devrenin uygun olcum noktalarinda duzenli ve tekrar eden pulse sinyali gozlemlendi.

Bu sonuc su acilardan onemlidir:

- Arduino'nun guvenilir bir test kaynagi olarak kullanilabildigi dogrulandi
- osiloskop, breadboard ve ortak `GND` zincirinin dogru calistigi goruldu
- fotodiyot olcum duzeneginin en azindan elektriksel test sinyallerini izleyebildigi teyit edildi

## Karsilasilan Sorunlar

### Breadboard guc raylarinin kopuk olmasi

Breadboard guc raylarinin bazi bolumlerinde sureklilik olmadigi fark edildi. Sorun jumper kablolarla koprulenerek giderildi.

### Zaman tabani uyumsuzlugu

Osiloskopta sinyalin yalnizca tek kenarinin ya da kayiyormus gibi gorunen bir izin izlenmesi, `Time/Div` ayarinin sinyal periyoduna uygun olmamasindan kaynaklandi. Zaman tabani yeniden ayarlaninca duzenli pulse gozlemi yapilabildi.

## Muhendislik Acisindan Cikarim

Bu raporun en faydali sonucu, fotodiyot devresinin dogrudan optik uyartimdan once elektriksel referans sinyalle dogrulanmasinin cok yararli oldugunu gostermesidir. Boylece:

- osiloskop ayarlari bagimsiz sekilde test edilebilir
- devrenin RC cevabi daha kontrollu incelenebilir
- optik deneylerde gorulen anormallikler once elektriksel taraftan elenebilir

## Not

Raporun son kisimlarinda hem `50 Hz` hem de daha yavas pulse mantigina referans veren aciklamalar bulunuyor. Bu tur farklar, farkli deney adimlarinda kullanilan Arduino gecikme surelerinin degismis olmasindan kaynaklaniyor olabilir; dolayisiyla sinyal frekansi yorumlanirken ilgili kod surumunun esas alinmasi gerekir.
