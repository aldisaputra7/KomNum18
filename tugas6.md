# Persmaan Differensial Biasa

## Metode Euler

Dalam matematika dan ilmu komputasi, Metode Euler juga disebut metode forward euler adalah prosedur numerik orde pertama untuk menyelesaikan persamaan differensial biasa dengan nilai awal yang diberikan. 

Metode Euler adalah salah satu dari metode satu langkah yang paling sederhana. Di banding dengan beberapa metode lainnya, metode ini paling kurang teliti. Namun demikian metode ini perlu dipelajari mengingat kesederhanaannya dan mudah pemahamannya sehingga memudahkan dalam memperlajari metode lain yang lebih teliti.

Metode Euler merupakan metode paling sederhana yang diturunkan dari deret Taylor. Penyelesaian initial value problems menggunakan metode Euler dilakukan melalui persamaan 
$$
y_{i+1}=y_{i}+f(x_{i},y_{i})h
$$
dimana *$i$* merupakan tahap iterasi

## Algoritma Metode Euler

1. Tentukan titik awal integrasi *$x_{0}$* dan *$y_{0}$*.
2. Tentukan jumlah iterasi *$n$* dan step size *$h$* yang digunakan.
3. Lakukan integrasi menggunakan persamaan diatas.

## Tugas Pemrograman

Buatlah program untuk menyelesaikan persamaan differensial biasa berikut dengan metode Euler
$$
\frac{dy}{dx} = 1+x^{2}, y(1)=-4
$$
Untuk menentukan *$y(1.01), y(1.02), y(1.03)$*

### Listing Program

```python
print("f(x,y)=1+x^2")
print("yi+1 = y1 + hf(xi+yi)")
x1 = float(input("Masukkan x1= "))
x2 = float(input("Masukkan x2= "))

h = 1.01-x1 #Langsung diatur sendiri karena yang dicari f(x,y) nilai x-nya=1.01
n=4 #jumlah x ada 4 yaitu 1, 1.01, 1.02, 1.03
xi = -4
hasil = xi
y=0
for i in range(n):
    print("hasil dari y"+str(i)+"= "+ str(hasil))
    hasil = xi + h*(1+(x1+y)**2)
    y+=h
    xi=hasil

```

dari listing program diatas terdapat variabel *$x_{1}$* adalah *$x$* awal dan *$x_{2}$* adalah *$x$* akhir. 

*$x_{i}$* adalah hasil awal yang kemudian akan dimassukkan pada proses iterasi. Karena rumus eurel adalah *$y_{1}= y_{0}+h(f(x,y))$* maka rumus barunya adalah *$y_{1}=y_{0}+h(1+x^{2})$*. Variabel y digunakan untuk penambahan nilai *$x$* agar selalu bertambah *$0.01$*