## GPG Key Setup for Git Commit Signing and Verification

This guide explains how to generate a GPG key for signing Git commits and verifying them in Jenkins.

---

### Step 1: Install GPG

Make sure **GPG (GNU Privacy Guard)** is installed.

### Linux / macOS
```bash
sudo apt install gnupg -y       # Ubuntu/Debian
# or
brew install gnupg              # macOS
```

### Step 2: Generate a New GPG Key
Run 
```bash 
gpg --full-generate-key
```

#### GPG Key Generation Guide

Follow the steps below to generate a GPG key for Git commit signing or verification.

#### GPG Key Details

When prompted, provide the following information:

| Prompt             | Example Input                                |
|-------------------|---------------------------------------------|
| **Key type**       | `1` (RSA and RSA)                           |
| **Key size**       | `4096`                                      |
| **Expiration**     | `0` (never expire) or `1y` for 1 year      |
| **Real name**      | `Naveen Ramlu`                              |
| **Email address**  | `your Git email` (e.g., `naveen@example.com`) |
| **Comment**        | *(optional)*                                |
| **Passphrase**     | Choose a strong one                         |

Once done, list your keys:
```bash 
gpg --list-secret-keys --keyid-format=long
```
Example output:
/home/naveen/.gnupg/secring.gpg

#### Key Details

| Type        | Key ID              | Algorithm / Size | Expiration  | Usage         |
|------------|-------------------|----------------|------------|---------------|
| **Primary** | `ABCDEF1234567890` | RSA 4096       | 2025-10-26 | SC (Sign & Certify) |
| **Subkey**  | `1234ABCD5678EF90` | RSA 4096       | 2025-10-26 | E (Encrypt)    |

#### Fingerprint
1234 5678 9ABC DEF1 2345 6789 0ABC DEF1 2345 6789

### Step 3: Export Keys
Private Key (for Jenkins verification)

Export securely:
```bash 
gpg --export-secret-keys --armor ABCDEF1234567890 > my-gpg-key.asc
```

⚠️ Keep this file secret — treat it like a password.

Public Key (for developers or verification)

Export public key:
```bash 
gpg --export --armor ABCDEF1234567890 > my-gpg-pub.asc
```

You can share this with your team or add it to GitHub/GitLab for commit verification.

### Step 4: Configure Git to Use This Key
```bash 
git config --global user.signingkey ABCDEF1234567890
git config --global commit.gpgsign true
```

Optional (if GPG program path issues occur):
```bash 
git config --global gpg.program gpg
```

Now every commit will be signed automatically:
```bash 
git commit -S -m "Signed commit message"
```

Verify a commit:
```bash 
git log --show-signature -1
```
### Step 5: Upload GPG Key to Jenkins

### Steps

1. Navigate to Jenkins:

Manage Jenkins → Credentials → Global → Add Credentials
2. Choose the following options:

| Field         | Value                                           |
|---------------|------------------------------------------------|
| **Kind**      | Secret file                                    |
| **File**      | Upload `my-gpg-key.asc`                        |
| **ID**        | e.g., `gpg-signing-key`                        |
| **Description** | "Private GPG key for commit verification"    |

3. Click **Save ✅**

#### Notes

- Jenkins can now securely import this key during pipeline runs.
- Use the ID `gpg-signing-key` in your pipelines to reference the uploaded GPG key.


### Step 6: Share Your Public Key (Optional but Important)

If using GitHub or GitLab:
```bash 
Go to Settings → SSH and GPG keys → New GPG Key
Paste the contents of my-gpg-pub.asc
```

GitHub will mark your commits as “Verified”.

### GPG Key Setup & Git Commit Signing

This guide summarizes the steps to generate a GPG key, configure Git to sign commits, and securely store the key in Jenkins.

#### Summary of Steps

| Step | Command / Action                                           | Purpose                                  |
|------|------------------------------------------------------------|-----------------------------------------|
| 1    | `gpg --full-generate-key`                                  | Create GPG key pair                     |
| 2    | `gpg --list-secret-keys --keyid-format=long`              | Get key ID                               |
| 3    | `gpg --export-secret-keys --armor <KEYID> > my-gpg-key.asc` | Export private key (for Jenkins)        |
| 4    | `gpg --export --armor <KEYID> > my-gpg-pub.asc`           | Export public key (for developers / GitHub) |
| 5    | Upload private key to Jenkins as **Secret File**           | For commit verification                  |
| 6    | `git config --global user.signingkey <KEYID>`             | Configure Git to sign commits            |

#### Notes

- Replace `<KEYID>` with your actual GPG key ID from step 2.
- Ensure the private key file `my-gpg-key.asc` is securely stored and uploaded only to Jenkins.
- Developers can use the public key `my-gpg-pub.asc` to verify commits.
- Once configured, all Git commits will be signed automatically.
