title: 5.1 Algorithm 1
date: 2015-06-25 22:49:44
tags:
categories: Thesis
---
## Display Matrix
Suppose the QR Code image matrix is：

$Q=\begin{bmatrix}
255 & 254 & 255 & 1 & 2 & \cdots\\\
255 & 255 & 255 & 1 & 1 & \cdots\\\
\cdots & \cdots & \cdots & \cdots & \cdots & \cdots
\end{bmatrix}$

Its binary form is：

$Q=\begin{bmatrix}
111111\color{red}{11} & 111111\color{red}{10} & 111111\color{red}{11} & 000000\color{red}{01} & 000000\color{red}{10} & \cdots\\\
111111\color{red}{11} & 111111\color{red}{11} & 111111\color{red}{11} & 000000\color{red}{01} & 000000\color{red}{01} & \cdots\\\
\cdots & \cdots & \cdots & \cdots & \cdots & \cdots
\end{bmatrix}$

The watermark image matrix is:

$M=\begin{bmatrix}
167 & 63 & 15 & \cdots\\\
255 & 127 & 128 & \cdots\\\
\cdots & \cdots & \cdots & \cdots
\end{bmatrix}$

Its binary form is:

$M=\begin{bmatrix}
10100111 & 00111111 & 00001111 & \cdots\\\
11111111 & 01111111 & 10000000 & \cdots\\\
\cdots & \cdots & \cdots & \cdots
\end{bmatrix}$

Now we will separate the watermark matrix to encode it to the QRcode matrix.
Let's focus the watermark matrix first.
## Watermark Matrix
For the watermark matrix above, we called it M, we can see M(1,1)=167, in binary form, M(1,1)=10100111. We separate it to 4 parts.

<strong><font color="red" size="6">10</font></strong><strong><font color="green" size="6">10</font></strong><strong><font color="blue" size="6">01</font></strong><strong><font color="yellow" size="6">11</font></strong>

1. The Red Part: the 1-2 bit
2. The Green Part: the 3-4 bit
3. The Blue Part: the 5-6 bit
4. The Yellow Part: the 7-8 bit

Then we can get 4 matrix from 4 parts:
1.The Red Part Matrix is:

$M1=\begin{bmatrix}
10 & 00 & 00 & \cdots\\\
11 & 01 & 10 & \cdots\\\
\cdots & \cdots & \cdots & \cdots
\end{bmatrix}=\begin{bmatrix}
2 & 0 & 0 & \cdots\\\
3 & 1 & 2 & \cdots\\\
\cdots & \cdots & \cdots & \cdots
\end{bmatrix}$

2.The Green Part Matrix is:

$M2=\begin{bmatrix}
10 & 11 & 00 & \cdots\\\
11 & 11 & 00 & \cdots\\\
\cdots & \cdots & \cdots & \cdots
\end{bmatrix}=\begin{bmatrix}
2 & 3 & 0 & \cdots\\\
3 & 3 & 0 & \cdots\\\
\cdots & \cdots & \cdots & \cdots
\end{bmatrix}$

3.The Blue Part Matrix is:

$M3=\begin{bmatrix}
01 & 11 & 11 & \cdots\\\
11 & 01 & 00 & \cdots\\\
\cdots & \cdots & \cdots & \cdots
\end{bmatrix}=\begin{bmatrix}
1 & 3 & 3 & \cdots\\\
3 & 1 & 0 & \cdots\\\
\cdots & \cdots & \cdots & \cdots
\end{bmatrix}$

4.The Yellow Part Matrix is:

$M4=\begin{bmatrix}
11 & 11 & 11 & \cdots\\\
11 & 11 & 00 & \cdots\\\
\cdots & \cdots & \cdots & \cdots
\end{bmatrix}=\begin{bmatrix}
3 & 3 & 3 & \cdots\\\
3 & 3 & 0 & \cdots\\\
\cdots & \cdots & \cdots & \cdots
\end{bmatrix}$

## Encoding Method
### Why we can encode QRCode Image with watermark image?
The QRCode Image is bigger than watermark image. The rows of QRCode image is 3 times higher than watermark image; the colmns is 5 times higher than watermark image. So we can embed the watermark matrix into qrcode matrix. It is very important. In our method, the watermark matrix M is a 392\*357 matrix; the qrcode matrix Q is a 900\*5000 matrix.

In addition, the QRCode image and watermark image are both grayscale images.
### How to encode?
We use Least Significant Bit Algorithm. First, we separate matrix Q to 5 parts.

$Q=\begin{bmatrix}
A&B& \\\
C&D& \\\
 & &E
\end{bmatrix}$

For matrix A,B,C,D, they are all 392\*357 matrix. E is the rest part of Q.
Then we use A,B,C,D and M1,M2,M3,M4 to encode. We set the least 2 bits of A,B,C,D to 0. For example:

$A=\begin{bmatrix}
111111\color{red}{11} & 111111\color{red}{10} & 111111\color{red}{11} & 000000\color{red}{01} & 000000\color{red}{10} & \cdots\\\
111111\color{red}{11} & 111111\color{red}{11} & 111111\color{red}{11} & 000000\color{red}{01} & 000000\color{red}{01} & \cdots\\\
\cdots & \cdots & \cdots & \cdots & \cdots & \cdots
\end{bmatrix}$

set the least 2 bits to 0:

$A1=\begin{bmatrix}
111111\color{red}{00} & 111111\color{red}{00} & 111111\color{red}{00} & 000000\color{red}{00} & 000000\color{red}{00} & \cdots\\\
111111\color{red}{00} & 111111\color{red}{00} & 111111\color{red}{00} & 000000\color{red}{00} & 000000\color{red}{00} & \cdots\\\
\cdots & \cdots & \cdots & \cdots & \cdots & \cdots
\end{bmatrix}$

then we use matrix M1 instead of the least 2 bits of A:
```python
A2 = A1 + M1
```
For B,C,D and M2,M3,M4 ,we do the some operation:
```python
B2 = B1 + M2
C2 = C1 + M3
D2 = D1 + M4
```
After that, we will get a new matrix called Q2:

$Q2=\begin{bmatrix}
A2&B2& \\\
C2&D2& \\\
 & &E
\end{bmatrix}$

The matrix Q2 contains all the information of watermark images. Now we have realized Encoding Module.

## Decoding Method
It is easy to get the watermark matrix. From Q2 we can extract A2,B2,C2,D2, then we will get M1,M2,M3,M4 by mod([A2,B2,C2,D2],4).
```python
M1(i,j) = A2(i,j) mod 4
M2(i,j) = B2(i,j) mod 4
M3(i,j) = C2(i,j) mod 4
M4(i,j) = D2(i,j) mod 4
```
From M1, M2, M3, M4, we will recover watermark matrix easily.
```python
M(i,j)=M4(i,j)＋4 * M3(i,j)＋16 * M2(i,j)＋64 * M1(i,j)
```
In this way, now we have already recover the watermark matrix.
