def encrypt(text, shift):
    result = ""
    for char in text:
        if char.isalpha():  
        
            base = ord('A') if char.isupper() else ord('a')
            result += chr((ord(char) - base + shift) % 26 + base)
        else:
            result += char  
    return result

def decrypt(text, shift):
    return encrypt(text, -shift)

plaintext = "ATTACKATDWAN"
shift = 3  

ciphertext = encrypt(plaintext, shift)
decrypted_text = decrypt(ciphertext, shift)

print("Plaintext:", plaintext)
print("Ciphertext:", ciphertext)
print("Decrypted:", decrypted_text)
<img width="887" height="837" alt="Screenshot 2026-07-11 132343" src="https://github.com/user-attachments/assets/3c51701c-b1bf-4e9b-8be4-410a8bf2dda5" />
