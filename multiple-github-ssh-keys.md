# How to Add Multiple GitHub SSH Keys (Work + Personal)

This guide explains how to set up **separate SSH keys** for work and personal GitHub accounts on the same machine using SSH config aliases.

---

## Step 1: Generate SSH Keys

### Personal GitHub Key

```bash
ssh-keygen -t ed25519 -C "your-personal-email@example.com"
# Save as: ~/.ssh/id_ed25519_personal
```
### Work GitHub Key

```bash
ssh-keygen -t ed25519 -C "your-work-email@example.com"
# Save as: ~/.ssh/id_ed25519_work
```

## Step 2: Add SSH Config Entries

Edit your SSH config file:
```bash
nano ~/.ssh/config
```

Add:
```bash
# Personal GitHub
Host github.com-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_personal
  IdentitiesOnly yes

# Work GitHub (default)
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_work
  IdentitiesOnly yes
```

## Step 3: Add Keys to SSH Agent

```bash
ssh-add ~/.ssh/id_ed25519_personal
ssh-add ~/.ssh/id_ed25519_work
```

## Step 5: Verify SSH Key Is Used
Test personal:
```bash
ssh -T git@github.com-personal
```

Test work:
```bash
ssh -T git@github.com
```

## How to Revert and Clean Up
1. Delete personal key files
   
```bash
rm ~/.ssh/id_ed25519_personal
rm ~/.ssh/id_ed25519_personal.pub
```

2. Remove personal entry from SSH config
   
Open `~/.ssh/config` and delete:
```ssh
# Personal GitHub
Host github.com-personal
...
```

3. Remove key from SSH agent

```bash
ssh-add -d ~/.ssh/id_ed25519_personal
# Or remove all and re-add work only:
ssh-add -D
ssh-add ~/.ssh/id_ed25519_work
```

4. Update any local repos if needed

If you used a personal remote:
```bash
git remote remove origin
# or update back to work
git remote set-url origin git@github.com:your-work-org/repo-name.git
```
