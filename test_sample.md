# Test Results

Python version used: 3.__ | Operating system: ________ | Date: ________

| # | Input | Expected result | Actual result | Pass/Fail |
|---|-------|-----------------|---------------|-----------|
| 1 | https://www.example.com/login | No listed warning signs | | |
| 2 | http://192.0.2.10/account | IP address + HTTP | | |
| 3 | http://example.com@sample.invalid/login | @ symbol + HTTP | | |
| 4 | https://a.b.c.d.e.example.invalid/path | Many hostname segments | | |
| 5 | https://xn--example.invalid/ | Punycode-style hostname | | |

## Notes
Write 2 or 3 lines: what you learned, and what surprised you.
