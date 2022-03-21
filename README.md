# ![GA Logo](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Auth Research Lab

---

Authentication is a complex and exciting topic that involves using many of the concepts we've already studied as well as several new ideas. 

An authentication system allows the registration / signup of new users and allows those users to sign in. It has to be able to identify each user and keep their information private and secure.

Being able to develop secure user login systems is in fact a whole career and life path in and of itself, but understanding the broad concepts of **Auth** is critically import for all developers. 

Describing auth flow and understanding key terms are very common **interview questions** for junior developers, so lets take some time to research and understand auth and the related concepts.

## Setup

Fork and clone this repository and answer the questions as you research directly in the README. You do not have to pull request and submit this lab, but you will want to have it on hand for reference in the future. 

## Auth Concepts Worksheet

#### Define the following

1. *Authentication*
    - Authentication is the process of verifying who someone is
    - Checking their credentials matching who they are
2. *Authorization*
    - Authorization is the process of verifying what specific applications, files, and data a user has access to
    - What they are able to do
3. Explain how *authentication* and *authorization* are related but distinct concepts.
    - Authentication is used to verify that users really are who they represent themselves to be. Once this is confirmed, authorization is then used to grant the user permission to access the different levels of information and perform specific functions, depending on the rules established for different types of users. Authentication and Authorization are the first lines of defense to prevent confidential data from falling into the wrong hands. 
    - https://www.sailpoint.com/identity-library/difference-between-authentication-and-authorization/#:~:text=Simply%20put%2C%20authentication%20is%20the,a%20user%20has%20access%20to.
    - https://www.okta.com/identity-101/authentication-vs-authorization/
4. *Sessions vs Token based auth*
    - Session and token based authentication methods are used to make a server trust any request sent by an authenticated user over the internet
    - In Session authentication methods
        - The Server stores the authentication details
        - The user sends a cookie to the server to have their requests authorized
        - The server looks up in its databases to find the right session thanks to the ID the user sends with the cookie in order to authorize users' requests
        - The server admins can perform security operations like logging users out, changing their details, etc. because the session is stored on the server.
    - In Token authentication methods 
        - The User side stores the authentication details
        - The user sends the token itself to the server to have their requests authorized
        - The server decrypts the user's token and verifies the signature in order to authorize the user's requests
        - The server admins can't perform security operations like logging users out, changing their details, etc. because the token is stored on the user's machine
    - https://www.geeksforgeeks.org/session-vs-token-based-authentication/#:~:text=The%20main%20difference%20is%20session,one%20the%20client%20stores%20them.
    - Session is stafeful. Token is stateless
    - Session is server side storing. Token is user side storing
5. *json web token (also know as a jwt)*
    - JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusteed because it is digitally signed.
    - JWT is a standard, meaning that all JWTs are tokens, but not all tokens are JWTs
    - It is a proposed internet standard for creating data with optional signature and/or optional encryption whose payload holds JSON that asserts some number of claims. The tokens are signed either using a private secret or a public/private key
    - The benefit to using JWTs when compared to simple web tokens (SWTs) and Security Assertion Markup Language (SAML) tokens is that...
        - JWTs are more compact: JSON is less verbose than XML, so when it is encoded, a JWT is smaller than a SAML token. THis makes JWT a good choice to be passed in HTML and HTTP environments.
        - JWTS are more secure: JWTs can use a public/proviate key pair in the form of an X.509 certificate for signing. A JWT can also be symmetrically signed by a shared secret using the HMAC algorithm. And while SAML tokens can use public/private key pairs like JWT, signing XML with XML Digital Signature without introducing obscure security holes is very difficult when compared to the simplicity of signing JSON. Read more about JWT signing algorithms.
        - JWTS are more common: JSON parsers are common in most programming languages because they map directly to objects. Conversely, XML doesn't have a natural docuent-to-object mapping. This makes it easier to work with JWT than SAML assertions
        - JWTS are easier to process: JWT is used at internet scale. THis means that it is easier to process on user's devices, especially mobile
    - https://jwt.io/introduction
    - https://auth0.com/docs/secure/tokens/json-web-tokens
    - Standard of how data should be organized. They aren't encrypted. But they are encoded. They do include a hash that indicates the JWTs origin. If your server sees a JWT that is not from that origin, it can be suspicious. JWTs have a return address from the server (kind of how letters have a return address). If it doesn't match up, it would be suspicious
6. *Encoding, encryption and hashing* along with the uses for and differences between the three
    - Encoding: Encoding data is a process involving changing data into a new format using a scheme. Encoding is a reversible process; data can be encoded to a new format and decoded to its original format. Encoding typically involves a publicly available scheme that is easily reversed. Encoding data is typically used to ensure integrity and usability of data and is commonly used when data cannot be transferred in its current format between systems or applications. Encoding is not used to protect or secure data because it is easy to reverse
        - Example: Take a scenario where a user wantst o upload a resume to a job application website and the web server stores
    - Hashing: Hashing involves computing a fixed-length mathematical summary of data, the input data can be any size. In contrast to encoding, hashing cannot be reversed. It is not possible to take a hash and convert it back to the original data, Hashing is commonly used to verify the integrity of data, commonly referred to as a checksum. If two pieces of identical data are hased using the same hash function, the resulting has will be identical. If the two pieces of data are different, The resulting hashes will be different and unique. 
        - As an example: Say Alice wants to send Bob a file and verify that Bob has the exact same file and that no changes occurred in the transferring process. Alice will email Bob the file along with a hash of the file. After Bob downloads the file, he can verify the file is identical by performing a hash function on the file and verify the resulting hash is the same as alice provided.
        - In addition to verifying the integrity of data, hashing is the recommended data transformation technique in authentication processes for computer systems and applications. It is recommended to never store passwords and instead store only the has of the "salted password". A salt is a random string appended to a password that only the authentication process system knows; This guarantees that if two users have the same password the stored hashes are different. 
        - When a user inputs a password to a web application, the password is sent to the web server. The web server then appends the salt to the password and performs a hash function on the password and a salt and compares this output hash with the hash stored in the database for the user. If the hashes match for that user, the user is granted access. Hashing ensures in the event of a breach, or malicious insider the original passwords can never be retrieved. Salting ensures that, if a breach does occur, an attacker cannot determine which users have the same passwords.
    - Encryption: Encryption is the process of securely encoding data in such a way that only authorized users with a key or password can decrypt the data to reveal the original. There are two basic types of encryption; symmetric key and public key. In symmetric key, the same key is used to encrypt and decrypt data, like a password. In public key encryption, one key is used to encrypt data and a different key is used to decrypt the data. 
        - Encryption is used when data needs to be protected so those without the decryption keys cannot access the original data. When data is sent to a webiste over HTTPS it is encrypted using the public key type.
        - While encryption does involve encoding data, the two are not interchangeable terms. Encryption is always used when referring to data that has been securely encoded. Encoding data is only used when talking about data that is not securely encoded.
        - It's like encoding but more secure

    - In Summary:
        - Encoding: Reversible transformation of data format, used to preserve usability of data.
        - Hashing: Is a one-way summary of data, cannot be reversed, used to validate the integrity of data.
        - Encryption: Secure encoding of data used to protect confidentiality of data.
    - https://medium.com/swlh/the-difference-between-encoding-encryption-and-hashing-878c606a7aff#:~:text=%2D%20Encoding%20is%20a%20process%20of,into%20a%20fixed%2Dlength%20string.
    - https://www.packetlabs.net/posts/encryption-encoding-and-hashing/
7. *oAuth* (pronounced oh-Auth)
    - OAuth is an open-standard authorization protocol or framework that describes how unrelated servers and services can safely allow authenticated access to their assets without actually sharing the initial, related, single logon credential. In authentical parlance, this is known as secure, third-party, user-agent, delegated authorization.
        - The simplest example of OAuth is when you go to log onto a website and it offers one or more opportunities to log on using another website's/service's logon. You then click on the button linked to the other website, the other website authenticates you, and the website you were originally connecting to logs you on itself afterward using permission gained from the second webiste.
    - https://www.csoonline.com/article/3216404/what-is-oauth-how-the-open-authorization-framework-works.html
    - OAuth is handing off auth to a trusted - i.e., logging in with google. And then they send over payload of information related to their login. It's convenient. When a site offers you to login to different types of OAuth, they are basically using different passport strategies.

#### Explore and then describe the following npm packages:

1. [bcrypt](https://www.npmjs.com/package/bcrypt)
    - bcrypt is a password-hashing function. Besides incorporating a salt to protect against rainbow table attacks, bcrypt is an adaptive function: over time, the iteration count can be increased to make it slower, so it remains resistant to brute-force search attacks eve with increasing computation power.
    - We use a bcrypt because bcrypt has salt by default. You can't not use salt. Bcrypt is the industry standard for doing hashing. If you're securing user data, you're going to use a package like bcrypt
    - https://codahale.com/how-to-safely-store-a-password/
2. [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)
    - It allows you to store users without storing any information about the users.
    - Allow us to manage jobs in stateless fashion
    - seems to be the most popular?
    - https://www.npmtrends.com/bcrypt-vs-bcryptjs-vs-jsonwebtoken-vs-passport-jwt-vs-passport-vs-json-web-token
    - https://holycoders.com/node-js-passport-jwt-token-api-authentication/
    -
3. [passport](https://www.npmjs.com/package/passport)
    - It's an all in one package for authentication.
    - They offer these things called strategies which are a one way of managing a passport package. you can have more than one strategy on an app.
    - You can have a session based app and token base app all in one app.
    - You can have a fb strategy, google strategy, etc. all in one app
    - Passport's sole purpose is to authenticate requests, which it does through an extensible set of plugins known as strategies. Passport does not mount routes or assume any particular database schema, which maximizes flexibility and allows application-level decisions to be made by the developer. The API is simple: you provide Passport a request to authenticate, and Passport provides hooks for controlling what occurs when authentication succeeds or fails.
    - https://www.passportjs.org/
    * also describe what a *strategy* is in the context of this npm package
        - Strategies are various plugins
        - Strategies are responsible for authenticating requests, which they accomplish by implementing an authentication mechanism. Authentication mechanisms define how to encode a credential, such as a password or an assertion from an identity provider (IdP), in a request. They also specify the procedure necessary to verify that credential. If the credential is successfully verified, the request is authenticated.
        - There are a wide variety of authentication mechanisms, and a corresponding variety of strategies. Strategies are distributed in separate packages which must be installed, configured, and registered.
- https://jonathas.com/token-based-authentication-in-nodejs-with-passport-jwt-and-bcrypt/


---

## Licensing
1. All content is licensed under a CC-BY-NC-SA 4.0 license.
2. All software code is licensed under GNU GPLv3. For commercial use or alternative licensing, please contact legal@ga.co.