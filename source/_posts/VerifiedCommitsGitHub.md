---
title: Verified Commits in the GitHub
date: 2024-07-10 22:09:24
tags:
---



Verified commits in GitHub are those that are signed and can be cryptographically verified to ensure that they come from a trusted source. Here's how you can set up and use GPG to sign your commits and tags:



## Step-by-Step Guide to Verified Commits

### 1. Install GPG

If you don't have GPG installed, you can install it using the following commands:

```bash
sudo apt install gnupg
```

### 2. Generate a GPG Key

If you don't already have a GPG key, you can generate one using the following command:

```bash
gpg --full-generate-key
```

Follow the prompts to generate your key. Choose RSA and RSA, key size of 4096 bits, and a key expiration period as per your preference.

### 3. List Your GPG Keys

To list your GPG keys and find the key ID, use the following command:

```bash
gpg --list-secret-keys --keyid-format LONG
```

Output:

```bash
gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
/home/raman/.gnupg/pubring.kbx
------------------------------
sec   rsa4096/69A232962D78CB0A 2024-07-06 [SC]
      29C678E0F97172E8238E1B3A69A232962D78CB0A
uid                 [ultimate] raman (created to do the verified commits) <kkraman02@gmail.com>
ssb   rsa4096/3DCDC68CC5F4C641 2024-07-06 [E]
```

### 4. Export Your GPG Key

export your GPG key in ASCII format:

```bash
gpg --armor --export 69A232962D78CB0A
```

copy and paste the generated **PUBLIC KEY BLOCK** to the here(https://github.com/settings/keys) -> GPG keys.

### 5. Configure Git to Use Your GPG Key

Set Git to use your GPG key for signing commits:

```bash
git config --global user.signingkey 69A232962D78CB0A
```

### 6. Sign Your Commits

To sign your commits, add the `-S` flag to the commit command:

```bash
git commit -S -m "Your commit message"
```

### 7. How to check verified and unverified commits

```bash
git log --show-signature	# show verified commits
git log
```