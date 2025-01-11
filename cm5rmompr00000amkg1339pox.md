---
title: "How SSL Certificates Work: Securing the Internet One Connection at a Time"
seoTitle: "Understanding SSL: Securing Internet Connections"
seoDescription: "SSL certificates secure browsing via data encryption and website verification, involving components and the SSL handshake process"
datePublished: Sat Jan 11 2025 03:30:09 GMT+0000 (Coordinated Universal Time)
cuid: cm5rmompr00000amkg1339pox
slug: how-ssl-certificates-work-securing-the-internet-one-connection-at-a-time
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1736215741832/add3dacb-87d6-4927-b640-bf6dd9ecc93d.png
tags: ssl, cloud, devops, ssl-certificate, sre, devsecops, platform-engineering

---

## What is an SSL certificate?

An **SSL certificate** is a digital file issued by a trusted third party known as a **Certificate Authority (CA)**. It has two main purposes:

1. **Encryption**: It encrypts data between the client (your browser) and the server, ensuring confidentiality.
    
2. **Authentication**: It verifies the legitimacy of the website, confirming it belongs to the intended domain owner.
    

## Components of an SSL Certificate

An SSL certificate includes the following information:

* The website’s **domain name**.
    
* The certificate holder’s **identity** (organization or individual).
    
* The **Certificate Authority (CA)** that issued the certificate.
    
* The certificate’s **validity period**.
    
* The **public key** (used in encryption).
    
* The **digital signature** of the CA.
    

## How SSL Certificates Work: Step-by-Step

### 1\. Establishing a Connection: The SSL Handshake

When you visit a website with SSL, your browser and the server go through a process called the **SSL Handshake** to create a secure connection.

#### **Step 1: Client Hello**

* Your browser sends a **Hello** message to the server.
    
* This message includes:
    
    * Supported encryption protocols (e.g., TLS 1.3, TLS 1.2).
        
    * A randomly generated number (used for encryption later).
        

#### **Step 2: Server Hello**

* The server replies with its **Hello** message, which includes:
    
    * The chosen encryption protocol.
        
    * Its SSL certificate, containing the **public key**.
        
    * Another random number.
        

#### **Step 3: Certificate Validation**

* The browser checks the server’s SSL certificate by verifying:
    
    * The CA’s signature (to confirm the certificate is from a trusted authority).
        
    * The domain name matches the one on the certificate.
        
    * The certificate is still valid.
        
* If any of these checks fail, the browser shows a warning.
    

#### **Step 4: Key Exchange**

* The browser creates a **pre-master secret**, a temporary key used to make the session key.
    
* It encrypts this pre-master secret with the server’s **public key** and sends it to the server.
    
* The server decrypts it using its **private key**.
    

#### **Step 5: Session Key Derivation**

* Both the client and server use the pre-master secret, along with the random numbers exchanged earlier, to create a **session key**.
    
* This session key is used for **symmetric encryption**, which is faster than public-key encryption.
    

#### **Step 6: Secure Communication**

* All further communication between the browser and the server is encrypted using the session key.
    
* This ensures data confidentiality, integrity, and security.
    

[![Diagram illustrating the SSL/TLS handshake process in six steps: 1) Client initiates communication. 2) Server sends an encrypted public key. 3) Client verifies the certificate and sends an encrypted key. 4) Server receives and decrypts it. 5) Server sends encrypted content. 6) Client decrypts the content to complete the handshake.](https://cdn.hashnode.com/res/hashnode/image/upload/v1735783894306/504e95c3-4dfd-4c02-b64f-f4745b52aab3.png align="center")](https://www.entrust.com/sites/default/files/inline-images/how-does-ssl-work-1258x489.png)

### 2\. The Role of Encryption in SSL

Encryption is the backbone of SSL. It ensures that even if someone intercepts the data, they cannot read or change it. SSL uses two types of encryption:

#### **Asymmetric Encryption**

* Involves a **public key** (shared with everyone) and a **private key** (kept secret by the server).
    
* Used during the SSL handshake to securely exchange the session key.
    

#### **Symmetric Encryption**

* Uses the **session key** to encrypt and decrypt data during the session.
    
* Faster and more efficient, making it ideal for ongoing communication.
    

## How to Check if a Website Uses SSL

1. Look for a **padlock icon** in the browser’s address bar.
    
2. Ensure the URL starts with **https://** instead of **http://**.
    
3. Click the padlock to view certificate details, such as the issuer and expiration date.
    

## References

1. How Does an SSL Certificate Work? - HTTPS Explained by Piyush Garg  
    [https://www.youtube.com/watch?v=0yw-z6f7Mb4](https://www.youtube.com/watch?v=0yw-z6f7Mb4)
    
2. How does SSL work? | SSL certificates and TLS  
    [https://www.cloudflare.com/learning/ssl/how-does-ssl-work/](https://www.cloudflare.com/learning/ssl/how-does-ssl-work/)