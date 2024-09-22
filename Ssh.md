# Install And Configure - SSH Key

## Description
This project provides a series of bash scripts and configuration tasks to set up SSH connections to a server using a specific private key. The goal is to ensure secure and password-less authentication.

## Tasks Overview

### 0: Create an RSA Key Pair
This script generates an RSA key pair named 'school' with 4096 bits and a passphrase 'betty'.

```bash
#!/usr/bin/env bash
# Creates an RSA key pair named 'school' with 4096 bits and a passphrase 'betty'
ssh-keygen -t rsa -b 4096 -f ~/.ssh/school -N betty
```

### 1: Configure SSH Client

Update SSH Configuration:
1. Change directory to `/etc`:
   ```bash
   cd /etc
   ```
2. Navigate to the `ssh` directory:
   ```bash
   cd ssh/
   ```
3. Open the `ssh_config` file for editing:
   ```bash
   sudo vi ssh_config
   ```

4. Configure SSH Client
Add the following configuration to your SSH config file to specify the identity file and disable password authentication.
```
Host *
  IdentityFile ~/.ssh/school
  PasswordAuthentication no
  ```
   - Change `PasswordAuthentication` to `no`.
   - Change the first `IdentityFile` line to use `~/.ssh/school`.

5. Add the SSH agent and add your private key:
   ```bash
   eval "$(ssh-agent)"
   ssh-add ~/.ssh/school
   ```
6. Connect to your server:
   ```bash
   ssh ubuntu@35.153.232.79
   ```
7. Once logged in, navigate to the `.ssh` directory and copy your public key to the `authorized_keys` file:
   ```bash
   cd ~/.ssh
   cat ../school.pub >> authorized_keys
   ```

8. Set the appropriate permissions:
   ```bash
   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/school
   chmod 644 ~/.ssh/school.pub
   chmod 600 ~/.ssh/authorized_keys
   ```

### 3: Puppet Manifest to Configure SSH Client
Use the following Puppet manifest to configure the SSH client:

```puppet
file_line { 'Turn off password authentication':
  path  => '/etc/ssh/ssh_config',
  line  => 'PasswordAuthentication no',
  match => '^#PasswordAuthentication',
}

file_line { 'Use the private key':
  path  => '/etc/ssh/ssh_config',
  line  => 'IdentityFile ~/.ssh/school',
  match => '^#IdentityFile',
}
```

### Task 0: Connect to the Server
This script connects to your server using a specific private key.

```bash
#!/usr/bin/env bash
# Connects to my server using a specific private key
ssh -i ~/.ssh/school ubuntu@172.17.0.34
```
## Notes
- Remember to replace `172.17.0.34` and `35.153.232.79` with your actual server IP addresses as needed.
- Ensure that you have the correct permissions for the private key and authorized keys for security reasons.
