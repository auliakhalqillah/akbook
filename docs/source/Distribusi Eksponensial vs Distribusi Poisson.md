# Distribusi Eksponensial vs Distribusi Poisson
Suatu data tidak terlepas dari karakter sebaran data atau yang sering disebut dengan istilah distribusi data. Distribusi menjelaskan sebaran suatu nilai dalam frekuensi (jumlah) atau peluang kemunculan (probabilitas). Beberapa jenis distribusi yang umum diketahui selain distribusi normal dan binomial di antaranya adalah distribusi eksponensial dan distribusi Poisson. Kedua jenis distribusi ini secara umum memiliki kesamaan untuk memodelkan peluang berdasarkan kejadian acak yang terjadi secara independen.

**Distribusi Eksponensial**
1.  memodelkan peluang antara dua kejadian berdasarkan data kontinu (termasuk bilangan berkoma)
2. berorientasi pada “berapa lama”
3. memiliki rentang tertentu (lebih kecil atau lebih besar)
4. parameter yang digunakan adalah laju (rate, $\lambda$), dimana nilainya lebih dari 0
5. Probability Density Function (PDF): $f(x)=\lambda e^{-\lambda x}$
6. Cumulative Density Function (CDF):
	$P(X \le x) = F(x) = 1 - e^{-\lambda x}$
	$P(X > x) = e^{-\lambda x}$
7. Nilai $x$ adalah bilangan random dari suatu variabel $X$

_Contoh_
Berapa peluang untuk seorang barista membuat kopi kurang dari 10 menit jika berdasarkan data barista mampu membuat 4 kopi selama 12 menit?

 - 4 kopi selama 12 menit, artinya rata-rata ($\mu$) membuat 1 kopi adalah 3 menit, $\mu = 3$
 - maka $\lambda = \frac {1}{\mu}=\frac {1}{3} = 0.33$
 - $P(X \le 10) = 1 - e^{-0.33 10} = 1 - 0.036=0.964 \simeq 96.4\%$

Artinya, barista berpeluang 96.4% secara intens membuat kopi kurang dari 10 menit

**Distribusi Poisson**
1.  memodelkan peluang jumlah kejadian berdasarkan data diskrit (bilangan bulat tidak negatif)
2. berorientasi pada “berapa banyak”
3. memiliki nilai yang tetap (fixed)
4. parameter yang digunakan adalah lau (rate, $\lambda$), dimana nilainya lebih dari 0
5. Dihitung menggunakan Probability Mass Function (PMF)
	$P(X = k) = \frac {\lambda^k e^{-\lambda}}{k!}$
	dimana $k$ adalah jumlah suatu kejadian pada suatu variabel $X$

_Contoh_
Berapa peluang untuk seorang barista membuat tepat 6 kopi dalam 12 menit selanjutnya jika barista membuat rata-rata 4 kopi dalam 12 menit?

 - Perlu ditekankan bahwa pada distribusi Poisson lebih berfokus pada jumlah kejadian, maka laju ($\lambda$=4) dan jumlah kejadian yang diinginkan, $k=6$
 - $P(X=6)=\frac {4^6 e^{-4}}{6!} = \frac {4096 x 0.018315}{720}=0.1042 \simeq 10.42\%$

Kesimpulannya, barista hanya memiliki peluang sekitar 10.42% untuk membuat tepat 6 kopi dalam 12 menit

