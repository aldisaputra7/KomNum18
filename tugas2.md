# Newton Raphson

## Metode Newton Raphson

**Metode Newton Raphson** biasa digunakan dalam mencari akar dari suatu persamaan non linier, jika diasumsikan *$f$* mempunyai turunan kontinu *$f'$*. Metode Newton Raphson merupakan salah satu metode terpopuler untuk menghampiri penyelesaian *$f(x)=0$* secara iteratif.  Metode ini dianggap  lebih mudah dari Metode Bagi Dua (Bisection Method) karena metode ini menggunakan pendekatan satu titik sebagai titik awal. Semakin dekat titik awal yang kita pilih dengan akar sebenarnya, maka semakin cepat konvergen ke akarnya.

![newton raphson](..\assets\images\newton-raphson.jpg)

Prosedur Metode Newton :

menentukan *$x_0$* sebagai titik awal, kemudian menarik garis lurus (misal garis $\imath$ ) yang menyinggung titik *$f(x_0)$* . Hal ini berakibat garis $\imath$ memotong sumbu *$x$* di titik *$x_1$* Setelah itu diulangi langkah sebelumnya tapi sekarang *$x_1$* dianggap sebagai titik awalnya. Dari mengulang langkah-langkah sebelumnya akan mendapatkan *$x_2 , x_3 , ... , x_n$* dengan *$x_n$* yang diperoleh adalah bilangan riil yang merupakan akar atau mendekati akar yang sebenarnya.

Perhatikan gambar diatas untuk menurunkan rumus **Metode Newton-Raphson**

persamaan garis $\imath : y - y_0 = m(x - x_0)$
$$
y - f(x_0) = f'(x_0)(x - x_0)
$$
*$x_1$* perpotongan garis $\imath$ dengan sumbu - *x*
$$
0 - f(x_0) = f'(x_0)(x - x_0)
$$
*y = 0* dan *x = $x_1$* maka koordinat titik (*$x_1$*,0)
$$
- \frac{f(x_0)}{f'(x_0)} = (x_1 - x_0)
$$
sehingga di dapat sebuah rumus :
$$
x_1 = x_0 - \frac{f(x_0)}{f'(x_0)} , x_2 = x_1 - \frac{f(x_1)}{f'(x_1)}, ... , x_n = x_{n-1} - \frac{f(x_{n-1})}{f'(x_{n-1})}
$$

------

### **Algoritma dan Pemrograman Newton Rhapson**

Dari rumus yang kita dapat diatas kita dapat menyusun sebuah algoritma yang nantinya akan dibuat menjadi sebuah program. Algoritma menyusun akar - akar *$f(x) = 0$* sebagai berikut :

1. Didefinisikan fungsi *$f$* dengan *$f(x)$* dan *$f'(x)$*
2. Ditentukan Epsilon sebagai Toleransi kesalahan serta iterasi maksimum untuk *Stopping Condition*
3. Dipilih tebakan awal *$x_0$* 
4. Dihitung *f($x_0$)* dan *f'($x_0$)*
5. Dihitung *$x_b = x_0 - \frac{f(x_0)}{f'(x_0)}f'(x_0) \neq 0$* .  jika *$f'(x_0) = 0$* kembali ke langkah - 3
6. Jika *$\left | x_b - x_0 \right | < \varepsilon$* . itersasi lebih dari iterasi maksimum tulis *$x_{hampiran} = x_b$* sebagai hasil hampiran akar; jika tidak, lanjutkan ke langkah berikutnya.
7. Ganti nilai *$x_0$* dengan *$x_0 = x_b$* dan kembali ke langkah-4

------

### **Implementasi Pemrograman**

**Script :**

```python
import math
e = 2.71828

def fungsi(x):
    x = float((e**x) - (4*x))
    return x

def fungsiturunan(x):
    x = float((e**x) - (4))
    return x

x = float(input('Masukkan nilai awal = '))
error = float(input('Masukkan nilai error = '))
perulangan = int(input('Masukkan maksimal pengulangan = '))

iterasi = 0
selisih = error+1
while iterasi <= perulangan  and selisih>error :
    iterasi += 1
    f_2 = x - (fungsi(x)/fungsiturunan(x))
    selisih = math.fabs(f_2 - x)
    x = f_2
    print("Iterasi ke = ",iterasi,", x = ",f_2, ", f(",f_2,") = ",fungsi(f_2),", selisih = ",error)
    if iterasi <= perulangan:
        print("Perulangan Mencapai Batas Maksimal dengan hasil = ", f_2)
    else :
        print("Toleransi tidak terpenuhi")

```

#### Output :

```python
Masukkan nilai awal = 2
Masukkan nilai error = 0.01
Masukkan maksimal pengulangan = 5
Iterasi ke =  1 , x =  2.180273095450679 , f( 2.180273095450679 ) =  0.1276171155949779 , selisih =  0.01
Perulangan Mencapai Batas Maksimal dengan hasil =  2.180273095450679
Iterasi ke =  2 , x =  2.1539532848570624 , f( 2.1539532848570624 ) =  0.0030383334624808356 , selisih =  0.01
Perulangan Mencapai Batas Maksimal dengan hasil =  2.1539532848570624
Iterasi ke =  3 , x =  2.153295473390226 , f( 2.153295473390226 ) =  1.8681594777802957e-06 , selisih =  0.01
Perulangan Mencapai Batas Maksimal dengan hasil =  2.153295473390226
```



#### Penjelasan :

1. Importh Library math
2. karena kita menggunakan contoh fungsi *$f(x) = e^x - 4X$* maka kita membuat sebuah fungsi yang sesuai , dan juga fungsi turunannya yaitu *$f'(x) = e^x - 4$*
3. Membuat sebuah inputan untuk X , Error / Epsilon , serta Maksimal perulangan untuk stopping condition
4. lalu deklarasikan iterasi = 0 untuk perulangan yang ke 0  nantinya dan akan ditambah setiap kali perulangan
5. deklarasikan selisih untuk *$x_b - x_0$*  untuk perbandingan
6. lakukan perulangan dengan kondisi iterasi kurang dari sama dengan inputan maksimal iterasi dan selisih lebih dari error / epsilon
7. hitung *$x_b$* dengan rumus yang sudah kita dapatkan sebelumnya
8. lalu lakukan perbandingan jika mencapai nilai *True* maka toleransi tidak terpenuhi namun perulangan sudah mencapai batas
9. jika pengecekan selisih > error bernilai bernilai *True* maka toleransi akan terpenuhi dengan nilai error serta fungsi x pada iterasi ke n 