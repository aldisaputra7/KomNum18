# Sistem Persamaan Linier

## Metode Eliminasi Gauss

Metode eliminasi Gauss adalah metode yang dikembangkan dari metode eliminasi yaitu dengan menghilangkan atau mengurangi jumlah variabel sehingga dapat diperoleh nilai dari suatu variabel bebas. Metode Gauss ini digunakan untuk menyelesaikan sebuah sistem persamaan linier dengan mengubah SPL (Sistem Persamaan Linier) tersebut kedalam bentuk sistem persamaan linier berbentuk segitiga atas, yakni yang semua koefisien dibawah diagonal utamanya bernilai nol. Bentuk segitiga atas ini dapat diselesaikan dengan menggunakan subtitusi. Sebelum merubah menjadi matriks segitiga atas, matriks harus dirubah menjadi augmented matriks :

**Augmented (A) = [A B]**

![augmented matriks](..\assets\images\matriks-A.JPG)

augmented matriks dirubah menjadi matriks segitiga atas dengan menggunakan OBE (Operasi Baris Elementer), seperti persamaan berikut :

![matrik gauss](..\assets\images\matriks-B.JPG)

Maka didapatkan penyeleseaian sebagai berikut :
$$
x_{n}= \frac{b_{n} }{a_{n,n}}
$$

### Implementasi Pemrograman 

Berikut program untuk persamaan linier dibawah ini:

1 . 3x + y + 2z = 4

2 . 3x + 3y + z = 5

3 . 2x + y + 2z = 2

**Listing Program :**

```
import numpy as np

#Definisi Matrix
A = []
B = []

n = int(input("Masukkan ukuran Matrix: "))
for i in range(n):
    baris=[]
    for i in range(n):
        a=int(input("Masukkan Nilai: "))
        baris.append(a)
    A.append(baris)
for i in range(n):
    h = int(input("Masukkan Hasil: "))
    B.append(h)

Matrix=np.array(A,float)
Hasil=np.array(B,float)

n=len(Matrix)

#Eliminasi Gauss
for k in range(0,n-1):
    for i in range(k+1,n):
        if Matrix[i,k]!=0 :
            lam=Matrix[i,k]/Matrix[k,k]
            Matrix[i,k:n]=Matrix[i,k:n]-(Matrix[k,k:n]*lam)
            Hasil[i]=Hasil[i]-(Hasil[k]*lam)

print("Matrix A : ",'\n',Matrix)

#Subtitusi
x=np.zeros(n,float)
for m in range(n-1,-1,-1):
    x[m]=(Hasil[m]-np.dot(Matrix[m, m+1:n], x[m+1:n]))/Matrix[m,m]
    print('Nilai X ',m+1, '=',x[m])
```

**Output :**

```python
Masukkan ukuran Matrix: 3
Masukkan Nilai: 3
Masukkan Nilai: 1
Masukkan Nilai: 2
Masukkan Nilai: 3
Masukkan Nilai: 3
Masukkan Nilai: 1
Masukkan Nilai: 2
Masukkan Nilai: 1
Masukkan Nilai: 2
Masukkan Hasil: 4
Masukkan Hasil: 5
Masukkan Hasil: 2
Matrix A :  
 [[ 3.          1.          2.        ]
 [ 0.          2.         -1.        ]
 [ 0.          0.          0.83333333]]
Nilai X  3 = -0.9999999999999998
Nilai X  2 = 1.1102230246251565e-16
Nilai X  1 = 2.0
```



## Metode Gauss Jacobi

Metode iterasi Jacobi merupakan salah satu metode tak langsung, yang bermula dari suatu hampiran penyelesaian awal dan kemudian memperbaiki hampiran dalam tak berhingga namun langkah kovergen. Metode iterasi Jacobi ini digunakan untuk menyelesaikan persamaan linier berukuran besar dan proporsi keofeisian nolnya besar. 

Jika diubah dari persamaan linier, maka akan menjadi : *$Ax=b$*

diketahui bahwa matriks  A dapat dituliskan sebagai A=L+D+U, dengan L adalah matriks segitiga bawah, D adalah matriks diagonal, dan U adalah matriks segitiga atas. Lalu persamaan tersebut diubah menjadi :
$$
Dx + (L + U)x = B
$$

$$
x = D^{-1}[b-(L +U)x]
$$

Jika ditulis dalam aturan iteratif, maka metode iterai Jacobi dapat ditulis sebagai berikut:
$$
X^{(k)}=D^-1(b-(L+U)X^{(k-1)}
$$
Dimana k merupakan banyaknya iterasi. Jika *$x^{(k)}$* menyatakan hampiran ke *$-k$*
penyelesaian SPL, maka *$x^{(0)}$* adalah hampiran awal.


$$
x_{i}^{(k)}=\frac{1}{a_{ii}}(\sum x^{n}_{j\ne i}),i = 1,2,...n;k=1,2,3,...,
$$


Suatu matriks A berukuran *$nxn$* dikatakan dominan secara diagonal apabila :
$$
|a_{ii}|>|a_{i,1}|+...+|a_{i,i-1}|+|a_{i,i+1}|+...+|a_{in}|
$$
untuk *$i =1,2,3,...,n$*

### Implementasi Pemrograman

Berikut program untuk persamaan linier dibawah ini:

1 . 3x + y + 2z = 4

2 . 3x + 3y + z = 5

3 . 2x + y + 2z = 2

**Listing Program**

```python
from pprint import pprint
from numpy import array, zeros, diag, diagflat, dot
import numpy as np

def jacobi(A,b,N=25,x=None):
        #Membuat iniial guess                                       
    if x is None:
        x = zeros(len(A[0]))

    #Membuat vektor dari elemen matrix A                             
    D = diag(A)
    R = A - diagflat(D)

    #Iterasi                                                                                          
    for i in range(N):
        x = (b - dot(R,x)) / D
    return x

Mat1 = []
Mat2 = []

n = int(input("Masukkan ukuran Matrix: "))
for i in range(n):
    baris=[]
    for i in range(n):
        a=int(input("Masukkan Nilai: "))
        baris.append(a)
    Mat1.append(baris)
for i in range(n):
    h = int(input("Masukkan Hasil: "))
    Mat2.append(h)

A = array(Mat1,float)
b = array(Mat2,float)
x=len(Mat1)
guess = np.zeros(x,float)

sol = jacobi(A,b,N=25,x=guess)

print("A:")
pprint(A)

print("b:")
pprint(b)

print("x:")
pprint(sol)

```

**Output:**

```python
Masukkan ukuran Matrix: 3
Masukkan Nilai: 3
Masukkan Nilai: 1
Masukkan Nilai: 2
Masukkan Nilai: 3
Masukkan Nilai: 3
Masukkan Nilai: 1
Masukkan Nilai: 2
Masukkan Nilai: 1
Masukkan Nilai: 2
Masukkan Hasil: 4
Masukkan Hasil: 5
Masukkan Hasil: 2
A:
array([[3., 1., 2.],
       [3., 3., 1.],
       [2., 1., 2.]])
b:
array([4., 5., 2.])
x:
array([105.35701362, 119.25506258, 130.92310531])
```



## Metode Gauss Seidel

Metode Gauss Seidel digunakan untuk menyelesaikan sistem persamaan linier (SPL) berukuran besar dan proporsi koefisien nolnya besar, seperti sistem-sistem yang banyak ditemukan dalam sistem persamaan diferensial. Metode iterasi Gauss Seidel dikembangkan dari gagasan metode iterasi pada solusi persamaan tak linier. Dengan metode Gauss seidel sesatan pembultan dapat diperkecil karena dapat meneruskan iterasi sampai solusinya seteliti mungkin sesuai dengan batass sesatan yang diperbolehkan.

Rumus iterasi untuk hampiran ke-k pada metode Gauss Seidel adalah sebagai berikut. Untuk *$i=1,2,...,n$* dan *$k=1,2,3,...$*
$$
x_{i}^{(k)} = \frac{1}{a_{ii}}(b_{i} - \sum_{j=1}^{i-1}a_{ij}x_{j}^{(k)} - \sum_{j=i+1}^{n}a_{ij}x_{j}^{(k-1)})
$$
dengan syarat *$a_{ii} \neq 0$*. Metode iterasi Gauss-Seidel dapat dinyatakan dalam bentuk matriks. Nyatakan matriks koefisien A sebagai *$A=D+(L+U)$*, dengan L dan U berturut-turut adalah matriks segitiga bawah dan atas dengandiagonal nol dan D matriks diagonal. 

Rumus iterasi Gauss-Seidel dapat ditulis dalam bentuk :
$$
X^{(k)}=D-1(b-LX^{(k)}-UX^{(k-1)}
$$

$$
\rightarrow (D+L)x^{(k)} = b-Ux^{(k-1)}
$$

$$
\rightarrow x^{(k)} = (D+L)^{-1}(b-Ux^{(k-1)})
$$

yang menghasilkan:
$$
 X^{(k)}=(D+L)^{-1} UX^{(k-1)}+(D+L)^{-1}b)
$$
Metode iterasi Gauss-Seidel hampir sama dengan metode iterasi Jacobi. Perbedaannya hanya terletak pada penggunaan nilai elemen vektor *$x^{baru}$* yang langsung digunakan pada persamaan di bawahnya.

### Implementasi Pemrograman 

Berikut program untuk persamaan linier dibawah ini:

1 . 3x + y + 2z = 4

2 . 3x + 3y + z = 5

3 . 2x + y + 2z = 2

**Listing Program :**

```python
def seidel(a, x ,b): 
    #Mencari Panjang Matrix  
    n = len(a)               
    for j in range(0, n):        
        d = b[j]                 
        #Menghitung xi, yi, zi 
        for i in range(0, n):    
            if(j != i): 
                d-=a[j][i] * x[i]        
        x[j] = d / a[j][j] #Solusi   
    return x     

m=int(input("Masukkan Panjang Matrix: "))
a=[]
b=[]
for k in range(m):
    mat1=[]
    for i in range(m):
        l=float(input("Masukkan a"+str(k+1)+","+str(i+1)+": "))
        mat1.append(l)
    h=float(input("Masukkan Hasil: "))
    b.append(h)
    a.append(mat1)

n = 3                           
x = [0, 0, 0]                        
print(x) 

for i in range(0, 100):          
    x = seidel(a, x, b)
    print(x)                 
```

**Output:**

```python
Masukkan Panjang Matrix: 3
Masukkan a1,1: 3
Masukkan a1,2: 1
Masukkan a1,3: 2
Masukkan Hasil: 4
Masukkan a2,1: 3
Masukkan a2,2: 3
Masukkan a2,3: 1
Masukkan Hasil: 5
Masukkan a3,1: 2
Masukkan a3,2: 1
Masukkan a3,3: 2
Masukkan Hasil: 2
[0, 0, 0]
[1.3333333333333333, 0.3333333333333333, -0.4999999999999999]
[1.5555555555555554, 0.27777777777777796, -0.6944444444444443]
[1.7037037037037035, 0.19444444444444453, -0.8009259259259258]
[1.802469135802469, 0.1311728395061731, -0.8680555555555555]
[1.8683127572016458, 0.08770576131687269, -0.9121656378600822]
[1.9122085048010973, 0.05851337448559687, -0.9414651920438957]
[1.941472336534065, 0.03901606081390022, -0.9609803669410151]
[1.9609815576893765, 0.026011897957628555, -0.9739875066681908]
[1.9739877051262509, 0.017341463763146048, -0.982658437007824]
[1.9826584700841672, 0.011561008918440733, -0.9884389745433876]
[1.9884389800561115, 0.00770734479168426, -0.9922926524519536]
[1.9922926533707408, 0.005138230779910343, -0.994861768760696]
[1.994861768913827, 0.0034254873397382792, -0.9965745125836962]
[1.996574512609218, 0.0022836582520140425, -0.997716341735225]
[1.9977163417394788, 0.0015224388389296628, -0.9984775611589436]
[1.9984775611596526, 0.001014959226661875, -0.9989850407729836]
[1.9989850407731018, 0.000676639484559316, -0.9993233605153815]
[1.999323360515401, 0.00045109298972612066, -0.9995489070102641]
[1.9995489070102674, 0.00030072865982067043, -0.9996992713401778]
[1.9996992713401784, 0.00020048577321415037, -0.9997995142267855]
[1.9997995142267857, 0.0001336571821428656, -0.9998663428178571]
[1.9998663428178574, 8.91047880950957e-05, -0.9999108952119049]
[1.9999108952119051, 5.94031920632491e-05, -0.9999405968079368]
[1.999940596807937, 3.960212804203037e-05, -0.9999603978719579]
[1.999960397871958, 2.6401418694699252e-05, -0.9999735985813054]
[1.9999735985813054, 1.760094579631814e-05, -0.9999823990542036]
[1.9999823990542034, 1.1733963864409466e-05, -0.9999882660361356]
[1.9999882660361354, 7.82264257640867e-06, -0.9999921773574236]
[1.9999921773574236, 5.215095050914442e-06, -0.9999947849049491]
[1.999994784904949, 3.4767300339429616e-06, -0.999996523269966]
[1.9999965232699661, 2.317820022616305e-06, -0.9999976821799774]
[1.9999976821799776, 1.5452133482381687e-06, -0.9999984547866517]
[1.9999984547866516, 1.030142232294473e-06, -0.9999989698577678]
[1.9999989698577678, 6.867614881963154e-07, -0.9999993132385119]
[1.999999313238512, 4.5784099193350397e-07, -0.9999995421590081]
[1.9999995421590082, 3.0522732781997536e-07, -0.9999996947726721]
[1.9999996947726721, 2.0348488523798855e-07, -0.9999997965151147]
[1.9999997965151148, 1.3565659014632322e-07, -0.9999998643434099]
[1.99999986434341, 9.043772660384992e-08, -0.9999999095622734]
[1.9999999095622734, 6.029181776057158e-08, -0.9999999397081822]
[1.9999999397081822, 4.019454517371438e-08, -0.9999999598054549]
[1.9999999598054548, 2.6796363461478734e-08, -0.9999999732036364]
[1.9999999732036364, 1.7864242455682227e-08, -0.9999999821357577]
[1.9999999821357577, 1.1909494797753458e-08, -0.999999988090505]
[1.999999988090505, 7.939663371203665e-09, -0.9999999920603367]
[1.9999999920603369, 5.293108729098606e-09, -0.9999999947068912]
[1.9999999947068912, 3.528739152732404e-09, -0.9999999964712607]
[1.9999999964712607, 2.3524929411896287e-09, -0.9999999976475071]
[1.9999999976475074, 1.5683284300867701e-09, -0.9999999984316715]
[1.9999999984316714, 1.0455524224184387e-09, -0.9999999989544477]
[1.9999999989544477, 6.970349482789592e-10, -0.9999999993029651]
[1.9999999993029653, 4.6468976814632395e-10, -0.9999999995353103]
[1.9999999995353104, 3.097930430702907e-10, -0.9999999996902069]
[1.999999999690207, 2.0652872005181658e-10, -0.9999999997934713]
[1.9999999997934712, 1.3768582570368912e-10, -0.9999999998623141]
[1.999999999862314, 9.179072317048546e-11, -0.9999999999082093]
[1.9999999999082094, 6.119367975306507e-11, -0.9999999999388063]
[1.9999999999388063, 4.079581117366615e-11, -0.9999999999592042]
[1.9999999999592042, 2.7197207449110767e-11, -0.9999999999728028]
[1.9999999999728029, 1.8131459296929126e-11, -0.9999999999818686]
[1.9999999999818687, 1.2087479165738083e-11, -0.9999999999879124]
[1.9999999999879126, 8.058331779636774e-12, -0.9999999999919418]
[1.9999999999919418, 5.372073156687899e-12, -0.9999999999946279]
[1.9999999999946276, 3.581579477440755e-12, -0.9999999999964184]
[1.9999999999964182, 2.3878676813637867e-12, -0.9999999999976121]
[1.999999999997612, 1.5920598173124745e-12, -0.9999999999984079]
[1.9999999999984077, 1.0615212412782664e-12, -0.9999999999989385]
[1.9999999999989386, 7.075451335936123e-13, -0.9999999999992923]
[1.9999999999992923, 4.716967557290749e-13, -0.9999999999995282]
[1.9999999999995282, 3.1463720517876936e-13, -0.9999999999996855]
[1.9999999999996856, 2.095730996150754e-13, -0.9999999999997904]
[1.9999999999997904, 1.3974007136615304e-13, -0.9999999999998602]
[1.9999999999998603, 9.314771176605063e-14, -0.999999999999907]
[1.999999999999907, 6.195044477408373e-14, -0.9999999999999379]
[1.9999999999999378, 4.1485333686826685e-14, -0.9999999999999586]
[1.9999999999999585, 2.7644553313166398e-14, -0.9999999999999722]
[1.9999999999999722, 1.8577731945394287e-14, -0.9999999999999816]
[1.9999999999999816, 1.2212453270876722e-14, -0.9999999999999877]
[1.9999999999999876, 8.326672684688674e-15, -0.9999999999999918]
[1.9999999999999918, 5.551115123125783e-15, -0.9999999999999946]
[1.9999999999999947, 3.515706244646329e-15, -0.9999999999999964]
[1.9999999999999964, 2.3684757858670005e-15, -0.9999999999999977]
[1.9999999999999976, 1.5913196686293911e-15, -0.9999999999999983]
[1.9999999999999982, 1.2212453270876722e-15, -0.9999999999999989]
[1.999999999999999, 8.141635513917814e-16, -0.9999999999999993]
[1.9999999999999993, 3.7007434154171886e-16, -0.9999999999999996]
[1.9999999999999993, 4.440892098500626e-16, -0.9999999999999996]
[1.9999999999999993, 4.440892098500626e-16, -0.9999999999999996]
```

