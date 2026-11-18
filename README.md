# PDF Password Cracking Lab (Dictionary Attack)

Week 3 practical for the Networkwalks Cybersecurity Internship. The exercise: extract a crackable hash from a password-protected PDF and recover the password with a dictionary attack.

## Scope and authorization

- **Targets:** three PDFs I created and encrypted myself (`My Locked PDF1.pdf`, `My Locked PDF2.pdf`, `My Locked PDF3.pdf`). No third-party or production files were used.
- **Tools:** Networkwalks' browser-based Hash Calculator and Dictionary Attack tool (built-in 100-word list). Processing happens locally in the browser; files are not uploaded to a server.
- **Technique:** dictionary attack — the same approach used by John the Ripper, hashing each wordlist entry and comparing it to the PDF's password hash.

Only crack passwords on files you own or have explicit permission to test.

## Method

1. **Extract the hash.** Upload the locked PDF to the Hash Calculator. It parses the PDF locally and extracts a `pdf2john`/hashcat-compatible `$pdf$...` hash.
2. **Run the attack.** Paste the hash into the Dictionary Attack tool and run it against the built-in wordlist.
3. **Recover the password.** The tool reports each attempt and stops at a match.

## Results

| PDF | Hash format | Attempts to crack | Password found |
|---|---|---|---|
| My Locked PDF1 | `$pdf$4*4*128*-1028*1*16...` | 9 / 100 | `good-luck` |
| My Locked PDF2 | `$pdf$4*4*128*-1028*1*16...` | 91 / 100 | `password1` |
| My Locked PDF3 | `$pdf$4*4*128*-1028*1*16...` | 35 / 100 | `1qaz2wsx` |

Crack speed was low (4-16 passwords/sec) since this ran in-browser against a small built-in list; a GPU tool like hashcat with a large wordlist would be far faster.

## What I learned

- A PDF's password isn't stored directly; it's a hash plus salt-like values that a cracking tool compares candidate passwords against.
- Dictionary attacks only succeed if the real password is in the wordlist. PDF2 took 91 attempts because `password1` was near the end of the built-in list; a weak but less common password takes longer to find even with a small list.
- All three test passwords were common, easily-guessed strings, which is exactly what makes dictionary attacks effective against real-world weak passwords.
- Strong PDF passwords should be long, random, and outside any common wordlist.

## Files

- `PDF1_Password.png`, `PDF2_Password.png`, `PDF3_Password.png`: dictionary attack in progress and result for each PDF
- `Hash_Calculator.png`: hash extraction from a locked PDF
- `My Locked PDF1.pdf`, `My Locked PDF2.pdf`, `My Locked PDF3.pdf`: the encrypted sample files (still password-protected)

Completion-flag screenshots are kept out of this repo, since each flag is unique per student and meant to show the work was done independently.
