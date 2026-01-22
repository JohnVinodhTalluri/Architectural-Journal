Perfect 👍
Below is the ready-to-use Markdown (.md) file content.

👉 You can copy-paste this exactly into a file named something like:
setup-github-ssh.md or docs/setup-github-ssh.md

⸻


# GitHub Repository Setup & SSH Authentication

## Objective
This document captures the complete steps followed to:
- Fix GitHub authentication failure caused by deprecated password-based access
- Configure SSH-based authentication on macOS
- Update Git remote from HTTPS to SSH
- Create an architecture playbook folder structure
- Commit and push changes successfully

---

## 1. Problem Faced

### Error Message

remote: Invalid username or token.
Password authentication is not supported for Git operations.
fatal: Authentication failed

### Reason
GitHub has disabled password-based authentication for Git operations over HTTPS.

Supported options:
- Personal Access Token (PAT)
- SSH-based authentication (preferred)

---

## 2. Chosen Approach: SSH Authentication

### Why SSH
- Secure and industry standard
- No repeated credential prompts
- Ideal for long-term development and architecture repositories

---

## 3. Generate SSH Key Pair

### Command Used
```bash
ssh-keygen -t ed25519 -C "thisisjohnvinodh@gmail.com"

Explanation
	•	ssh-keygen generates an SSH key pair
	•	ed25519 is a modern and secure algorithm
	•	-C adds a comment (email) for identification

Input Provided

Enter file in which to save the key: GithubLoginSSH

Files Generated
	•	GithubLoginSSH → Private key
	•	GithubLoginSSH.pub → Public key

Note: Since no path was specified, the keys were created in the current directory.

## 4. Move SSH Keys to Standard Location

Commands Used

mkdir -p ~/.ssh
mv GithubLoginSSH ~/.ssh/
mv GithubLoginSSH.pub ~/.ssh/
chmod 600 ~/.ssh/GithubLoginSSH
chmod 644 ~/.ssh/GithubLoginSSH.pub

Reason
	•	~/.ssh is the standard directory for SSH keys
	•	Private key permissions must be restricted
	•	SSH refuses keys with insecure permissions

⸻

5. Start SSH Agent and Add Key

Commands Used

eval "$(ssh-agent -s)"
ssh-add --apple-use-keychain ~/.ssh/GithubLoginSSH

Reason
	•	ssh-agent stores keys in memory
	•	--apple-use-keychain stores the passphrase in macOS Keychain
	•	Prevents repeated passphrase prompts

Verification

ssh-add -l

Expected: fingerprint of GithubLoginSSH key is listed.

⸻

6. Configure SSH for GitHub

Edit SSH Config

nano ~/.ssh/config

Configuration Added

Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/GithubLoginSSH
  AddKeysToAgent yes
  UseKeychain yes
  IdentitiesOnly yes

Reason
	•	Forces SSH to use the correct key for GitHub
	•	Avoids conflicts when multiple SSH keys exist

Secure Config File

chmod 600 ~/.ssh/config


⸻

7. Add Public Key to GitHub Account

Copy Public Key

pbcopy < ~/.ssh/GithubLoginSSH.pub

GitHub Steps
	1.	Login to GitHub account (JohnVinodhTalluri)
	2.	Go to Settings → SSH and GPG keys
	3.	Click New SSH key
	4.	Paste the copied key
	5.	Save

⸻

8. Update Git Remote from HTTPS to SSH

Check Existing Remote

git remote -v

Update Remote URL

git remote set-url origin git@github.com:JohnVinodhTalluri/Architectural-Journal.git

Verify

git remote -v


⸻

9. Test SSH Authentication

Command Used

ssh -T git@github.com

Successful Output

Hi JohnVinodhTalluri! You've successfully authenticated,
but GitHub does not provide shell access.

Meaning: SSH authentication is correctly configured.

⸻

10. Create Architecture Playbook Folder Structure

Required Structure

Architectural-Journal/
├── diagrams/
│   ├── cloud/
│   ├── kubernetes/
│   └── integration/
├── architectures/
│   ├── api-gateway-pattern.md
│   ├── async-processing.md
├── adr/
│   ├── ADR-001-sync-vs-async.md
│   ├── ADR-002-db-selection.md
└── README.md



