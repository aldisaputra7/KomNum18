

# Pendekatan Deret MacLaurin

## DERET MacLaurin

*DERET MacLaurin* adalah Suatu fungsi *$f(x)$* yang memiliki turunan *$f'(x), f''(x), f'''(x)$* dan seterusnya yang kontinyu dalam interval *a,x I* maka untuk *$x$* disekitar *a* yaitu *|x-a|< R,f(x)* dapat diekspansi kedalam Deret Taylor.

Dalam kasus khusus jika *a=0*, maka disebut *Deret MacLaurin* atau sering disebut Deret Taylor baku. Dan didefinisikan sebagai berikut 

Definisi :
$$
f(x)=f(0)+{f^{1}(0)}x+\frac{f^{2}(0)}{2 !} x^{2}+\frac{f^{3}(0)}{3 !} x^{3}+\frac{f^{4}(0)}{4 !} x^{4} + ...+\frac{f^{n}(0)}{n !} x^{n}
$$
Atau bisa dinyatakan dengan:

$$
f(x)=\sum_{n=0}^\infty \frac{f^{(n)}n(0)}{n!}x^{n}
$$
Deret MacLaurin sangat bermanfaat dalam metode numerik untuk menghitung atau menghampiri nilai-nilai fungsi yang sudah dihitung secara manual seperti nilai *sin x, cos x*, eksponensial, dll. Tentu kita tidak akan bisa menghitung nilai-nilai fungsi tersebut tanpa menggunakan bantuan kalkulator atau tabel. Dalam tulisan ini saya akan mencoba untuk mendekati fungsi-fungsi tersebut menggunakan Deret 
MacLaurin.

## Tugas

Hitunglah *$e^{2x}$* untuk nilai x=4, kemudian expensikan hingga selisih yang dihasilkan kurang dari nilai error yang ditentukan yaitu e < 0,001.

### Penyelesaian

Fungsi awal exponen :
$$
f(x) = e^{2x}\
$$
Dapat juga didefinisikan dengan rumus   : 
$$
e^{2x} = \sum_{n=0}^\infty \frac{(2x)^n}{n!} = \sum_{n=0}^\infty (2)^n\frac{x^n}{n!}
$$
Deret turunan  :
$$
f(a)=e^{2x}
$$
$$
f^1(a)=2e^{2x}
$$

$$
f^2(a)=4e^{2x}
$$

$$
f^3(a)=8e^{2x}
$$

$$
f^4(a)=16e^{2x}
$$

$$
...
$$

$$
f^n(a)=2^{n}e^{2x}
$$



Berikut adalah penyelesaian untuk mencari nilai expansi :
$$
f(x)=f(0)+\frac{f^{1}(0)}{1 !} x+\frac{f^{2}(0)}{2 !} x^{2}+\frac{f^{3}(0)}{3 !} x^{3}+\frac{f^{4}(0)}{4 !} x^{4} + ...+\frac{f^{n}(0)}{n !} x^{n} :
$$
Deret turunan :

$$
f(x)=1+\frac{2}{1 !} x+\frac{4}{2 !} x^{2}+\frac{8}{3 !} x^{3}+\frac{16}{4 !} x^{4} + ...+\frac{2^{n}}{n!} x^{n}
$$
kemudian, nilai x diganti dengan 4 :
$$
f(x)=1+\frac{2}{1 !} 4+\frac{4}{2 !} 4^{2}+\frac{8}{3 !} 4^{3}+\frac{16}{4 !} 4^{4} + ...+\frac{2^{n}}{n !} 4^{n}
$$
perhitungan diatas akan terus menerus berulang hingga nilai selisih mendekati nilai error yang ditentukan yaitu kurang dari 0,001

### Listing Program

Script

```python
import math

error = 0.001
def f(x):
    f_turunan = 1
    current=i=0
    iteration = True
    while iteration:
        old= current
        current += (f_turunan*(x**i))/math.factorial(i)
        print('f ke-', i,'=',current, 'Ea=', current-old )
        if current-old < error:
            iteration = False
        else:
            f_turunan *=2
            i +=1

f(4)
```

Output

```python
f ke- 0 = 1.0 Ea= 1.0
f ke- 1 = 9.0 Ea= 8.0
f ke- 2 = 41.0 Ea= 32.0
f ke- 3 = 126.33333333333333 Ea= 85.33333333333333
f ke- 4 = 297.0 Ea= 170.66666666666669
f ke- 5 = 570.0666666666666 Ea= 273.0666666666666
f ke- 6 = 934.1555555555556 Ea= 364.08888888888896
f ke- 7 = 1350.2571428571428 Ea= 416.1015873015872
f ke- 8 = 1766.35873015873 Ea= 416.1015873015872
f ke- 9 = 2136.226807760141 Ea= 369.8680776014112
f ke- 10 = 2432.12126984127 Ea= 295.89446208112895
f ke- 11 = 2647.317242263909 Ea= 215.195972422639
f ke- 12 = 2790.781223879002 Ea= 143.46398161509296
f ke- 13 = 2879.0667510267513 Ea= 88.28552714774924
f ke- 14 = 2929.515623682608 Ea= 50.448872655856576
f ke- 15 = 2956.4216890990647 Ea= 26.90606541645684
f ke- 16 = 2969.874721807293 Ea= 13.45303270822842
f ke- 17 = 2976.2055607288125 Ea= 6.330838921519444
f ke- 18 = 2979.0192669161543 Ea= 2.8137061873417224
f ke- 19 = 2980.2039853108245 Ea= 1.184718394670199
f ke- 20 = 2980.6778726686925 Ea= 0.47388735786807956
f ke- 21 = 2980.8584011859757 Ea= 0.18052851728316455
f ke- 22 = 2980.924047919533 Ea= 0.06564673355751438
f ke- 23 = 2980.946881565988 Ea= 0.022833646454728296
f ke- 24 = 2980.9544927814727 Ea= 0.0076112154847578495
f ke- 25 = 2980.9569283704277 Ea= 0.0024355889549951826
f ke- 26 = 2980.957677782414 Ea= 0.0007494119863622473
```



Jadi, proses perulangan akan berhenti pada iterasi ke-26 karena selisih dari expansi yang dihasilkan mendekati nilai error yang ditentukan yaitu e < 0,001.

















































<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {inlineMath: [['$$','$$'],['$','$']]}
});
</script>
  <script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>