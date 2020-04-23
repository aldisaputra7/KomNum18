# Integrasi Numerik

## Metode Recursive Trapezoid

Metode trapesium rekursif adalah suatu metode pendekatan integral numerik dengan polinom orde satu. Dalam metode ini, kurva yang berbentuk lengkung di dekatkan dengan garis lurus sedemikian sehingga bentuk dibawah kurvanya seperti trapesium.

![recursive trapezoid](..\assets\images\trapezoid.JPG)

Luas dibawah kurva dengan fungsi *$f(x)$* antara *$a=x_{0}$* dan *$b=x_{1}$* didekati oleh suatu trapesium. Dalam trapesium ini f(a) dan f(b) sebgaai alas dan sisi atas dan *$b-a$* adalah tinggi dari trapesium tersebut. Menurut teorema dasar rumus integral dapat dihitung dengan rumus berikut:
$$
{\displaystyle \int _{a}^{b}f(x)\,dx=F(b)-F(a)}
$$
Aturan trapesium bekerja dengan cara mendekati daerah bawah grafik fungsi f(x) sebagai trapesium dan menghitung luas daerah yang terasir.

Estimasi berdasarkan satu interval :
$$
h=b-a
$$

$$
R(0,0) = \frac{b-a}{2}(f(a)+f(b))
$$

Estimasi berdasarkan 2 interval :
$$
h = \frac{b-a}{2}
$$

$$
R(1,0) = \frac{b-a}{2}\left [(f(a+h)+\frac{1}{2}(f(a)+f(b)) \right ]
$$

$$
R(1,0) = \frac{1}{2}R(0,0)+h[f(a+h)]
$$

- *$R(0,0)$* : berdasarkan pada estimasi sebelumnya dan
- *$h[f(a)+(h)]$* : berdasarkan pada titik baru



## Formula Metode Recursive Trapezoid

Jadi, dari penjabaran estimasi interval diatas didapatkan formula untuk metode trapesium rekursif seperti berikut :
$$
R(0,0) = \frac{b-a}{2}(f(a)+f(b))
$$

$$
R(n,0) = \frac{1}{2}R(n-1,0)+h\left [\sum_{k=1}^{2^{n-1}}f(a+(2k-1)h) \right ]
$$

dengan  menggunakan
$$
h=\frac{b-a}{2^n}
$$

## Pemrograman Integral Trapezoid

**Listing Program** 

```python
def fungsi (x) :
    y = 1/(1+x)
    return y

print("f(x) = 1/(1+x)")
a = float(input("Masukkan batas bawah integral : "))
b = float(input("Masukkan batas atas integral : "))
c = int(input("masukkan n : "))
eror = []

for iterasi in range (0,c):
    n=2**iterasi
    h=(b-a)/n

    xi = a
    y = 0
    for i in range(1,n):
        xi = xi+h
        y += fungsi(xi)
    hasil = (h)*((fungsi(a)+(2*y)+fungsi(b))/2)
    eror.append(hasil)
    print ('iterasi ke-',iterasi+1,"n:",n,'hasil =',hasil)
print (eror[iterasi-1])
print(eror[iterasi])
akhir = (eror[iterasi-1]-eror[iterasi])
print(akhir)
print ("estimasi error : "+str(akhir))


```

Output :

```python
f(x) = 1/(1+x)
Masukkan batas bawah integral : 3
Masukkan batas atas integral : 4
masukkan n : 6
iterasi ke- 1 n: 1 hasil = 0.225
iterasi ke- 2 n: 2 hasil = 0.2236111111111111
iterasi ke- 3 n: 4 hasil = 0.22326066391468866
iterasi ke- 4 n: 8 hasil = 0.2231728434998559
iterasi ke- 5 n: 16 hasil = 0.22315087523974755
iterasi ke- 6 n: 32 hasil = 0.22314538235056947
0.22315087523974755
0.22314538235056947
5.492889178088101e-06
estimasi error : 5.492889178088101e-06
```

