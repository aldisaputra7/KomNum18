# Turunan Numerik

## Metode Extrapolasi Richardson 

Metode untuk memperoleh rumus hampiran turunan dengan orde yang lebih tinggi dari hampiran dengan orde yang lebih rendah disebut dengan ekstrapolasi. Metode tersebut dikembangkan oleh Lewis Fry Richardson di awal abad 20, sehingga metode tersebut kemudian dikenal dengan Ekstrapolasi Richardson. 

Dalam analisis numerik, Extrapolasi Richardson adalah metode percepatan urutan, yang digunakan untuk meningkatkan laju konvergasi suatu urutan. Extrapolasi RIchardson juga dapat diterapkan pada turunan numerik untuk memperoleh solusi yang lebih teliti.

## Teorema Extrapolasi Richardson

Beda terpusat (Central Difference) orde *$O(h^{2})$*:
$$
{f}'(x)=\frac{f(x+h)-f(x-h)}{2h}+O(h^{2})
$$
Dari beda terpusat diatas dapat dibuat formula dengan ditetapkan *$f(x)$* dan *$x$* tertentu :


$$
\varnothing(h)=\frac{f(x+h)-f(x-h)}{2h}
$$

$$
\varnothing(h)={f}'(x)-a_{2}h^{2}-a_{4}h^{4}-a_{6}h^{6}-\cdots
$$

$$
\varnothing(\frac{h}{2})={f}'(x)-a_{2}\left ( \frac{h}{2} \right )^2-a_{4}\left ( \frac{h}{2} \right )^4-a_{6}\left ( \frac{h}{2} \right )^6-\cdots \\
$$

$$
\varnothing(h)-4\varnothing(\frac{h}{2})=-3{f}'(x)-\frac{3}{4}a_{4}h^{4}-\frac{15}{16}a_{6}h^{6}-\cdots \\
$$

Maka didapatkan formula baru seperti dibawah ini :
$$
f'(x)=\frac{4}{3}\varnothing(\frac {h}{2})-\frac{1}{3}\varnothing(h)+O(h^4)
$$

## Implementasi Pemrograman

berikut program untuk *$f(x) = -0.1x^{4} - 0.15x^{3} - 0.5x^{2} - 0.25x + 1.2$* mulai dengan *$h_{1}=0.5$* dan *$h_{2}=0.25$* menggunakan nilai estimasi *$f'(0.5)$*

**Listing Program**

```python
from math import *
def zeros(n,m):
    Z=[]
    for i in range(n):
        Z.append([0]*m)
    return Z

def D(Func,a,h):
        return (Func(a+h)-Func(a-h))/(2*h)

def Richardson_dif(func,a): 
    
    k=9
    L=zeros(k,k)
    for I in range(k):
        L[I][0]=D(func,a,1/(2**(I+1)))
    for j in range(1,k):
        for i in range(k-j):
            L[i][j]=((4**(j))*L[i+1][j-1]-L[i][j-1])/(4**(j)-1)
    return L[0][k-1]
    

print('f = -0.1*x**4-0.15*x**3-0.5*x**2-0.25*x+1.2 dengan x = 0.5')
print('hasil estimasi =','%04.20f'%Richardson_dif(lambda x: -0.1*x**4-0.15*x**3-0.5*x**2-0.25*x+1.2 ,0.5))

```

**Output**

```python
========================= RESTART: F:\richardson.py =========================
f = -0.1*x**4-0.15*x**3-0.5*x**2-0.25*x+1.2 dengan x = 0.5
hasil estimasi = -0.91250000000000530687
```

nilai sesungguhnya dari *$f'(0.5) = -0,9125$* . Setelah dihitung menggunakan Richardson Extrapolation menghasilkan nilai yang sama persis.