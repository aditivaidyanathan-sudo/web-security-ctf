# Web Security CTF — 10-Level Penetration Testing Challenge
10-level web application penetration testing CTF. Exploited and  documented XSS, SQL injection, command injection, IDOR, Shellshock,  cookie manipulation, and Java bytecode reverse engineering using  Burp Suite, SQLMap, and curl. Each level writeup includes methodology.

## Overview
A 10-level web application security CTF covering a wide range of real-world 
attack techniques, documented with methodology and payloads.

## Levels Completed

| Level | Vulnerability | Technique |
|-------|--------------|-----------|
| 1 | Credential exposure | JS console manipulation, source code review |
| 2 | Header spoofing | curl with custom Referer header |
| 3 | Reflected XSS | `<script>printFlag();</script>`, Base64 decoding |
| 4 | Command injection | URL-encoded payload, Referer bypass |
| 5 | Weak auth + IDOR | Default credentials, uid parameter manipulation |
| 6 | Cookie manipulation | ROT13 encoding, Burp Suite |
| 7 | SQL injection | SQLMap `--dump --dbs` on username field |
| 8 | Hidden field + cookie | Burp Suite Repeater, admin=1 injection |
| 9 | Shellshock | URL-encoded payload bypassing input sanitisation |
| 10 | Reverse engineering | Java bytecode decompilation (JD-GUI), Python decryption script |

## Tools Used
`Burp Suite` `SQLMap` `curl` `JD-GUI` `Browser DevTools` `Python`

## Key Takeaways
- Shellshock and command injection often require encoding to bypass sanitisation
- Cookie-based auth is trivially bypassable without server-side validation
- Java bytecode can be reverse engineered to extract encrypted flags

## Reflection

What surprised me most across these 10 levels was how rarely the vulnerability 
was technically sophisticated — and how often it came down to missing validation, 
exposed source code, or misplaced trust in client-supplied input. Level 1 hid 
credentials in an HTML comment. Level 5 used admin:admin. These aren't edge 
cases; they're among the most common findings in real penetration tests.

The challenges that pushed me hardest were Levels 3 and 9. In Level 3, I 
initially overcomplicated the XSS payload when the actual solution was simply 
calling the already-existing printFlag() function — a reminder that in security 
testing, understanding what the code is *trying* to do is often more valuable 
than brute-forcing payloads. Level 9 (Shellshock) was harder because the input 
sanitisation made the vulnerability non-obvious; I had to recognise that the 
filter itself was the clue, and that URL encoding was the bypass.

Working through SQL injection in Level 7 using SQLMap was interesting from a 
tooling perspective — it automated what would have been hours of manual testing 
in seconds. But the more important lesson was understanding *why* the username 
field was injectable in the first place (no parameterised queries), because that 
understanding is what transfers to code review and secure development work.

Overall, this CTF reinforced that effective security testing is as much about 
reading and reasoning about code as it is about knowing which tools to run.
