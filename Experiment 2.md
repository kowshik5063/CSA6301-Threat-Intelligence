import hashlib
def calculate_hash(filename):
    sha256_hash = hashlib.sha256()
    with open(filename, "rb") as f:
        for byte_block in iter(lambda: f.read(4096), b""):
            sha256_hash.update(byte_block)
    return sha256_hash.hexdigest()
with open("example.txt", "w") as f:
    f.write("This is the original file content.")
original_hash = calculate_hash("example.txt")
print("Original File Hash:", original_hash)
with open("example.txt", "w") as f:
    f.write("This file has been modified!")
modified_hash = calculate_hash("example.txt")
print("Modified File Hash:", modified_hash)
if original_hash == modified_hash:
    print("File integrity verified: No changes detected.")
else:
    print("File integrity compromised: The file has been tampered with!")
    <img width="1027" height="731" alt="Screenshot 2026-07-11 132633" src="https://github.com/user-attachments/assets/e99c8a65-c0c1-408f-88e6-170f3c0e08af" />
