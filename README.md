# 103. README / Catatan Praktikum

## Nama dan NRP

- Mario Napitupulu — 5025241085
- Nathanael Oliver Amadhika Yuswana — 5025241109

## Nama Asset

**Kotak Perkakas Kestrel-09** (`P09_02_Kotak_Perkakas.blend`)

## Konsep Asset

Kestrel-09 adalah kotak perkakas mekanis bergaya sci-fi untuk membawa perkakas servis dan modul kecil di lapangan. Body berwarna biru gelap menjadi struktur utama; panel kontrol, handle, kaki, pelindung sudut, ventilasi, sirip grille, fastener, dan aksen amber membuatnya terbaca sebagai perlengkapan industri. Handle melengkung di bagian atas membantu menunjukkan fungsi untuk dibawa.

## Primitive Awal

- **Cube** untuk body berukuran 4 × 3 × 2,4 unit, skid bawah, kaki, bumper, panel kontrol, guard, rusuk, dan detail kotak lainnya.
- **Plane/quad** untuk pelat armor samping, badge, dan panel tipis yang kemudian diberi ketebalan.
- **Cylinder** 24 sisi untuk fastener dan inti fastener.
- **Bezier curve** untuk handle atas; radius tabung dibuat dengan pengaturan bevel pada curve.

## Operasi Modeling yang Digunakan

1. Menetapkan dimensi dan posisi komponen dengan nilai numerik, lalu menerapkan scale sebelum memasang bevel.
2. Membagi dua area body secara vertikal pada X = −1,2 dan X = 1,2. Pemotongan quad ini dibuat dengan BMesh sebagai padanan loop cut pada posisi presisi.
3. Memilih face tengah pada sisi depan, membuat inset, lalu meng-extrude face ke dalam untuk membentuk recess panel.
4. Menyusun panel kontrol dan detail sebagai komponen terpisah agar dapat diatur dan diperiksa melalui Outliner.
5. Menggunakan Mirror dan Array untuk menggandakan detail yang simetris atau berulang tanpa membuat tiap salinan secara manual.
6. Membuat diagonal Knife split pada panel aksen samping dan handle Bezier dengan radius terkontrol.

## Modifier yang Digunakan

- **Bevel** untuk chamfer pada body dan tepi komponen; lebar disesuaikan dengan skala bagian.
- **Weighted Normal** untuk membantu shading bidang keras setelah bevel.
- **Mirror** pada `Front_Guards_Mirror`, pada sumbu X, untuk menghasilkan guard kiri dan kanan.
- **Array** pada `Top_Vent_Rib_Array` sebanyak 6 rib dan `Front_Grille_Fin_Array` sebanyak 7 sirip.
- **Solidify** pada armor samping (ketebalan 0,075), badge (0,035), dan panel Knife (0,045).
- **Curve bevel** pada handle Bezier, dengan depth 0,045 dan resolution 4, untuk membentuk tabung.

## Bagian yang Menggunakan Extrude

Face tengah di bagian depan body di-extrude ke arah dalam sebesar 0,12 unit setelah inset. Operasi ini membentuk recess tempat panel kontrol dipasang. Teks label kecil juga memakai extrude curve 0,002 unit.

## Bagian yang Menggunakan Inset

Face tengah pada sisi depan body di-inset sebesar 0,16 unit. Inset ini membuat perimeter tepi sebelum face didorong ke dalam.

## Bagian yang Menggunakan Loop Cut

Body utama mendapat dua potongan vertikal pada X = −1,2 dan X = 1,2 untuk membagi area depan secara seimbang. Script membangunnya dengan operasi bisect BMesh pada quad; tujuannya sama seperti menempatkan dua loop cut dengan Ctrl+R pada posisi tersebut.

## Bagian yang Menggunakan Bevel

Bevel dipakai pada tepi body, skid, bumper, kaki, panel, guard, rusuk, fastener, dan detail mekanis lain. Body memakai lebar 0,055 dengan 3 segmen; pelat armor samping memakai 0,025 dengan 2 segmen. Lebar bagian kecil dibuat lebih tipis agar sudutnya tidak terpotong berlebihan.

## Cleanup yang Dilakukan

- Menerapkan scale pada primitive berdimensi sebelum bevel; body disimpan pada scale (1, 1, 1).
- Menjalankan **Merge by Distance** pada vertex body dengan jarak 0,0001 untuk menghapus vertex yang bertumpuk.
- Menghitung ulang face normal body setelah operasi topology.
- Memakai Weighted Normal pada komponen ber-bevel untuk menjaga shading bidang datar.
- Memisahkan body, panel, fastener, kaki, handle, dan detail berulang dengan nama fungsi yang jelas di Outliner.

## Challenge yang Dikerjakan

- **A — Symmetric Prop:** guard depan dibuat berpasangan dengan Mirror pada sumbu X.
- **B — Repeated Mechanical Detail:** enam rib ventilasi dan tujuh sirip grille dibuat dengan Array.
- **C — Thin Panel + Solidify:** pelat armor samping, badge, dan panel tipis mendapat ketebalan dengan Solidify.
- **D — Advanced Paneling:** panel depan bertingkat memakai Loop Cut, Inset, dan Extrude untuk membuat recess.
- **E — Knife Detail:** diagonal Knife split membagi aksen samping menjadi dua face.
- **F — Controlled Curved Form:** handle atas dibuat dari Bezier curve dengan radius tabung terkontrol.
- **G — Modular Asset:** bagian utama dan detail dipisah menjadi object bernama di Outliner.
- **H — Precision Modeling:** dimensi, offset, dan posisi komponen ditetapkan dengan nilai numerik dan sumbu yang konsisten.

## Kendala

Bevel dapat tampak terlalu lebar atau tidak konsisten ketika scale object belum diterapkan. Panel depan juga harus ditempatkan dengan hati-hati supaya tidak menembus body atau menutupi recess. Potongan topology harus simetris agar panel kiri dan kanan tetap seimbang.

## Solusi

Scale diterapkan sebelum bevel dan lebar bevel disesuaikan terhadap ukuran tiap komponen. Posisi panel diatur memakai koordinat numerik. Dua potongan vertikal body ditempatkan pada X = ±1,2, sedangkan inset dan extrude menggunakan nilai tetap agar recess terukur. Mirror dan Array menjaga simetri dan jarak detail tetap konsisten.

## Screenshot

- `screenshot_blockout.png` — bentuk dasar dan proporsi awal.
- `screenshot_modeling.png` — body, panel, dan komponen utama.
- `screenshot_final.png` — hasil akhir Kotak Perkakas Kestrel-09.
