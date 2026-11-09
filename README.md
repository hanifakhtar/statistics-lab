# Statistics Learning Lab — Web Edition

Aplikasi pembelajaran statistika interaktif, dikonversi dari Shiny R ke **HTML, CSS, dan JavaScript**. Dapat di-host gratis melalui **GitHub Pages** tanpa R, Shiny Server, backend, database, CDN, atau API.

© 2026 Hanif Akhtar · https://www.hanifakhtar.com

## Modul

1. Sampling Distribution: Normal, Skewed, Uniform, Bimodal; mean/median; empirical dan theoretical SE.
2. Confidence Interval: repeated sampling, interval coverage, interval width, t confidence interval.
3. p-value Simulator: individual Welch t-study, null tail area, p-value distribution, effect estimates, empirical significant rate.
4. Statistical Power: independent t-test, paired t-test, one-way ANOVA; power curves dan estimasi required sample size.
5. Correlation Explorer: Pearson, Spearman, Fisher z CI / bootstrap CI, outlier, nonlinear relationship, range restriction.
6. Regression Playground: simple OLS, residual diagnostics, quadratic misspecification, heteroscedasticity, CI for mean response dan prediction interval.
7. t-test: Welch, Student, paired, one-sample, effect size Cohen's d/dz, confidence intervals.
8. One-way ANOVA: F test, eta squared, omega squared, group descriptives, Tukey HSD pairwise comparisons.

Semua modul mencakup **preset eksperimen**, parameter interaktif, grafik Plotly lokal, interpretasi, light/dark mode, dan ekspor data simulasi CSV.

## Cara deploy ke GitHub Pages

1. Buat repository publik di GitHub, misalnya `statistics-learning-lab`.
2. Ekstrak file ZIP aplikasi, lalu upload **isi folder** ke bagian root repository (jangan hanya upload ZIP). Pastikan `index.html`, `README.md`, dan folder `assets/` ada pada root repo.
3. Commit changes ke branch `main`.
4. Buka **Settings → Pages → Build and deployment → Source: Deploy from a branch**.
5. Pilih `main` dan folder `/ (root)`, kemudian **Save**.
6. Setelah GitHub Pages berhasil publish, situs umumnya dapat diakses di `https://USERNAME.github.io/statistics-learning-lab/` (ganti `USERNAME` dan nama repo sesuai akun). Lihat URL aktual di halaman Pages.

Jika menggunakan ZIP **standalone** (`index.html` tunggal), cukup upload satu file itu ke root repository. Ukurannya lebih besar karena JavaScript grafik sudah ditanam di dalamnya.

## Menjalankan secara lokal

Buka `index.html` dengan browser modern (Chrome, Edge, Firefox, atau Safari). Alternatif, untuk menjalankan HTTP server lokal:

```bash
python3 -m http.server 8000
```

Kemudian buka `http://localhost:8000`.

## Struktur file

```
index.html
README.md
.nojekyll
assets/
    style.css
    app.js
    math.js
    studentized-range.js
    plotly.min.js
THIRD_PARTY_NOTICES.md
```

## Catatan metode dan keterbatasan

- Ini adalah **konversi fungsional untuk pembelajaran**, bukan hasil transpile R otomatis. Generator angka acak dan rendering plot berbeda dari R Shiny sehingga hasil simulasi dengan seed yang sama tidak identik dengan R, tetapi dapat direproduksi di versi HTML.
- Uji t, korelasi, regresi, ANOVA, dan distribusi Student/F memakai rumus statistik dalam JavaScript. Perhitungan statistik pembelajaran telah diuji dengan beberapa acuan SciPy.
- Power t-test dihitung dengan pendekatan integrasi noncentral t dan aproksimasi Wilson–Hilferty untuk komponen chi-square. Power ANOVA memakai distribusi noncentral F melalui Poisson mixture. **Untuk perencanaan sampel resmi, verifikasi dengan R/JASP/G*Power.**
- Tukey HSD menggunakan interpolasi numerik survival function studentized range yang ditabulasi dari SciPy (grid q 0–12; df 10–2000), sehingga p adjusted dan interval merupakan hasil *aproksimasi interpolasi*.
- Aplikasi memakai data hasil simulasi, tidak mendukung upload dataset riset pengguna saat ini. Semua komputasi simulasi dilakukan **di perangkat pengguna**; tidak ada pengiriman data ke server. Browser hanya menggunakan localStorage untuk menyimpan pilihan tampilan light/dark.
- Github Pages merupakan hosting **static site**, sehingga gratis dan cocok untuk penggunaan publik tanpa backend. Untuk analisis dataset sungguhan, akun pengguna, penyimpanan respons, atau komputasi R khusus, dibutuhkan fitur tambahan.

## Testing

Pengujian otomatis internal dilakukan pada perhitungan modul default, pilihan t-test/ANOVA/relationship alternatif, nilai distribusi t dan F, interpolasi Tukey, dan pemeriksaan browser berbasis Chromium untuk seluruh delapan modul serta tampilan mobile. Kode pengujian tidak diperlukan untuk deployment.
