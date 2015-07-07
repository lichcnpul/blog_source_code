title: thesis
date: 2015-07-01 21:29:23
categories: Zhang's Thesis
tags: thesis
toc: true
---
# Network-based Fingerprint Authentication System Using a Mobile Device
## Abstract:
Present fingerprint system has problems in security, usability and cost. In this case, we propose a touch-less fingerprint authentication method.  Use mobile device’s built-in camera to capture fingerprint image, and then send it to the server to complete the identity authentication work. Based on this method, the system comprises capture, preprocessing, matching stages and is implemented in a prototype as application for the Android OS. The experimental results show that our method is feasible and lets off some potential problems in the touch-based fingerprint technology.
## Key words:
*Fingerprint authentication*, *touch-less*, *network-based*, *mobile device*
## 1 Introduction
More than a century has passed since the Home Ministry Office, UK, accepted that no two individuals have the same fingerprints and then industriously practiced the idea for solving crimes [1]. Nowadays, due to increasing concerns about security and identity fraud have created a growing need for fingerprint for person recognition, fingerprint authentication is not only needed in forensic applications, but also in a large number of non-forensic applications. The present fingerprint authentication systems are generally called Automatic Fingerprint Identification Systems (AFIS). AFIS accept live-scan digital images acquired with an electronic fingerprint scanner where the finger surface is directly sensed.

However, the seems-good system has the potential problems in security, usability and cost. For example, an e-payment in a convenient store, a usual procedure is (1) put a finger on the scanner for ensuring (2) the POS deals with obtained fingerprint according to the local database (3) if the fingerprint is matched, e-payment is completed. In this process, security problems happens, which fingerprint left on the reader may be duplicated by others and applications may leak fingerprint information. In usability aspect, fingerprint system (FP System) is wired and bulky. The other problem is FP system equipment is expensive and maintenance expense is cost, for instance software updating and hardware upgrading both cost money.

Due to the case above, this paper proposes a network-based finger authentication using a camera. This method is that user uses mobile device’s built-in camera to capture fingerprint (FP) image, and send preprocessed FP image to the server through Internet, then the server send back feedback after matches this FP image with initial fingerprint stored in database. The client reacts according to the feedback.

Allowing for smartphone’s some advantages:  (1) the build-in camera has zooming, auto-focusing and high resolution that is suitable to capture high quality images (2)affordable cost [2] (3)the enough computational capacities to process the photos and execute algorithms, we opted for the smartphone as our experiment tool.  There are no extra devices needed to perform the proposed solution. The capture process is touch-less, so no latent fingerprint is left. In addition, sending FP and receiving feedback is wireless, just through the Internet, hence, it is convenient.  Compared with present AFIS, our method is much safer, stronger usability and less cost.

The rest of the paper is organized as follows. Section 2 will talk about related works in the touch-less finger recognition. Section 3 will discuss the challenges of fingerprint image authentication. Section 4 will talk about procedure and detailed algorithm design. Section 5 will show the basic architecture of the system. Section 6 will show experiment results. Section 7 is discussion. Section 8 is the conclusion.

## 2 Background
### 2.1 Biometrics System Model
Biometric systems generally comprise three basic components [3]:
* An automated mechanism scans and captures a digital or analogue image of a living individual’s characteristics.
* Another mechanism handles compression, processing, storage and comparison of the collected data with the stored data.
* A third component interfaces with the application system to which the user is attempting to gain access.

Obviously, the configuration of such a system may be altered to suit a particular situation. However, the majority of biometric control systems follow this simple model.

It should be noted that there is one crucial step required in setting up a biometric system: enrollment. The only way to gain access to a biometrical controlled system is to enroll.

Enrollment is required to generate a reference template. The methods of enrollment vary according to the device used but usually involve scanning the required biometric data a number of times to gain an accurate measurement. A template is then created and linked to the user’s identity. This template provides the reference for comparison when access attempts are made.

### 2.2 Overview of current AFIS
Generally, a fingerprint system designer make sure that the system makes the correct trade-offs. These trade-offs may include recognition accuracy, response time, system integrity, complexity, cost (component price as well as integration and support costs), privacy, government standards, liveness detection, ease of integration, durability, modality of usage, etc. A good fingerprint recognition system should provide a good balance of security, privacy, convenience, and accountability.

Based on the model above, current AFIS is consists of sensors, fingerprint processing and matching hardware and software. Because of fingerprint recognition’s advantages, AFIS are now being increasingly used in many fields.
![Figure 1](/images/thesis2/image1.png)
Figure 1 shows various applications involving electronic access or transaction that require reliable automatic user recognition.
## 2.3 Fingerprint authentication in Electronic Payment
An application in E-payment using fingerprint authentication is called fingerprint payment system. Fingerprint payment system allows the consumer to pay with the touch of a finger on a fingerprint scanner. Biometric payment providers require completion of a pre-enrollment process in which index fingers are scanned and address and banking information is recorded in an account database [12]. This transactions process reportedly takes a few seconds. The service was launched in United States in 2005 and spread swiftly into worldwide. For example, Walmart, 7-11 and Taobao all support the service.
![Figure 2](/images/thesis2/image2.png)
Figure 2 shows the workflow and its problems.
## 2.4 Disadvantages of touch based sensors
The sensor is the most critical component of the entire fingerprint recognition process. Recognition is highly dependent on the quality of the captured fingerprint image as in less noise, and better image. The core technology used to manufacture the sensors can introduce noise and errors on the captured fingerprint image, influencing the recognition to such a negative extreme that you could be continuously rejected by the system (false rejection) or somebody else could be granted access to the system instead of you (false acceptance).

Current fingerprint capture method is touch-based. In order to acquire fingerprint images, the touch-based fingerprint sensors require the user to place his finger on the flat window of the sensor. Because the skin of the finger is not flat, the user must apply enough pressure on the window to obtain sufficient size and achieve good image quality. However, this pressure produces unavoidable physical distortion in arbitrary directions, which is represented differently throughout every area of the same fingerprint image [4] .During the touch, the fingerprint can be acquired with different technologies. There are two main types of touch-based technologies: optical sensors and IC’s or CMOS sensors. Optical sensors are more accurate than IC’s, but they have the similar problems of above.
![Figure 3](/images/thesis2/image3.png)
Figure 3 shows the images from touch based sensor using different impression strength.

As the sensor’s protecting layer is thin, its continuous usage will destroy its surface, making the device useless. In everyday life, things are even worst. You usually use your hands for different tasks and you usually touch different types of materials. Small portions of the objects you touch accumulate on the skin of your finger. When you touch the fingerprint sensor, you deposit these materials on its surface. Additionally, your skin produces sweat (a combination of water and different types of salts) and the sebum (an oily/waxy substance our body produces). When you touch the surface of a fingerprint sensor, the mix of the sweat, sebum and any substance accumulate during your daily activities become a killer combination for the sensor surface that speeds up the destruction of its surface. Fingerprint sensor manufacturers never achieved great success in this issue.

Meanwhile, after pressing on the surface, a latent fingerprint will be left on it. A latent fingerprint refers to the trail of fingerprint on the surface of the sensor. This can lead to fraudulent use, such as the faking of fingerprints, as well as hygienic problems.
![Figure 4](/images/thesis2/image4.png)
Figure 4 shows the latent fingerprint on a sensor [1].

In addition, a set of fingerprint recognition system equipment is expensive and its maintenance expense is cost, for instance software updating and hardware upgrading both cost money.

As shown above in Figure 2, current fingerprint authentication system based on touched sensors almost have similar problems.

## 3 Related Work
To date, several approaches for touch-less fingerprint recognition system have been reported. Application of fingerprint verification technology to mobile handsets is discussed in [5] and a novel method for fingerprint enhancement has been developed for that particular design[5, 6]. In [11] , the authors proposed a preprocessing technique which included low pass filtering, segmentation and Gabor enhancement for their own-designed touch-less sensor. Later,[7] resolved the 3D to 2D image mapping problem that was introduced in [11] by a strong view difference image rejection method. Preprocessing of fingerprint images captured with mobile camera was suggested by [8]. Most lately, [9] introduced a new touch-less device - The Surround Imager, which can acquire 3D rolled-equivalent fingerprints. To make 3D touch-less fingerprints interoperable with the current AFIS system, [10] proposed an unwrapping algorithm that unwraps the 3D touch-less fingerprint images into 2D representations that are comparable with the legacy rolled fingerprints.

## 4 Proposal Solution
To solve these problems, this paper proposes a network-based finger authentication using mobile device. This method is that user uses mobile device’s built-in camera to capture fingerprint (FP) image, and send preprocessed FP image to the server through Internet, then the server send back feedback after matches this FP image with initial fingerprint stored in database. The client reacts according to the feedback.

The capture process with fingerprint is performed touch-less, just use smartphone camera. Hence, no latent fingerprint is left, privacy leak and hygienic problems won’t be worried any more.

The other advantage of the touch-less method compared to the touch-based ones is that, since the finger does not need to touch any rigid surfaces, the skin does not deform and the image captures very rich details that can make the recognition more accurate.

In addition, network-based system make fingerprint recognition work be done anywhere and anytime. It is much more convenient than the way that you have to go to somewhere and use certain sensor.

At last, current smartphone is good enough to capture the finger in sufficient quality and process the photos and execute algorithms for fingerprint recognition. Apart of this, there are no extra devices. And a smartphone is durable to use, so maintenance charge is small.
In general, out proposal solution will be safer, convenient and cost less.
![Figure 5](/images/thesis2/image5.png)
Figure 5 shows our proposed solution and advantages.

## 5 Method
The proposed method includes Image obtain, Image preprocessing, Image Enhancement, Feature Extraction and Matching Stages.
### 5.1 Image Obtain
This part contains capture process and quality assurance.
**Capture Process**
The intention of the fingerprint recognition is that for authentication the user simply positions his finger close in front of the camera in order to capture a biometric sample. The focus is set to “macro mode”, such that the camera uses the closest possible focus. The LED is switched on during the capture process. The LED spotlights the finger such that it appears brighter than the background. This simplifies the segmentation of the finger against the background. Another advantage is the reduced camera noise and risk of blurring caused from hand-motion due the high brightness from the LED. The LED also stabilizes the lighting conditions and creates more homogeneous illumination.
**Quality Assurance**
The algorithms for finger detection and quality assurance check continuously the preview images of the camera after the capture process has been initiated by the user. The results of the algorithms are calculated in real-time and are displayed on the graphical user interface of the developed prototype. A photo is automatically taken when all criteria (see Section 7) for the fingerprint recognition are fulfilled.

Quality Estimation: Based on the gradient distribution of an ideal fingerprint, calculate to estimate subject image’s coherence and symmetrization.

### 5.2 Image Preprocessing
Skin Color Detection
Ostu Adaptive Thresholding
Morphological Processing
Normalization
### 5.3 Image Enhancement
Median Filtering
Bicubic Interpolation
Histogram Equalization
Gaussian Filtering
Core Point Detection: the Poincare index
Cropping 353*392 size
### 5.4 Feature Extraction
AFIS Open Source Engine
### 5.5 Matching
Using AFIS Open Source Engine to get two compared fingerprints score.

## 6 Results
We chose two group fingerprint sample. Each of them contains 30 finger images and then we compared the two group samples with corresponding database fingerprints. Through analyzing the resulting score matrix, the first group: false reject number is 8, FRR is 0.888%, false accept number is 0, FAR is 0%; the second group:  false reject number is 1, FRR is 0.111%, false accept number is 2, FAR is 0.222%
## 7 Discussion
The experiment  results has been shown that fingerprint recognition on smartphones is possible. A capture process for fingerprint in combination with efficient processing algorithms was developed. The implemented algorithms ensure the suitability of the captured photos for fingerprint recognition.
## Reference
[1] D. Maltoni, D. Maio, A. K.Jain, and S. Prabhakar, Handbook of Fingerprint Recognition, Springer- Verlag, New York, 2003.
[2] B.Y. Hiew, Andrew B.J. Teoh, Member, IEEE and Y.H. Pang, Digital Camera based Fingerprint Recognition, Proceedings of the 2007 IEEE International Conference on Telecommunications and Malaysia International Conference on Communications, 14-17 May 2007, Penang, Malaysia.
[3] Rodger Jamieson, Ph.D., CA, Greg Stephens and Santhosh Kumar, Fingerprint Identification: An Aid to the Authentication Process, 2005 Information Systems Audit and Control Association.
[4] Jainam Shah*, Ujash Poshiya, Touchless Fingerprint Reorganization, Vishwakarma Government Engineering College, Chandkheda Gujarat, India.
[5] M. Hashimoto, S. Tanaka, and J. Thornton, "Biometrics in Mobile Handsets", Technical Report, Mitsubishi Electric Corporation, June 2005.
[6] T. Nakamura, H. Fujiwara, M. Hirooka, and K. Sumi, "Fingerprint Enhancement Using a Parallel Ridge Filter", 17th International Conference on Pattern Recognition 2004, Cambridge, United Kingdom, 2004.
[7] C. Lee, S. Lee, and J. Kim, "A Study of Touchless Fingerprint Recognition System", Joint IAPR International Workshops, SSPR 2006 and SPR 2006, Hong Kong, China, 2006.
[8] C.H. Lee, S.H. Lee, J.H. Kim, and S.J. Kim, "Preprocessing of a Fingerprint Image Captured with a Mobile Camera ", Advances in Biometrics: International Conference, Hong Kong, China, 2006.
[9] G. Parziale and E. Diaz-Santana, "The Surround Imager: A Multi-camera Touchless Device to Acquire 3D Rolled-Equivalent Fingerprints", IAPR International Conference on Biometrics, Hong Kong, China, 2006.
[10] Y. Chen, G. Parziale, E. Diaz-Santana, and A. Jain, "3D Touchless Fingerprints: Compatibility with Legacy Rolled Images", Proceeding of Biometric Symposium, Biometric Consortium Conference, Baltimore,MD, U.S.A, 2006.
[11] Y. Song, C. Lee, and J. Kim, "A New Scheme for Touchless Fingerprint Recognition System", International Symposium on Intelligent Signal Processing and Communication Systems, Korea, 2004
[12] Dileep Kumar, Yeonseung Ryu, A Brief Introduction of Biometrics and Fingerprint Payment Technology , International Journal of Advanced Science and Technology Vol. 4, March, 2009
