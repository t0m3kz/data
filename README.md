# VyOS configuration

## Desired state files

The data repository contains files related to the VyOS device deployment described in [design document](DESIGN.md).

Inventory files:

* hosts.yml: This file contains the host information of VyOS devices to be deployed. It's a YAML file that lists the devices, their IP addresses and group assignments.
* groups.yml: This file defines groups of VyOS devices that contain common parameters like DNS/NTP settings.
* inventory.yaml: This file contains the inventory definition. It is not recommended to change the file.

Desired state files:

* s1-tr-vyos.yaml: Desired state file for VyOS device in S1 trusted network.
* s1-ntr-vyos.yaml: Desired state file for VyOS device in S1 non trusted network.
* s2-tr-vyos.yaml: Desired state file for VyOS device in S2 trusted network.
* s2-ntr-vyos.yaml: Desired state file for VyOS device in S2 non trusted network.

## Creating a New Branch and Pull Request on GitHub

1. Create a New Branch
   To create a new branch, follow these steps:

    * Go to your repository on GitHub and click on the "Code" tab.
    * Click on the "Branch" dropdown menu and select "New branch".
    * Enter a name for your new branch, following the standard naming convention (e.g., test_name or TEST_Application).
    * Click on the "Create branch" button.

    Alternatively, you can create a new branch using the command line:

    ```bash
    git checkout -b test_name
    ```

2. Make Changes and Commit
    Make the necessary changes to your desired state files and commit them to your new branch:

    ```bash
    git add .
    git commit -m "Commit message"
    ```

3. Push Your Changes
    Push your changes to the remote repository:

    ```bash
    git push origin test_name
    ```

4. Create a Pull Request
    To create a pull request, follow these steps:

    * Go to your repository on GitHub and click on the "Pull requests" tab.
    * Click on the "New pull request" button.
    * Select the branch you want to merge into (usually main or master) and the branch you want to merge from (your new branch).
    * Enter a title and description for your pull request.
    * Click on the "Create pull request" button.
5. Review and Merge
    Once your pull request is created, it will be reviewed by your team. If everything looks good, the pull request will be merged into the main branch
    and deployed on the devices.

Tips and Best Practices
Always create a new branch for new deployment.
Use descriptive branch names and commit messages.
Keep your pull requests small and focused on a single test case.
Use GitHub's built-in code review tools to review and discuss changes.

## Use cases

Each change requires new branch, desired file changes and pull request creation as described previously.

### Change/deploy gateway IPs

Edit respective desired state file and add edit one or more gateways.

```yaml
gateways:
  - vlan: 123 # VLAN ID
    gateway: 192.168.5.1/24 # Gateway IP/Mask
```

### Change/deploy NTP servers

The NTP servers can be changed in the desired state files for respective device or (recommended) in groups files.

```yaml
s1: # site name
  data:
    ntp_servers:
      - 10.254.1.1 # NTP server IP
      - 10.254.1.2 # Another NTP server IP
```
