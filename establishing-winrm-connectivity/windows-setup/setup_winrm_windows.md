# Windows WinRM Setup for Ansible

This repository contains the necessary configuration script and documentation for setting up Windows Remote Management (WinRM) to enable Ansible automation on Windows hosts.

## Overview

WinRM is Microsoft's implementation of WS-Management Protocol, a standard SOAP-based protocol that allows hardware and operating systems from different vendors to interoperate. This repository helps you configure WinRM on Windows machines to work with Ansible.

## Prerequisites

### Windows Host Requirements
- Windows Server 2012 R2 or later
- PowerShell 3.0 or later
- Administrator access

### Ansible Control Node Requirements
- Ansible 2.10 or later
- Python 3.x
- pywinrm package
```bash
pip install pywinrm
```

## WinRM Configuration Steps

### 1. On Windows Host

1. Download the `ConfigureRemotingForAnsible.ps1` script from this repository
2. Open PowerShell as Administrator
3. Navigate to the directory containing the script
4. Run the script:
```powershell
Set-ExecutionPolicy Bypass -Scope Process
.\ConfigureRemotingForAnsible.ps1
```

The script will:
- Enable PowerShell Remoting
- Create and configure a WinRM HTTPS listener
- Generate a self-signed SSL certificate
- Configure firewall rules for WinRM HTTPS (TCP 5986)
- Enable Basic authentication (can be disabled using -DisableBasicAuth switch)

### Script Parameters

The script supports several parameters for customization:

```powershell
.\ConfigureRemotingForAnsible.ps1 [parameters]

Parameters:
-SubjectName [string]           # Certificate subject name (default: computer name)
-CertValidityDays [int]        # Certificate validity period (default: 1095 days)
-SkipNetworkProfileCheck       # Skip network profile check
-ForceNewSSLCert              # Force new SSL certificate creation
-EnableCredSSP                # Enable CredSSP authentication
-DisableBasicAuth            # Disable Basic authentication
-GlobalHttpFirewallAccess    # Configure firewall for global HTTP access
```

### 2. Testing WinRM Configuration

After running the script, you can test the WinRM configuration using:

```powershell
# Test HTTP
Test-WSMan

# Test HTTPS (requires SkipCNCheck due to self-signed cert)
Test-WSMan -UseSSL -Credential (Get-Credential)
```

### 3. Ansible Inventory Setup

Create an inventory file with your Windows host details:

```yaml
# inventory.yml
windows_hosts:
  hosts:
    win_server:
      ansible_host: your_windows_server_ip
      ansible_user: administrator
      ansible_password: your_password
      ansible_connection: winrm
      ansible_winrm_server_cert_validation: ignore
      ansible_port: 5986
      ansible_winrm_scheme: https
```

### 4. Test Ansible Connection

Test the connection using Ansible's win_ping module:

```yaml
# test_winrm.yml
---
- name: Test Windows Connectivity
  hosts: windows_hosts
  tasks:
    - name: Ping Windows Host
      win_ping:
```

Run the playbook:
```bash
ansible-playbook -i inventory.yml test_winrm.yml
```

## Troubleshooting

### Common Issues

1. **Certificate Errors**
   - Error: "The server certificate on the destination computer is invalid"
   - Solution: Add `ansible_winrm_server_cert_validation: ignore` to inventory
   
2. **Authentication Failures**
   - Error: "Authentication failed"
   - Solutions:
     - Verify credentials in inventory
     - Ensure Basic authentication is enabled
     - Check user has admin privileges

3. **Connection Timeout**
   - Error: "WinRM Connection Timeout"
   - Solutions:
     - Check firewall rules
     - Verify WinRM service is running
     - Test network connectivity

### Verification Commands

On Windows host:
```powershell
# Check WinRM service status
Get-Service WinRM

# View WinRM listeners
winrm enumerate winrm/config/Listener

# Check WinRM configuration
winrm get winrm/config
```

## Security Considerations

1. **Production Environments**
   - Replace self-signed certificates with valid certificates from trusted CA
   - Use domain authentication instead of Basic authentication
   - Implement proper firewall rules
   - Consider using Kerberos authentication

2. **Basic Authentication**
   - Basic authentication transmits credentials in base64 encoding
   - Always use HTTPS (port 5986) when using Basic authentication
   - Consider disabling Basic authentication if not needed

