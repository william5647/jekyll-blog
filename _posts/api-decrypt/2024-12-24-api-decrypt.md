---
layout: post
title:  "Decrypting and Manipulating Encrypted API Request"
date:   2024-12-24 10:00:00 +0700
categories: jekyll update
usemathjax: true
tag:
  - tips
  - web
  - decryption
image: 
  - /api-decrypt/img1.PNG
image1:
  - /api-decrypt/img2.PNG
image2:
  - /api-decrypt/img4.PNG
image3:
  - /api-decrypt/img3.PNG
image4:
  - /api-decrypt/img5.PNG
image5:
  - /api-decrypt/img6.PNG
image6:
  - /api-decrypt/img7.PNG
image7:
  - /api-decrypt/img8.PNG
image8:
  - /api-decrypt/img9.PNG
---


What if all the requests sent by the application are encrypted during the assessment, making it impossible to modify any requests during transmission? This can hinder the penetration testing process. Let's address this issue.

When an API request or response is encrypted, there will always be a client-side script responsible for the encryption process. Our task is to identify the key used in this process.

In this demo web application, the API request will be encrypted with AES encryption. Let's dive deeper into the client-side script to explore it further.

<figure>
<img src="{{ page.image8 }}" alt="Demo Application">
<figcaption>Demo Application</figcaption>
</figure>

The "generateRandomString()" function will generate random strings from the "characters" constant and the "encryptValue()" function will take three variables, which includes "value", "key", and "iv" to perform encryption process.

<figure>
<img src="{{ page.image }}" alt="JavaScript Function">
<figcaption>JavaScript Function</figcaption>
</figure>

The following snippet shows that "loginData" constant containing "username" and "password" variable will be encrypted with the "encryptValue()" function as the value, and will grab the "key" and "iv" from the randomly generated strings.

<figure>
<img src="{{ page.image1 }}" alt="API Encryption">
<figcaption>API Encryption</figcaption>
</figure>

Here, we can see the end result of the encryption process.

<figure>
<img src="{{ page.image2 }}" alt="Encrypted Request">
<figcaption>Encrypted Request</figcaption>
</figure>

### How do we decrypt and manipulate the API request then?

On the web application, we can send an example request to submit our credential with "foo" username and "foo" password.

<figure>
<img src="{{ page.image3 }}" alt="Example Request">
<figcaption>Example Request</figcaption>
</figure>

Here, we can set a breakpoint in the web browser debugger, enabling us to manipulate the data, even if it is not being entered through user input. We will then change the username from "foo" to "bar" for demonstration purposes.

<figure>
<img src="{{ page.image4 }}" alt="Request Parameter Manipulation">
<figcaption>Request Parameter Manipulation</figcaption>
</figure>

We then can grab the randomly generated IV and Key by setting a breakpoint on the encryption function where it is being called.

IV=rq1vLGpUYj8MUzQo and Key=DZs88qaQ6kzUYbZZ

<figure>
<img src="{{ page.image5 }}" alt="IV and Key">
<figcaption>IV and Key</figcaption>
</figure>

Here is now our newly generated encrypted body request.

<figure>
<img src="{{ page.image6 }}" alt="Encrypted Request">
<figcaption>Encrypted Request</figcaption>
</figure>

As we know the IV and Key from our previous step, we can decrypt the payload with any online [AES decryptor](https://www.devglan.com/online-tools/aes-encryption-decryption).

<figure>
<img src="{{ page.image7 }}" alt="Decrypted Request">
<figcaption>Decrypted Request</figcaption>
</figure>

Now we have successfully learned how to decrypt and manipulate encrypted API request.
