# Install and Configure - SSH Key for GitHub

## Description
This project provides a series of steps to create and configure an SSH key for GitHub authentication. By setting up an SSH key, you can interact with your GitHub repositories without entering your username and password every time.

## Tasks Overview

### 0: Check for Existing SSH Key
Check if you already have an SSH key by listing files in the `.ssh` directory.

```bash
#!/usr/bin/env bash
# Check if an SSH key already exists
ls -al ~/.ssh
```

### 1: Generate a New SSH Key
This script generates a new RSA SSH key pair with a specified email.

```bash
#!/usr/bin/env bash
# Generate a new RSA SSH key pair
ssh-keygen -t rsa -b 4096 -C "john.doe@gmail.com" -f ~/.ssh/id_rsa -N betty
```

### 2: Add SSH Key to the SSH Agent
Add your new SSH key to the SSH agent to manage your keys.

```bash
#!/usr/bin/env bash
# Start the SSH agent and add the private key
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

### 3: Add SSH Key to Your GitHub Account
Copy your SSH public key and add it to your GitHub account.

```bash
#!/usr/bin/env bash
# Copy the SSH public key to clipboard
cat ~/.ssh/id_rsa.pub
```

1. Go to [GitHub - SSH and GPG keys settings](https://github.com/settings/keys).
2. Click **New SSH Key**.
3. Paste the key into the "Key" field and give it a descriptive title.
4. Click **Add SSH key**.

### Task 4: Test the SSH Connection
Verify that your SSH key is properly set up by testing the connection to GitHub.

```bash
#!/usr/bin/env bash
# Test SSH connection to GitHub
ssh -T git@github.com
```

You should see a message like:
```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

### Task 5: Use SSH for Git Operations
When cloning a repository, ensure you use the SSH URL:

```bash
# Clone a repository using SSH
git clone git@github.com:username/repository.git
```

### Task 6: Set Permissions for SSH Files
Ensure your `.ssh` directory and files have the correct permissions:

```bash
#!/usr/bin/env bash
# Set correct permissions for SSH files
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
```

### Task 7: Update Remote URL to Use SSH
Check your Git remote URL and update it to use SSH if it is set to HTTPS:

```bash
# Check the current remote URL
git remote -v

# Change to SSH URL if necessary
git remote set-url origin git@github.com:username/repository.git
```

### Task 8: Generate a New SSH Key with Ed25519 (if needed)
If you encounter security issues with RSA, generate a new SSH key using Ed25519:

```bash
#!/usr/bin/env bash
# Generate a new Ed25519 SSH key
ssh-keygen -t ed25519 -C "john.doe@gmail.com" -f ~/.ssh/id_ed25519 -N betty
```
**Add SSH Key to the SSH Agent**
Add your new SSH key to the SSH agent to manage your keys.

```bash
#!/usr/bin/env bash
# Start the SSH agent and add the private key
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub
ssh -T git@github.com
```
### Task 9: Configure Git Push Behavior

When you clone a repository using the HTTPS URL, Git defaults to a push behavior called `matching`. This means that when you run `git push`, Git will attempt to push all local branches that have matching names on the remote. However, if you've set up SSH authentication later on, this can lead to confusion and warnings.

#### Why the Warning Occurs

If you initially clone a repository using HTTPS and later switch to using SSH for pushing changes, you might encounter a warning regarding the `push.default` setting. This happens because:

1. **Different Authentication Methods**: The initial clone was done using HTTPS, which requires you to enter your username and password. If you later set up SSH keys for authentication, the mismatch can lead to confusion about how Git handles your push requests.

2. **Push Behavior**: The default `matching` behavior can be problematic when your local branches don’t correspond to the remote branches. For example, if you have a local branch named `feature` but the remote only has `main`, a `git push` may not behave as expected.

#### Recommended Solution

To resolve these issues and streamline your workflow, it's advisable to set the push behavior to `simple`. This configuration ensures that:

- When you run `git push`, Git will only push the current branch to its upstream branch (the remote branch it tracks).
- If the current branch does not have an upstream branch, Git will prompt you for the correct target, making it clear what is happening.

You can configure this by running the following command:

```bash
# Set the recommended push behavior
git config --global push.default simple
```

#### Benefits of Using `simple`

1. **Clarity**: You’ll only push your current branch, reducing the risk of pushing changes to unintended branches.
2. **Ease of Use**: If no upstream branch is set, Git will inform you, allowing you to easily establish the correct connection.
3. **Streamlined Workflow**: This behavior is particularly useful when transitioning from HTTPS to SSH, as it prevents confusion and ensures your pushes are directed correctly.

By setting your push behavior to `simple`, you can avoid confusion stemming from using different authentication methods and ensure a smoother experience when pushing your changes.
## Notes
- Make sure to replace `username` and `repository` with your actual GitHub username and repository name.
- Ensure you have the correct permissions for your SSH keys to maintain security.
- If you're working with a private Git server, ensure your public key is added to the `~/.ssh/authorized_keys` file on that server.

