# GPG GitHub Tutorial for Beginners

## Introduction

This tutorial provides a step-by-step guide on using GPG signatures with GitHub to cryptographically sign commits for identity verification and integrity. Digitally signing commits with GPG allows you to generate tamper-evident hashes that validate author identity rather than encrypting the contents. This allows others to trust that specific approved GPG keys were used to produce commits pushed from a GitHub account.

## Prerequisites  

Before starting, make sure you have the following:  

- GPG command line tools installed
- A GitHub account  
- Git command line tools installed
- A text editor like Visual Studio Code

## Generate a GPG Key Pair  

```
gpg --full-generate-key
```

(Select option 1 for RSA and RSA)  
(Select 4096-bit key size when prompted)

(Select whether the key should expire)  

(Enter GitHub email address for user ID)

(Enter a secure passphrase) 

## Get Your GPG Public Key ID  

```
gpg --list-secret-keys --keyid-format LONG
```

(Identify and copy the GPG key ID you'd like to use)

## Export GPG Public Key  

```
gpg --armor --export [email used for key gen] 
```

(Copy key beginning with -----BEGIN PGP PUBLIC KEY BLOCK-----)

## Add Your GPG Key to GitHub   

1. Go to GitHub --> Settings --> SSH and GPG keys   
2. Click New GPG key, paste your public key, and click Add GPG key

## Configure Git to Use GPG

```
git config --global user.signingkey YOUR-KEY-ID   

git config --global gpg.program gpg  
```

## Signing Commits with GPG  

```
git commit -S -m "your commit message"
``` 
(Enter your GPG passphrase when prompted)

## Verify Signatures on Cloned Repo

```
git verify-commit LocallySignedCommitHash
```

Green verified message indicates successful PGP signing.

## Amending Commits

If you forget to sign commit initially:

```  
git commit --amend -S -m "commit message"
```

## Back Up Your GPG Private Key   

1. Export private key:   
   ```   
   gpg --export-secret-keys [KEY_ID] > my-private-key-backup.gpg
   ```
2. Store backup in a very safe & secure place (e.g. encrypted USB drive)   

## Additional Resources    

- [GitHub Docs on GPG Commit Signing](https://help.github.com/articles/signing-commits-with-gpg/)
- [GNU Privacy Guard Documentation](https://gnupg.org/documentation/index.html)
