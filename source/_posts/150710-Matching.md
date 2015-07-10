title: 6 Matching
date: 2015-07-10 06:22:41
tags:
categories: Thesis
---
# 6 Matching
## 6.1 Basic Concept
After the server receives the picture send from client, it will decode it and get the real fingerprint picture. Now the fingerprint picture is send to matching module. It will be matched with fingerprints stored in the database. Basically, the matching module will extract fingerprint features from fingerprint picture. Traditionally, two fingerprints have been compared using discrete features called minutiae. These features include points in a finger's friction skin where ridges end (called a ridge ending) or split (called a ridge bifurcation). The figure shows an example of the two types of minutiae.
![minutiae](/images/thesis/chapter6/1.png)
The matching engine will compare two fingerprints by minutiae. After that, it will give a matching score. If the fingerprint is matching, the match score will be high. Otherwise, the score will be zero.
## 6.2 SourceAFIS
There are some open-source fingerprint matching software on the internet. We tried NBIS software and SourceAFIS software. We also used a commercial software called UrU SDK to do the experiment. Finally, we choose SourceAFIS as our matching engine. The matching algorithm is like this:
``` csharp
static AfisEngine Afis = new AfisEngine();
Fingerprint fp1 = new Fingerprint();
Person person1 = new Person();
person1.Fingerprints.Add(fp1);
// person2 do the same operation as person1
Afis.Extract(person1);
Afis.Extract(person2);
score = Afis.Verify(person1, person2);
```
1. Step1: Define a match engine Afis.
2. Step2: Define 2 Fingerprint Objects from fingerprint pictures.
3. Step3: Define 2 Person Objects and add the Fingerprint Objects to Person.
4. Step4: Use the method Extract of match engine to extract features.
5. Step5: Use the method Verify of match engine to get the match score.
6. Step6: The client determines whether the authentication is passed by the score.
