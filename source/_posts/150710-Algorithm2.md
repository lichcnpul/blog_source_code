title: 5.2 Algorithm 2
date: 2015-07-10 05:28:55
tags:
categories: Thesis
---

## 5.2 Image Encryption Algorithm
As we talked in chapter 3, we will use a key to encrypt the picture we made in 5.1. Then we can use the same key to decrypt.
### 5.2.1 Principle
1. First client uses user's password to generate a barcode picture and takes this picture as a key.
2. Second the client uses this key to encrypt the real picture we want to transfer.
3. Then the server requires user's password from database, and uses it to generate the same key.
4. The server decrypts the picture send from client and gets the real picture.
5. Get the barcode picture and fingerprint picture from the real picture.

### 5.2.2 Encryption and Decryption
The key point is how to encrypt picture using another picture(key). Here we use a very simple algorithm called XOR.
Now suppose matrix A and B:

$A=\begin{bmatrix}
128 & 127 & 64\\\
10 & 20 & 30\\\
20 & 0 & 255
\end{bmatrix}$

$B=\begin{bmatrix}
128 & 128 & 1\\\
1 & 1 & 2\\\
255 & 255 & 1
\end{bmatrix}$

The binary form is:

$A=\begin{bmatrix}
10000000 & 01111111 & 01000000\\\
00001010 & 00010100 & 00011110\\\
00010100 & 00000000 & 11111111
\end{bmatrix}$

$B=\begin{bmatrix}
10000000 & 10000000 & 00000001\\\
00000001 & 00000001 & 00000010\\\
11111111 & 11111111 & 00000001
\end{bmatrix}$

#### 5.2.2.1 Encryption
We take matrix B as key, A as original picture. Then we let matrix C = A XOR B.

$C = A \oplus B = \begin{bmatrix}
00000000 & 11111111 & 01000001\\\
00001011 & 00010101 & 00011100\\\
11101011 & 11111111 & 11111110
\end{bmatrix} = \begin{bmatrix}
0 & 255 & 65\\\
11 & 21 & 28\\\
235 & 255 & 254
\end{bmatrix}$

We get a picture C by A XOR B, we will send this picture to the server. The attackers can intercept picture C. Howerver, he cannot recover picture A until he steals user's password and generates it to a barcode.
#### 5.2.2.2 Decryption
The server requires the user's password from database. Then the server will get the key from password. Now server take the picture C send from client and key B to decrypt. We let D = C XOR B.

$D = C \oplus B = \begin{bmatrix}
10000000 & 01111111 & 01000000\\\
00001010 & 00010100 & 00011110\\\
00010100 & 00000000 & 11111111
\end{bmatrix} = \begin{bmatrix}
128 & 127 & 64\\\
10 & 20 & 30\\\
20 & 0 & 255
\end{bmatrix} = A$

Now the server recovers picture A by C XOR B. After that, the sever side can extract fingerprint image from picture A.
