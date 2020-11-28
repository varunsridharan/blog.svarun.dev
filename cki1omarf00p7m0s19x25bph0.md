## Convert Putty Key Gen File Into RSA Key File

As a windows user i generate my SSH keys using `Putty Key Generator` which provides the key in `.ppk`. but today i had a special requirement which required my **SSH** Key in ***RSA*** Format

Since i learned something new on how to convert `.ppk` into `RSA` i thought that i could share it with you to.

## Lets Get Started

### Requirements
1. Putty Generated Key
2. Putty Key Generator App For Windows
3. Linux Server (Ubuntu preferred)

### Step 1
Load the **Private Key File** in Putty Key Generator and export it as OpenSSH Key

![Image](https://s2.do-spaces.com/2020/Nov/28/160656658160.jpg)

The exported key file should have text "BEGIN OPENSSH PRIVATE KEY"
![Exported File](https://s2.do-spaces.com/2020/Nov/28/160656672478.jpg)

### Step 2
Upload the file to a Linux server and run the below cmd which will convert the OpenSSH Key into RSA and update the same file

```
ssh-keygen -p -m PEM -f  {your-key-filename}
```

### Step 3
Thats it. your putty Generated key file is now converted to RSA key. 

---

%%[blog-footer]

---

