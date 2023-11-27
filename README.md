# GPG GitHub Tutorial for Beginners 

## Introduction

This tutorial provides a step-by-step guide on how to use GPG encryption with GitHub to encrypt commits and signatures. This allows you to verify work and sign commits cryptographically to ensure authenticity.

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
(Select option for RSA and RSA)
(Select 4096 bit key size when prompted)  

(Select whether key should expire)  

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


To verify signed commit:

```
git show --show-signature MostRecentCommitHash 
```

Green verified message indicates successful PGP signing.

## Back Up Your GPG Private Key  

1. Export private key:  
   ``` 
   gpg --export-secret-keys [KEY_ID] > my-private-key-backup.gpg
   ```
2. Store backup in very safe & secure place (e.g. encrypted USB drive)  

## Additional Resources 

- [GitHub Docs on GPG Commit Signing](https://help.github.com/articles/signing-commits-with-gpg/)
- [GNU Privacy Guard Documentation](https://gnupg.org/documentation/index.html)  
