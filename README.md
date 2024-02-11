# AES-128-OneKey-CBC

AES-128-OneKey-CBC is a simplified cryptographic mode based on AES-128, offering straightforward encryption and decryption processes using a single key. The mode utilizes Cipher Block Chaining (CBC) without the need for a separate Initialization Vector (IV) key. This design is especially suitable for scenarios where simplicity is crucial, and a distinct IV key is impractical.

## Features
- **AES-128 Encryption:** Leverages the AES-128 algorithm for robust cryptographic operations.
- **OneKey Operation:** Uses a single key for both encryption and decryption, reducing complexity.
- **Integrated CBC Mode:** Implements CBC mode seamlessly without requiring a separate IV key.
- **No Padding Support:** Assumes that input blocks are precisely 16 bytes each.
- **Key Length:** The key length must be 16 bytes for AES-128.

## Functions
### 1. AES_EncryptInit
```c
void AES_EncryptInit(AES_CTX *ctx, const uint8_t *key);
```
- **Description:** Initializes the AES context with the provided 16-byte key for encryption.
- **Parameters:**
  - `ctx`: Pointer to the AES context structure.
  - `key`: Pointer to the 16-byte AES encryption key.
- **Example Usage:**
  ```c
  AES_CTX ctx;
  uint8_t key[AES_KEY_SIZE];
  
  // Set the AES key
  memcpy(key, "This is aes key!", AES_KEY_SIZE);
  
  // Initialize the AES context for encryption
  AES_EncryptInit(&ctx, key);
  ```

### 2. AES_Encrypt
```c
void AES_Encrypt(AES_CTX *ctx, const uint8_t *input, uint32_t length, uint8_t *output);
```
- **Description:** Encrypts the input data using the initialized AES context.
- **Parameters:**
  - `ctx`: Pointer to the initialized AES context structure.
  - `input`: Pointer to the input data to be encrypted.
  - `length`: Length of the input data.
  - `output`: Pointer to the buffer where the encrypted output will be stored.

### 3. AES_DecryptInit
```c
void AES_DecryptInit(AES_CTX *ctx, const uint8_t *key);
```
- **Description:** Initializes the AES context with the provided 16-byte key for decryption.
- **Parameters:**
  - `ctx`: Pointer to the AES context structure.
  - `key`: Pointer to the 16-byte AES decryption key.
- **Example Usage:**
  ```c
  AES_CTX ctx;
  uint8_t key[AES_KEY_SIZE];
  
  // Set the AES key
  memcpy(key, "This is aes key!", AES_KEY_SIZE);
  
  // Initialize the AES context for decryption
  AES_DecryptInit(&ctx, key);
  ```

### 4. AES_Decrypt
```c
void AES_Decrypt(AES_CTX *ctx, const uint8_t *input, uint32_t length, uint8_t *output);
```
- **Description:** Decrypts the input data using the initialized AES context.
- **Parameters:**
  - `ctx`: Pointer to the initialized AES context structure.
  - `input`: Pointer to the input data to be decrypted.
  - `length`: Length of the input data.
  - `output`: Pointer to the buffer where the decrypted output will be stored.

## Usage
1. **Key Initialization:**
   - Initialize the AES context with the 16-byte key using `AES_CTX ctx;`.

2. **Encryption:**
   - Encrypt plaintext with `AES_Encrypt` for consistent 16-byte blocks.

3. **Decryption:**
   - Decrypt ciphertext using the same 16-byte key and `AES_Decrypt`.

## Example
```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <stdint.h>
#include <string.h>
#include "AES.h"

// Output function to print data in hex format
void output(const char* title, uint8_t *data, uint32_t size) {
	printf("%s", title);
	for (uint8_t index = 0; index < size; index++) {
		printf("%02x", data[index]);
	}
	printf("\n");
}

int main() {
	// Initialize the AES key and data
	uint8_t key[AES_KEY_SIZE];
	uint8_t data[32];
	
	// Set the AES key
	memcpy(key, "This is aes key!", AES_KEY_SIZE);
	// Set the plaintext data
	memset(data, 0x79, 32);
    
	// Print the original data
	output("original: 0x", data, 32);
    
	// Initialize AES context for encryption
	AES_CTX ctx;
	AES_EncryptInit(&ctx, key);
	// Encrypt the data
	AES_Encrypt(&ctx, data, 32, data);
	
	// Print the encrypted data
	output("encrypted: 0x", data, 32);
	
	// Initialize AES context for decryption
	AES_DecryptInit(&ctx, key);
	// Decrypt the data
	AES_Decrypt(&ctx, data, 32, data);
	
	// Print the decrypted data
	output("decrypted: 0x", data, 32);
	return 0;
}
```

## Example Code Explanation
- The provided example code demonstrates the encryption and decryption process.
- The initialization of the AES context and 16-byte key is crucial for proper operation.

## Note
This mode does not support padding, so ensure that input blocks are precisely 16 bytes each. It offers a straightforward approach to AES-128 encryption and decryption with the added simplicity of a one-key CBC mode. Adapt it to your cryptographic applications for efficient and secure operations.

## Contributions
Contributions are welcome! If you have improvements, bug fixes, or additional features, feel free to submit a pull request.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
