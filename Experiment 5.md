import socket

domains = [
    "www.google.com",
    "www.python.org",
    "notarealdomain12345.com"
]

print("=" * 60)
print("        DNS LOOKUP (OSINT BASICS)")
print("=" * 60)

for domain in domains:
    try:
        ip = socket.gethostbyname(domain)
        print(f"{domain:35} -> {ip}")
    except socket.gaierror:
        print(f"{domain:35} -> Could not resolve (invalid/unreachable)")

print("\nDNS Lookup Complete!")
<img width="1357" height="803" alt="Screenshot 2026-07-14 112921" src="https://github.com/user-attachments/assets/bd759b44-4586-422d-969e-4c67441e38ff" />
