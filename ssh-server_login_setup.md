# Install and Configure - SSH Key

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

4. Configure SSH Client:  
   Add the following configuration to your SSH config file to specify the identity file and disable password authentication:
   ```
   Host *
     IdentityFile ~/.ssh/school
     PasswordAuthentication no
   ```
   - Set `PasswordAuthentication` to `no`.
   - Ensure the `IdentityFile` line points to `~/.ssh/school`.

5. Add the SSH agent and add your private key:
   ```bash
   eval "$(ssh-agent)"
   ssh-add ~/.ssh/school
   ```

6. Navigate to the `.ssh` directory and copy your public key to the `authorized_keys` file:
   ```bash
   cd ~/.ssh
   cat ./school.pub >> authorized_keys
   ```

7. Set the appropriate permissions:
   ```bash
   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/school
   chmod 644 ~/.ssh/school.pub
   chmod 600 ~/.ssh/authorized_keys
   ```

8. Connect to your server:
   ```bash
   ssh ubuntu@35.153.232.79
   ```

### 2: Connect to the Server
This script connects to your server using a specific private key.

```bash
#!/usr/bin/env bash
# Connects to my server using a specific private key
ssh -i ~/.ssh/school ubuntu@172.17.0.34
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

## Notes

- **Backup Your SSH Private Key**: 
  Always keep a backup of your private key (`~/.ssh/school`) in a secure location. Losing this key means you will not be able to access any servers where it has been used for authentication.

- **Using the Key on a New Server**:
  If you create a new server, ensure that the public key (`~/.ssh/school.pub`) is added to the `~/.ssh/authorized_keys` file of the server's user (e.g., `ubuntu`). You can do this using:
  ```bash
  cat ~/.ssh/school.pub | ssh ubuntu@NEW_SERVER_IP 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'
  ```

- **Automatic Connection After Setup**:
  After setting up your SSH config file, you can connect to your server using a simple command without specifying the key:
  ```bash
  ssh web-01
  ```
  Make sure to replace `web-01` in your `~/.ssh/config` file with the appropriate host configuration:
  ```
  Host web-01
    HostName 35.153.232.79
    User ubuntu
    IdentityFile ~/.ssh/school
  ```

- **IP Address Replacement**:
  Remember to replace `172.17.0.34` and `35.153.232.79` with your actual server IP addresses as needed.

- **Permissions**: 
  Ensure that you have the correct permissions for the private key and authorized keys for security reasons.
