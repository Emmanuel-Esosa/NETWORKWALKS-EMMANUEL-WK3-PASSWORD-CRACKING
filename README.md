# NETWORKWALKS-EMMANUEL-WK3-PASSWORD-CRACKING
Week 3 Cybersecurity Internship Project- Password cracking with John the Ripper(JTR) AND Networkwalks tools.

### INFORMATION

| Field | Details |
| --- | --- |
| Student Name | Emmanuel-Osagie Esosa Ifeoluwa |
| Training Institution | NetworkWalks Academy |
| Programme | Cybersecurity Training, Batch B084 |
| Assessment | Week 3 Practical Assessment |
| Main Modules | W3-PM1 and W3-PM2 |
| Operating System | Kali Linux |

---

## 1. LIABILITY DISCLAIMER

This repository documents practical cybersecurity exercises completed as part of the NetworkWalks Academy cybersecurity training programme.

All activities documented in this report were conducted for educational purposes within the scope of the assigned training exercises and authorized lab environment, using password-protected files provided for this exercise.

The tools and techniques demonstrated are intended for ethical cybersecurity learning, password security awareness, and defensive security education. No unauthorized access or testing outside the approved training scope is intended or endorsed.

---

## 2. INTRODUCTION

The Week 3 cybersecurity assessment focused on password security and password-cracking concepts in a controlled learning environment.

The practical exercises involved extracting password hashes from three protected PDF files and recovering their passwords, first using John the Ripper (JTR) natively on Kali Linux, and then using NetworkWalks' own online Hash Calculator and Password Cracker tools. Running both methods against the same files also made it possible to compare the two approaches directly.

---

## 3. OBJECTIVES

The main objectives of the assessment were to:

- Understand how password hashes are extracted from protected files.
- Gain practical experience with John the Ripper (JTR).
- Explore the NetworkWalks Hash Calculator and Password Cracker tools.
- Compare results between a native command-line tool and an online tool.
- Understand how wordlist choice affects password-cracking speed and success.
- Document practical results and collect evidence of completed exercises.

---

## 4. TOOLS AND TECHNOLOGIES USED

| Tool / Technology | Purpose |
| --- | --- |
| Kali Linux | Cybersecurity testing and learning environment |
| pdf2john.pl | Extracting a crackable hash from a password-protected PDF |
| John the Ripper (JTR) | Password security testing and recovery |
| NetworkWalks Hash Calculator | Extracting password hashes from protected PDF files, in the browser |
| NetworkWalks Password Cracker | Testing extracted hashes against chosen wordlists |

---

## 5. MODULES COMPLETED

| Module | Description | Status |
| --- | --- | --- |
| W3-PM1 | Password Cracking with John the Ripper | Completed |
| W3-PM2 | Password Cracking with NetworkWalks Tools | Completed |

---

## 6. ACTIVITIES PERFORMED

### 6.1 W3-PM1 – Password Cracking with John the Ripper

John the Ripper comes pre-installed on Kali Linux, so this module was carried out directly in the terminal. For each of the three provided PDF files, a password hash was first extracted using pdf2john.pl and saved to its own hash file. John the Ripper was then run against each hash file in turn.

John the Ripper first ran its single-crack mode. When no match was found, it proceeded to its default wordlist and successfully recovered the passwords for all three PDF files.

### 6.2 W3-PM2 – Password Cracking with NetworkWalks Tools

The second module used NetworkWalks' own browser-based tools, with no terminal or installation involved. For each PDF, the file was uploaded to the Hash Calculator to extract its hash, which was then pasted into the Password Cracker and run against a chosen wordlist.

The built-in 100-password list was not enough to crack the first file, so a larger wordlist was uploaded instead, after which the attack succeeded; the same larger wordlist also recovered the passwords for the second and third files. I then tried the same three files against a smaller curated wordlist and the built-in list as well, to compare how each performed (see section 7).

---

## 7. RESULTS AND OBSERVATIONS

All three results were confirmed independently by both John the Ripper and the NetworkWalks Password Cracker, which gives good confidence in the findings.

Key observations:

- Password hashes can be pulled directly out of a protected PDF without first knowing the password, using either pdf2john.pl or the NetworkWalks Hash Calculator.
- Weak or common passwords can be recovered in seconds once a wordlist that contains them is used.
- John the Ripper and NetworkWalks' online tools, used independently, gave the same three results.

I also compared three wordlists of different sizes against all three files, to see how wordlist choice affects cracking: NetworkWalks' built-in 100-password list, a 221-word curated list (fasttrack.txt), and John the Ripper's own 3,556-word default list. The position at which each wordlist found the correct password (counted as word number / total words in that list) was:

| File | JTR list (3,556 words) | fasttrack.txt (221 words) | Built-in list (100 words) |
| --- | --- | --- | --- |
| My Locked PDF1.pdf | Found at 3,456 / 3,556 | Not found | Not found |
| My Locked PDF2.pdf | Found at 15 / 3,556 | Found at 81 / 221 | Found at 91 / 100 |
| My Locked PDF3.pdf | Found at 2,078 / 3,556 | Found at 212 / 221 | Found at 35 / 100 |

The larger JTR list was the only one that contained every password and so was the only list to crack all three files; the two smaller lists both missed PDF1's password entirely. Where a password did appear in more than one list, its position was not consistently near the start or end of either list: First locked pdf password was found early in the large list (position 15) but later in the two smaller ones, while third locked pdf password was found in the second half of the large list but still faster overall through fasttrack.txt, since fasttrack.txt is so much shorter to begin with. The main lesson is that a wordlist's coverage (whether it contains the target password at all) matters more than its size or ordering; a smaller list only wins on speed when it happens to contain the password, and offers no guarantee otherwise.

A few practical issues came up and were resolved along the way: the hash-extraction script needed the Perl interpreter rather than Python, since it is a .pl script; and a hash was briefly saved under the wrong filename, which was caught immediately and corrected.

---

## 8. RISK ANALYSIS / IMPACT

The exercise demonstrated that password-protected documents secured with weak or commonly used passwords may be vulnerable to password recovery attempts using wordlists.

In an organisational environment, this could expose confidential information contained in protected documents, potentially affecting data confidentiality and privacy. It also shows that password protection alone may not provide sufficient security when weak passwords are used.

The potential impact depends on the sensitivity of the documents and the information they contain. Although this exercise was conducted using training files, the findings highlight the importance of applying strong password security practices when protecting organisational information.

---

## 9. RECOMMENDATIONS

Based on the findings and potential impacts identified during the password security assessment, the following recommendations are proposed:

1. **Enforce strong password policies:** Encourage the use of long, unique passwords that are not easily found in common wordlists or dictionary databases.

2. **Discourage predictable passwords:** Users should avoid common words, personal information and predictable keyboard patterns when creating passwords.

3. **Use appropriate file encryption:** Sensitive PDF documents should be protected using strong encryption and robust passwords to reduce the risk of unauthorised access.

4. **Implement Multi-Factor Authentication (MFA):** Where password-protected documents are accessed through user accounts or online platforms, MFA should be enabled to provide an additional layer of protection.

5. **Promote password management practices:** Encourage the use of reputable password managers to generate and securely store unique passwords.

---

## 10. CONCLUSION
The exercise demonstrated that wordlist coverage and ordering both influence password recovery. A smaller curated list can recover a password in fewer attempts when that password appears earlier in the list, while a larger list may provide broader coverage.

---

## 11. EVIDENCE COLLECTED

The following screenshots provide visual evidence of the practical activities and results achieved during the Week 3 assessment.

**Hash Extraction Troubleshooting:** Initial Perl/Python-related issue encountered during PDF hash extraction.

<img width="1431" height="549" alt="perl, python error pdf1" src="https://github.com/user-attachments/assets/2790b17b-e631-4451-9a0a-d1d918d80c7e" />


**PDF 1 Successful Password Cracking:** John the Ripper successfully cracked the password for PDF 1

<img width="1433" height="634" alt="PDF1 password found zoomed no perl command" src="https://github.com/user-attachments/assets/622c3559-bcda-424d-a863-348dee8ea7e3" />


**PDF 2 Hash Extraction and Successful Password Cracking:** Resolution of the hash-overwriting issue, followed by successful password cracking

<img width="1439" height="780" alt="PDF2 CRACKED overwrote hash2 " src="https://github.com/user-attachments/assets/e5535b0f-35a6-4f1d-a8b4-e53d80093ce6" />


**PDF 3 Successful Password Cracking:** John the Ripper successfully cracked the password for PDF 3

<img width="1431" height="629" alt="USE PDF3 password found zoomed" src="https://github.com/user-attachments/assets/dedc64e7-790b-49c9-9e13-8d3c0035839d" />


### Evidence 5 

<img width="698" height="699" alt="PDF1 cracked" src="https://github.com/user-attachments/assets/32e7d477-267a-45f1-9705-25225c774839" />


### Evidence 6 

<img width="694" height="705" alt="PDF2 cracked" src="https://github.com/user-attachments/assets/22f7913a-b071-46cc-9fd9-3c22e592de42" />


### Evidence 7 

<img width="694" height="705" alt="PDF3 cracked" src="https://github.com/user-attachments/assets/98e0820b-3cfb-4b4f-81fa-492699f2f940" />


### Evidence 8

<img width="1433" height="812" alt="Builtin first fsilure" src="https://github.com/user-attachments/assets/82644972-b471-4c6a-bf79-58c72c906b0f" />


### Evidence 9

<img width="1436" height="811" alt="pdf1 password found tools" src="https://github.com/user-attachments/assets/75a954c3-e19b-406f-bd02-ef315c57ad50" />


### Evidence 10

<img width="1440" height="811" alt="pdf2 password found tool" src="https://github.com/user-attachments/assets/7f9da7e4-cd82-4994-8e3d-4435a3f57de5" />

### Evidence 11

<img width="1440" height="811" alt="pdf3 password found tool" src="https://github.com/user-attachments/assets/94580a6f-5724-41fc-a09f-c333d34fd52a" />


---

## 12. AUTHOR

**Emmanuel-Osagie Esosa Ifeoluwa**

Cybersecurity intern | NetworkWalks Academy, Batch B084

- **LinkedIn:** [https://www.linkedin.com/in/esosa-ifeoluwa-emmanuel-4b2364349](https://www.linkedin.com/in/esosa-ifeoluwa-emmanuel-4b2364349)

