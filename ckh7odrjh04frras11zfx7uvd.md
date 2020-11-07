## How To Setup Deploy 🔑 In Github Repository?

## What is the Deploy key?
Deploy key is an SSH key configured in your repository to grant `read` or `write` access without logging into your GitHub account.

## Why should I use it?
Using **Deploy Keys** can come in handy when you don't want to login to your GitHub account on a machine or just wanted to configure a single repository in that machine.

As the name says, its primary function is to be used in places where `read-only` access is needed. Therefore keep the repository safe from the attack, in case the server-side is fallen.

> Before we start first, let's create a new Github Repository if you don't have 1 already.

* ⚙️ [Generating SSH Keys](#generating-ssh-keys)
* 🔩  [Configuring Local Machine](#generating-ssh-keys)
* 🔩  [Configuring Github Repository](#generating-ssh-keys)
* 🧪 [Testing](#generating-ssh-keys)

---

### ⚙️  Generating SSH Keys
1. Open **Terminal** / Open **Git Bash** if you are on windows 
2. Run `ssh-keygen -t ed25519 -C "your_email@example.com"` make sure to replace `your_email@example.com` with your email which is associated GitHub.com
	
When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location. You also save it in any location
```bash
Enter a file in which to save the key (/xyz/xyz/.ssh/id_ed25519):
```
At the prompt, type a secure passphrase
```bash
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```
![https://s2.do-spaces.com/2020/Nov/07/1604740021-136.gif](https://s2.do-spaces.com/2020/Nov/07/1604740021-136.gif)
---

### 🔩  Configuring Local Machine
Add your SSH private key to the ssh-agent. If you created your key with a different name, in a different location, or if you are adding an existing key that has a different name, replace id_rsa in the command with the name of your private key file.

***Before adding a new SSH key to the ssh-agent*** make sure the **ssh-agent** is running.

```bash
eval "$(ssh-agent -s)"
```
The above cmd will output similar to `Agent pid 111931` which means the agent is up & running

```bash
ssh-add {your-key-location}
```
> Replace `{your-key-location}` with the actual path for that key file

![https://s2.do-spaces.com/2020/Nov/07/1604747908-124.gif](https://s2.do-spaces.com/2020/Nov/07/1604747908-124.gif)

---

### 🔩  Configuring Github Repository
Copy public key from the `{key-file-name}.pub` file
![https://s2.do-spaces.com/2020/Nov/07/1604740282-139.gif](https://s2.do-spaces.com/2020/Nov/07/1604740282-139.gif)

1. Navigate to your repository
2. Click `⚙️ Settings`
3. Click `Deploy keys`
4. Click `Add deploy key`

![https://s2.do-spaces.com/2020/Nov/07/1604746960-175.gif](https://s2.do-spaces.com/2020/Nov/07/1604746960-175.gif)

---

### 🧪 Testing
To Test if your key is configured correctly run the below cmds 

#### Read Only Test

```bash
git clone git@github.com:{username}/{repository}.git
```
Above cmd should output something similar to below output
![https://s2.do-spaces.com/2020/Nov/07/1604747974-11.jpg](https://s2.do-spaces.com/2020/Nov/07/1604747974-11.jpg)

#### Write Test
**Navigate Into The Folder**
```bash
cd your-repository-path
```
**Configure Git identity**
```bash
git config user.email "your-github-useremail@example.com"
git config user.name "Your Name"
```
**Create A New File**
```bash
touch test-file.md
```
**Add Some Content To The File**
```bash
echo "## Hello World" >> test-file.md
```
**Add & Commit The File**
```bash
git add test-file.md
git commit -m "🎉 Successfully Pushed Using Deploy Keys"
```

**Push To Github**
```bash
git push
```

![https://s2.do-spaces.com/2020/Nov/07/1604748933-140.jpg](https://s2.do-spaces.com/2020/Nov/07/1604748933-140.jpg)

> 🎉🎉🎉 Congrats you have successfully configured the repository with SSH Deploy key 🎉🎉🎉

---

Questions or feedback?  Please comment below. 

See all my projects at <a href=https://github.com/varunsridharan/>Github</a>.

Follow me on <a href="https://twitter.com/varunsridharan2">Twitter for updates</a>