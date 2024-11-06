# Establishing SSH Connectivity on Mac for Ansible Ping

## Step 1: Generate SSH Keys (if you haven't already)

* Open Terminal on your Mac
* Run `ssh-keygen -t rsa` (accept defaults or customize as needed)

## Step 2: Copy the Public Key to Your Linux/Mac Target Machine

* `scp ~/.ssh/id_rsa.pub user@target_machine_ip:/home/user/`
* Alternatively, use a tool like `ssh-copy-id user@target_machine_ip`

## Step 3: Configure SSH on the Target Machine

* Append the public key to `~/.ssh/authorized_keys` on the target machine
* Ensure permissions are set correctly (e.g., `chmod 600 ~/.ssh/authorized_keys`)

## Step 4: Test SSH Connectivity

* `ssh user@target_machine_ip` (should connect without prompting for a password)