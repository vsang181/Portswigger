# Brute-Forcing Passwords (Human Behaviour & Predictable Patterns)

While strict password policies aim to force high randomness (**entropy**), human habits often reintroduce predictable weaknesses that attackers can exploit.

## How Users Weaken Strong Password Policies

- **Forcing Simple Words to Fit Rules**: Instead of creating truly random strings, users usually take an easy-to-remember word and tweak it just enough to pass the policy checks. For example, `mypassword` becomes `Mypassword1!` or `Myp4$$w0rd`.

- **Predictable Password Rotations**: When websites force periodic password resets, users rarely invent a brand-new password. Instead, they make minor, sequential edits to their existing one, such as changing `Mypassword1!` to `Mypassword1?` or `Mypassword2!`.

## Why This Matters for Attackers

- **Targeted Wordlists**: Because humans follow common patterns (such as capitalising the first letter and adding a number and symbol at the end), attackers do not need to guess every random character combination.

- **Rule-Based Attacks**: Attackers use password-cracking tools with transformation rules (like "leetspeak" substitutions or appending `1!`) to guess complex passwords much faster.
