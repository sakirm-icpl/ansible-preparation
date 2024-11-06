# Establishing SSH Connectivity on Linux for Ansible Ping

## Step 1: Generate SSH Keys (if you haven't already)

* Open Terminal on your Linux machine
* Run `ssh-keygen -t rsa` (accept defaults or customize as needed)

## Step 2: Copy the Public Key to Your Linux/Mac Target Machine

* `ssh-copy-id user@target_machine_ip` (or use `scp` as in the Mac instructions)
* Alternatively, manually append the public key to `~/.ssh/authorized_keys` on the target machine

## Step 3: Configure SSH on the Target Machine

* Ensure permissions are set correctly (e.g., `chmod 600 ~/.ssh/authorized_keys`)
* Restart the SSH service if necessary (e.g., `sudo systemctl restart sshd`)

## Step 4: Test SSH Connectivity

* `ssh user@target_machine_ip` (should connect without prompting for a password)