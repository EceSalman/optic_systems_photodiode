# star_tracking_all

Bu repo, star tracker optigi ve algilama zinciri uzerine yuruttugum teknik arastirma notlarini, ara raporlari ve PDF/Markdown dokumanlarini duzenli sekilde toplamak icin kullaniliyor.

Repo amaci iki katmanli:

- gunluk arastirma ve teknik dusunceyi kaybetmemek
- olgunlasan notlari paylasilabilir teknik dokumanlara donusturmek

## Repo mantigi

Bu repo bir "nihai tasarim dokuman seti" degil. Daha cok:

- arastirma notlari
- teknik ara raporlar
- PDF kaynaklari
- Markdown'a aktarilmis okunabilir surumler

bir arada tutulan duzenli bir muhendislik deposu olarak kurgulandi.

## Klasor yapisi

- `pdf/`: kaynak PDF belgeleri
- `docs/`: Markdown notlari, donusturulmus metinler ve ek aciklamalar

## Belge dizini

| Konu | Durum | Markdown | PDF |
| --- | --- | --- | --- |
| Baffle temel raporu | Taslak / donusturulmus not | [`docs/baffle_WO_vanes_rapor.md`](./docs/baffle_WO_vanes_rapor.md) | [`pdf/baffle_WO_vanes_rapor.pdf`](./pdf/baffle_WO_vanes_rapor.pdf) |
| Baffle aciklama notu | Yardimci not | [`docs/baffle_raporu_hakkinda.md`](./docs/baffle_raporu_hakkinda.md) | - |
| CMOS APS / PPD star tracker notu | Duzenlenmis teknik not | [`docs/CMOS_APS_PPD_star_tracker.md`](./docs/CMOS_APS_PPD_star_tracker.md) | [`pdf/CMOS_APS_PPD_star_tracker.pdf`](./pdf/CMOS_APS_PPD_star_tracker.pdf) |
| Fotodiyot lab raporu | Duzenlenmis teknik not | [`docs/Fotodiyot_Lab_Raporu.md`](./docs/Fotodiyot_Lab_Raporu.md) | [`pdf/Fotodiyot_Lab_Raporu.pdf`](./pdf/Fotodiyot_Lab_Raporu.pdf) |

Detayli belge listesi icin: [`docs/README.md`](./docs/README.md)

## Calisma prensibi

Ileride bu repo su sekilde buyuyecek:

1. Yeni teknik calisma once PDF veya ham not olarak uretilir.
2. Uygunsa Markdown surumu `docs/` altina eklenir.
3. README'deki belge dizinine ilgili kayit eklenir.
4. Taslak, ara not ve daha olgun teknik metinler birbirinden ayristirilarak tutulur.

## Teknik odak alanlari

- star tracker optigi
- baffle ve stray light kontrolu
- sensor mimarisi
- PSF, centroid ve goruntu kalitesi
- algilama zinciri ve yonelim dogrulugu

## Not

Buradaki bazi belgeler ham PDF donusumu oldugu icin dil, karakter kodlamasi veya bicim acisindan tam temiz olmayabilir. Bu normaldir; repo hem arastirma arsivi hem de giderek temizlenen teknik dokuman havuzu gibi kullanilmaktadir.
