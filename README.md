# Encryption Program

## Overview
This project is an encryption and decryption program developed as part of the **INFR2141 Final Project**. It allows users to securely encrypt and decrypt text using cryptographic techniques implemented in Python.

## Features
- **Encryption**: Securely encrypts input text using a cryptographic algorithm.
- **Decryption**: Allows decryption of previously encrypted text.
- **User Interface**: Command-line based input/output.
- **File Handling**: Reads from and writes encrypted/decrypted data to files.

## Dependencies
This program requires Python 3.x and the following libraries:
```bash
pip install cryptography
```

## How It Works
The encryption program follows these main steps:
1. **Generate a Key**: The program generates a cryptographic key if one does not exist.
2. **Encrypt Data**: Uses the generated key to encrypt input text and outputs the ciphertext.
3. **Decrypt Data**: Uses the same key to decrypt the ciphertext back to the original message.
4. **File Handling**: Saves encrypted messages and reads them for decryption.

## Code Breakdown
### 1. Importing Libraries
```python
from cryptography.fernet import Fernet
```
The `cryptography` library is used to implement encryption and decryption.

### 2. Key Generation
```python
def generate_key():
    key = Fernet.generate_key()
    with open("secret.key", "wb") as key_file:
        key_file.write(key)
```
- Generates a key using `Fernet.generate_key()`.
- Saves the key to a file (`secret.key`).

### 3. Loading the Key
```python
def load_key():
    return open("secret.key", "rb").read()
```
- Reads the previously generated key from `secret.key`.

### 4. Encrypting Data
```python
def encrypt_message(message):
    key = load_key()
    f = Fernet(key)
    encrypted_message = f.encrypt(message.encode())
    return encrypted_message
```
- Loads the encryption key.
- Encrypts the message using `Fernet`.
- Returns the encrypted message.

### 5. Decrypting Data
```python
def decrypt_message(encrypted_message):
    key = load_key()
    f = Fernet(key)
    decrypted_message = f.decrypt(encrypted_message).decode()
    return decrypted_message
```
- Loads the encryption key.
- Decrypts the message.
- Returns the original plaintext message.

### 6. User Input & Execution
```python
if __name__ == "__main__":
    choice = input("Do you want to encrypt or decrypt a message? (e/d): ")
    if choice == "e":
        message = input("Enter the message to encrypt: ")
        encrypted = encrypt_message(message)
        print(f"Encrypted Message: {encrypted}")
    elif choice == "d":
        encrypted = input("Enter the encrypted message: ")
        decrypted = decrypt_message(encrypted.encode())
        print(f"Decrypted Message: {decrypted}")
    else:
        print("Invalid choice!")
```
- Takes user input for encryption or decryption.
- Calls the appropriate function based on user choice.
- Prints the encrypted or decrypted message.

## Usage
1. Run the script:
```bash
python INFR2141_Final_Project_Group4.py
```
2. Choose an option:
   - **Encrypt a message**: Type `e` and enter the plaintext.
   - **Decrypt a message**: Type `d` and enter the encrypted text.

## Contributing
Contributions are welcome! If you find issues or want to improve the code, feel free to open a pull request.

## License
This project is open-source and available under the MIT License.

