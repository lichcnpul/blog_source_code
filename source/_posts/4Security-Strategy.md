title: 4. Security Strategy
date: 2015-06-24 18:19:43
categories: Thesis
tags: thesis
toc: true
---
# Chapter 4 Security Strategy
This chapter discuss the security strategy in the fingerprint authentication system. First, we will talk about security threat briefly; Second, we discuss the traditional approach to enhance security; Third, we give a fingerprint watermark approach to solve the security problems. We will discuss reversible watermarking technology in this part.
## 4.1 Security Threat and Common Approach
### 4.1.1 Security Threat
As we have talked in chapter 1, there are some types of internet attack. One is to **intercept information**. The purpose of intercepting information is to steal data content itself. Another one is to **replay attack**. Replay attack is a form of network attack in which a valid data transmission is maliciously or fraudulently repeated or delayed. In our system, attackers will try to intercept user’s packages which contain fingerprint images. This is a kind of intercept attack. In this case, user information will be leaked. In addition, the attackers intercept data packages then they can resend these data packages to the server regardless of whether the data is encrypted. This is a kind of replay attack. Attackers use replay attack to realize the purpose of spoofing server. Then the server will consider the attacker to be the original user.

The fingerprint authentication system should be security. We try to design some security subsystem to enhance the system security. Then the system should be prevent information interception and replay attack.
### 4.1.2 Common Approach
File encryption and digital signature is a common approach to enhance system security.
* File encryption : Prevent information leaks.
* Digital signature : Ensure the message sent by the original sender.

File encryption： The basic process flow of file encryption is to encode the original file by an algorithm, making it unreadable(commonly referred to as “ciphertext”). The original file cannot be displayed without **key**. By this way we can prevent data from being illegally stolen. The reverse process is called decryption. such as: [Algorithm 1](http://blog.csdn.net/stpeace/article/details/8315772) and [Algorithm 2](http://wenku.baidu.com/link?url=Szecji7gvHr35DDq2ltqNqa4aYdajxnfNinz8WA3_4WWVXKHgj6IFUvjTgY_V-w9eqcz4YppASDBfejSm0cIMGMZA62YlXNME9e2ZfxwVoK)

Digital signature: A digital signature is a mathematical technique used to validate the authenticity and integrity of a message, software or digital document. see [searchsecurity](http://searchsecurity.techtarget.com/definition/digital-signature). The basic flow of digital signature is like this:
![figure 1](/images/thesis/1.png)
From this diagram, we can know how digital-signature works. First, the data sender uses his private key to encode the information he prepared to send, then he gets a signed message. Second, he send the signed message to the receiver. The receiver gets the signed message and decodes the message by the sender’s public key. Then the receiver gets the decrypted hash. If the decrypted hash matches a second computed hash of the same data, it proves that the data hasn’t changed since it was signed. Otherwise, it proves that the data has been changed by attackers since it was signed.
### 4.1.3 New Approach
The traditional approach is good enough to enhance system security and prevent internet attack. However, there are still some disadvantages to apply it to our fingerprint system.
1. **Complex**. Digital-signature need to be controlled in a complex architecture. Besides, we need to build two separate subsystems, one is for file encryption, the other one is for digital signature. It will be more complex.
2. **Common Approach**. It is a common approach to enhance system security. It does not take into account the characteristics of the fingerprint image.

In order to overcome the two drawbacks, we try to propose a new approach. The new approach is a kind of reversible digital watermark technology and it combine file encryption with authentication. We will discuss the detail in 4.3 Solution and 4.4 Algorithm.

## 4.2 Architecture

Waiting to write ...

## 4.3 Solution

Waiting to write ...

## 4.4 Algorithm

Waiting to write ...

### Step1: Read and display
Display the QrCode image and fingerprint image. use fingerprint image as watermark.
```matlab
clear;
clc;

%= Read the QRCode and FP watermarkImage
qrImage = imread('qrImage.png');
fpImage = imread('watermarkImage.bmp');
watermarkImage = double(fpImage);

figure;
imshow(qrImage);
title('the qrCode Image!');

figure;
imshow(uint8(watermarkImage));
title('the image with water marks!');
```
Then the QR Code Image and fingerprint image are displayed.
![figure 2](/images/thesis/2.jpg)
![figure 3](/images/thesis/3.jpg)
### Step2: Encoding
Use the algorithm below to encode the QRcode with fingerprint image.
```matlab
[m,n] = size(watermarkImage);
newwatermark=zeros(m,n);
newwatermark2 = zeros(m,n);
multiwatermarkImage = zeros(2*m,2*n);
orimod = zeros(2*m,2*n);

qrImage1 = qrImage;
qrImage2 = qrImage;

for i=1:m
  for j=1:n
    orimod(i,j)=mod(qrImage(i,j,1),4);
    orimod(i+m,j) = mod(qrImage(i+m,j,1),4);
    orimod(i,j+n) = mod(qrImage(i,j+n,1),4);
    orimod(i+m,j+n) = mod(qrImage(i+m,j+n,1),4);

    qrImage1(i,j,1) = qrImage(i,j,1)-orimod(i,j);
    qrImage1(i+m,j,1) = qrImage(i+m,j,1)-orimod(i+m,j);
    qrImage1(i,j+n,1) = qrImage(i,j+n,1)-orimod(i,j+n);
    qrImage1(i+m,j+n,1) = qrImage(i+m,j+n,1)-orimod(i+m,j+n);

    k1 = fix(watermarkImage(i,j));
    k2 = fix(k1/4);
    k3 = fix(k2/4);
    k4 = fix(k3/4);

    multiwatermarkImage(i,j) = mod(k1,4);
    multiwatermarkImage(i+m,j) = mod(k2,4);
    multiwatermarkImage(i,j+n) = mod(k3,4);
    multiwatermarkImage(i+m,j+n) = mod(k4,4);

    qrImage2(i,j,1) = qrImage1(i,j,1) + multiwatermarkImage(i,j);
    qrImage2(i+m,j,1) = qrImage1(i+m,j,1) + multiwatermarkImage(i+m,j);
    qrImage2(i,j+n,1) = qrImage1(i,j+n,1) + multiwatermarkImage(i,j+n);
    qrImage2(i+m,j+n,1) = qrImage1(i+m,j+n,1) + multiwatermarkImage(i+m,j+n);
  end
end

QrImagewithwatermarkImage=qrImage2;
figure;
imshow(QrImagewithwatermarkImage);
title('the image with water marks!');
```
Now we can see the QRcode image with watermark.
![figure 4](/images/thesis/4.jpg)
### Step3: Decoding
Use the same algorithm to decode the image with watermark. Then get the reversed fingerprint image.
```matlab
for i=1:m
  for j=1:n
    x1 = mod(QrImagewithwatermarkImage(i,j,1),4);
    x2 = mod(QrImagewithwatermarkImage(i+m,j,1),4);
    x3 = mod(QrImagewithwatermarkImage(i,j+n,1),4);
    x4 = mod(QrImagewithwatermarkImage(i+m,j+n,1),4);

    newwatermark(i,j) = x1 + x2*4 + x3*16 + x4*64;
  end
end
newwatermark2 = uint8(newwatermark);
figure;
imshow(newwatermark2);
title('the watermark!');
```
![figure 5](/images/thesis/5.jpg)
