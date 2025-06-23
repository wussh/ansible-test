# Windows Deployment Ansible Project

This project contains Ansible playbooks to deploy and extract a Windows application package to target Windows hosts.

## Project Overview

The project automates the deployment of a Windows application package (`win-x64.zip`) to Windows hosts and extracts it to the specified destination.

## Prerequisites

- Python 3.8 or higher
- Ansible 2.10 or higher
- WinRM configured on target Windows hosts
- Network connectivity to target Windows hosts

## Installation

1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd <project-directory>
   ```

2. Set up a Python virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install Ansible and required dependencies:
   ```bash
   pip install ansible pywinrm
   ```

## Configuration

1. Update the `inventory.ini` file with your target Windows hosts:
   ```ini
   [windows]
   your-windows-host-ip

   [windows:vars]
   ansible_user=your-username
   ansible_password=your-password
   ansible_connection=winrm
   ansible_winrm_transport=ntlm
   ansible_port=5985
   ansible_winrm_server_cert_validation=ignore
   ```

   **Note:** For security reasons, consider using Ansible Vault for storing sensitive information like passwords.

2. Place your Windows application package (`win-x64.zip`) in the project root directory.

## Usage

Run the deployment playbook with:

```bash
ansible-playbook -i inventory.ini copy-win.yml
```

This will:
1. Copy `win-x64.zip` to `C:\test\` on the target Windows hosts
2. Extract the zip file to `C:\test\win-x64\`
3. Remove the zip file after extraction

## Security Considerations

- Never commit credentials to your repository
- Use Ansible Vault to encrypt sensitive information:
  ```bash
  ansible-vault create vault.yml
  ansible-vault edit vault.yml
  ```

## Troubleshooting

- If you encounter WinRM connectivity issues, ensure WinRM is properly configured on the target hosts
- Verify the target Windows hosts are accessible from your Ansible control node
- Check firewall settings to ensure ports 5985 (HTTP) or 5986 (HTTPS) are open

## License

[Specify your license here]

## Contributing

[Specify contribution guidelines if applicable] 