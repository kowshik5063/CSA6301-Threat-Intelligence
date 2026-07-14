import re

def check_url(url):
    reasons = []

    if re.match(r"https?://\d{1,3}(\.\d{1,3}){3}", url):
        reasons.append("Uses raw IP address instead of domain name")

    if "@" in url:
        reasons.append("Contains '@' symbol (can hide real destination)")

    if url.count("-") > 3:
        reasons.append("Too many hyphens in domain (common phishing trick)")

    keywords = ["login", "verify", "update", "secure"]
    if any(keyword in url.lower() for keyword in keywords) and not url.startswith("https://"):
        reasons.append("Suspicious keyword without HTTPS")

    return reasons

urls = [
    "https://www.google.com",
    "http://192.168.10.5/login",
    "http://paypal-verify-account.com@evil.com",
    "https://github.com",
    "http://secure-login-update.com",
    "https://amazon.com"
]

print("=" * 60)
print("           PHISHING URL DETECTOR")
print("=" * 60)

for url in urls:
    issues = check_url(url)
    verdict = "SUSPICIOUS" if issues else "Looks OK"

    print(f"\nURL: {url}")
    print(f"Verdict: {verdict}")
<img width="1357" height="803" alt="Screenshot 2026-07-14 112921" src="https://github.com/user-attachments/assets/d0697fe5-b060-409f-9f31-15de7835c0e3" />

    if issues:
        print("Reasons:")
        for reason in issues:
            print(f" - {reason}")

print("\nAnalysis Complete!")
