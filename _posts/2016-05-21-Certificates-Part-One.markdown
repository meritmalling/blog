---
layout: post
title:  Server & Mutual Handshakes
date:   2016-05-21
---

###Identification

A very powerful tool, digital certificates can be used to verify the sender of information, the server you are connecting to, or even the users that are connecting to your server.

To identify the holder of a certificate, each certificate contains certain information. This includes information about the organization to which the certificate was issued, information about the issuing authority, an expiration date, a serial number, the certificate holder’s public key.

###Certificate Authorities

Like any identifying document certificates are issued by a trusted agency, these are called Certificate Authorities. Certificate Authorities both certify individual identities and issue certificates that allow other entities to verify they are indeed who they claim to be.

Certificate authorities can be anyone. Any organization that needs to identify callers can create it's own authority to verify those callers. There are also third party vendors that are in the business of issuing certificates (Digicert, Entrust, etc.)

###Encryption:

There are two types of encryption: symmetric and asymmetric.

In symmetric encryption there is a single shared private key - that is both parties (sending and receiving) have the same key. This key will do the work both of encrypting a decrypting the exchanged information.

In asymmetric encryption there are two keys: a public key and a private key. The public key is, just as described: public. It is used for encryption only and can not be used to decrypt information encrypted with it. Nor can the private key be computed from the public key.


###Server Authentication:

1. The Client sends a *Hello* message.
2. The Server responds with a *Hello* message, follows up with a *Server Certificate* message, and ends with a *Server Hello Done* message.
3. The client generates a one time *Session Key*, encrypts it with the server's public key and sends it to the server.
4. Once the server has received that session key both the client and the server independently use that key to compute a common session key. (In this step both computers are independently generating the same information.)
5. Once both computers have computed the session key to be used to communication they send a *Finished* message to each other. If both computers can read this message the session key was computed correctly and an encrypted connection is established.

###Client Authentication:

1. The Client sends a *Hello* message.
2. The Server responds with a *Hello* message, follows up with a *Server Certificate* message and a *Certificate Request* message and then ends with a *Server Hello Done* message.
3. The client sends a *Client Certificate* message.
3. The client generates a one time *Session Key*, encrypts it with the server's public key and sends it to the server, following it with a *Certificate Verify* message.
4. Once the server has received that session key both the client and the server independently use that key to compute a common session key. (In this step both computers are independently generating the same information.)
5. Once both computers have computed the session key to be used to communication they send a *Finished* message to each other. If both computers can read this message the session key was computed correctly and an encrypted connection is established.
