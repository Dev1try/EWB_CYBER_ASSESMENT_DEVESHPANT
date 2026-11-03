# EWB Phishing URL Awareness Checker

## Overview
Phishing is a trick where criminals send fake links or messages to make
people give away passwords, card numbers or OTPs. This project is a small
Python command-line tool that reads a URL as plain text and points out
six visible warning signs. It never opens the URL or sends any data.

## Features
- Detects an @ symbol in the URL
- Flags unusually long URLs (over 100 characters)
- Flags IP-address hostnames
- Flags many hostname segments (5 or more)
- Flags punycode-style hostnames (xn--)
- Flags the HTTP scheme
- Loop mode: check many URLs in one run, type q to quit
- "REVIEW CAREFULLY" summary with a count of warning signs
- Safe handling of malformed input (no crash)

## Requirements
Python 3.10 or later. No extra packages.

## How to Run
Windows: python phishing_checker.py
Mac/Linux: python3 phishing_checker.py

## Example Output
```
EWB Phishing URL Awareness Checker
Text checks only - this program does not open URLs.

Enter a sample URL (or type q to quit): http://192.0.2.10/account

Result:
- Uses an IP address instead of a familiar domain.
- Uses HTTP. HTTPS alone does not prove trust.

REVIEW CAREFULLY: 2 warning sign(s) found.
Never enter passwords from unexpected links.
```

## Testing
| # | Input | Expected | Actual | Result |
|---|-------|----------|--------|--------|
| 1 | https://www.example.com/login | No warning signs | No listed warning signs found | PASS |
| 2 | http://192.0.2.10/account | IP address + HTTP | IP address and HTTP flagged | PASS |
| 3 | http://example.com@sample.invalid/login | @ symbol + HTTP | @ symbol and HTTP flagged | PASS |
| 4 | https://a.b.c.d.e.example.invalid/path | Many hostname segments | Many segments flagged | PASS |
| 5 | https://xn--example.invalid/ | Punycode-style hostname | Punycode flagged | PASS |

Full table: tests/test_samples.md

## Screenshots
![Sample run](screenshots/sample_run.png)
![Test results](screenshots/test_results.png)

## Improvements
1. **Loop with quit (A)** - The original asked for one URL and exited. I
   wrapped the input in a `while True` loop that stops when the user types
   q, quit or exit. This is easier to use when testing many URLs. I tested
   it by entering two URLs in a row and then q.
2. **Review carefully summary (B)** - I added a `has_warnings()` helper
   that tells real warnings apart from information messages, so the tool
   prints "REVIEW CAREFULLY: N warning sign(s) found." only when needed.
   I tested it with a URL with warnings and one without.
3. **Malformed input handling (C)** - Typing `http://[bad` made Python
   raise a ValueError and crash. I wrapped `urlparse` in `try/except` so
   the tool prints "This text is not a valid URL format." instead. I then
   re-ran all five tests to confirm nothing broke.

## Limitations
This is an educational tool. It only reads URL text. It does not visit
URLs, scan for malware or prove that a URL is safe. No warning signs
found does NOT mean a URL is safe.

## Ethical Use
Use sample strings only. Do not collect credentials. Do not use this
project to deceive anyone or to test websites without permission.

## Author
Sample Author, Instructor Reference, EWB Courses
