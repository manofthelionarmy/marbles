# Summary
---
# Related Stuff:
[[Authentication - Go Web Intermediate Udemy Course]]
#golang
#security
#webapplications 
#nodejs 
#express
#cryptography

---
# Notes:
- AES is an encryption standard rooted in symmetric encryption. 
> Symmetric encryption is when the same key or password is used to encrypt and decrypt the data.
> - Secuirty with Go - Cryptograhpy, Symmetric Encryption
- Moreso about symmetric encryption, it is reversable, while asymmetric encryption is irreversable.
- AES is a `block cipher`.
- Block ciphers are a type of cipher that combines a core <mark style="background: #FFB86CA6;">algorithm</mark> working on <mark style="background: #FFB86CA6;">blocks of data</mark> with a <mark style="background: #FFB86CA6;">mode of operation</mark>, or a technique to process a sequence of blocks.
- A cipher, as defined by the book *Serious Cryptography*, is a encryption algorithm.
- A block cipher consists of an encryption algorithm and a decryption algorithm.
	- The encryption algorithm (E) takes in a plaintext block (P) and a key (K) as input and produces a cipher block as output (C).
		 - C = E(K, P)
	- The decryption algorithm involves the same parts, but takes a cipher block and a key as input and generates a plaintext block as output.
		 - P = D(K, C)
	 - Because these alogrithms are the inverse of each other, they involve the same opeartions. 
  - All of the info above is availabe in the book *Serious Cryptography* under the chapter *The Advanced Encryption Standard*.
 - In the course *Go Intermediate Web Development by Trevor Sawler*, we used AES encryption to encrypt the user's email sent in through the payload, or even high jack the url to reset their password.
 - We learned that a malicious user can sniff the packets, observe the request headers and body, and try to obtain that info. So we can instead use encryption to hide the content.
 - Given AES is based on block ciphers, there are several modes of operation. <mark style="background: #FFB86CA6;">In the course we used CFB mode</mark>, hence the name.
 - To generate the cipher blocks, we need to do some XOR operations. From the book *Serious Cryptography*, this is how its normally done.
 - There is also some wierd value in the code called `iv`, but after further research, the `Security With Go` book clears this up.
 > 	At some point you will see the message being split into two pieces, the IV, and the cipher text. The initialization vector, or IV, is a random value that gets prepended to the actual encrypted message. Everytime a message is encrypted with AES, a random value is generated and used as part of the encryption. The random value is called nonce, which means simply a number that is only used once.
- Hence why we see in the code we are setting the `iv` to some random value via `rand.Reader`. The `iv` acts like a salt hash. 
> The random IV is used in a similar fashion to a salt. It is used primarily so that when the same message is encrypted repeatedly, the cipher text is different each time.
- Putting all of the pieces together, here is the snippet:
```go
func encrypt(key, message []byte) ([]byte, error) {
	block, err := aes.NewCipther(key)
	if err != nil {
		return nil, err
	}
	// create the byte slice that will hold encrypted message
	cipherText := make([]byte, aes.BlockSize + len(message))
	// Generate the Initialization Vector nonce
	// The IV is the same length as the AES blocksize
	iv := cipherText[:aes.BlockSize]
	_, err := io.ReadFull(rand.Reader, iv)
	if err != nil {
		return nil, err
	}

	// Chose the block cipher mode of operation. Using the cipher feedback (CFB) mode here.
	// CBCEncrypter also available
	cfb := cipher.NewCFBEncrypter(block, iv)

	// Generate the encrypted messaged and store it in the remaining bytes after the IV nonce
	cfb.XORKeyStream(cipherText[aes.BlockSize:], message)
	return cipherText, nil
}
```

- Continuing on, here is the decryption snippet:
```go
func decrypt(key, cipherText []byte) ([]byte, error) {
	// initialize block cipher
	block, err := aes.NewCipher(key)
	if err != nil {
		return nil, err
	}

	// Separate the IV nonce from the encrypted message bytes
	iv := cipherText[:aes.BlockSize]
	cipherText = cipherText[aes.BlockSize:]

	// Decrypt the message using the CFB block mode
	// why does this accept the iv as a second arg?
	cfb := cipher.NewCFBDecrypter(block, iv)
	cfb.XORKeyStream(cipherText, cipherText)
	return cipherText, nil
}
```
- The mode of operation for the cipher blocks involve XOR's, fyi.
## Follow up, why does NewCFBDecrypter or NewCFBEncrypter receive the iv as the second argument?