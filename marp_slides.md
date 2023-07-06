---
marp: true
theme: default
class: invert
author: Petr Ankudinov
# size 16:9 1280px 720px
size: 16:9
paginate: true
math: mathjax
# backgroundImage: "linear-gradient(to bottom, #1e3744, #301B29)"
style: |
    :root {
      background: linear-gradient(to bottom, #1e3744, #301B29);
    }
    img[alt~="custom"] {
      float: right;
    }
    .columns {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 1rem;
    }
    footer {
      font-family: Brush Script MT;
      font-size: 14px;
    }
    section::after {
      font-family: Brush Script MT;
      font-size: 14px;
    }
---

# AVD Extended Workshop

<!-- Do not add page number on this slide -->
<!--
_paginate: false
-->

<style scoped>
code {
  font-family: "Bradley Hand", cursive;
}
</style>

```Intro into Ansible, Ansible AVD, Git and VSCode for new and existing AVD users```

![bg left fit](img/avd-logo.webp)

---

# What is this Workshop about?

<!-- Add footer starting from this slide -->
<!--
footer: 'Arista Ansible AVD Extended Workshop, 2023'
-->

<style scoped>section {font-size: 14px;}</style>

![bg right](img/pexels-suzy-hazelwood-1226398.jpg)

- This workshop is split into 3 sections. Each section takes around 2 hours to complete. That can be done as a full day workshop or split into 3 separate sessions.
- Topics:

  > - Section 1 - Intro:
  >   - Introducing the Tools
  >   - Before We Start - get lab environment up and running
  >   - How to setup Ansible AVD in Arista Test Drive environment
  >   - Prepare Github Codespaces Environment
  >   - Run AVD Playbooks
  >   - Make Some Changes in AVD Repository
  > - Section 2 - Ansible and Git 101:
  >   - `Under construction`
  > - Section 3 - Common AVD provisioning cases:
  >   - `Under construction`

- Make a break when you see a slide with a coffee cup ☕️
- Ask questions at any time!

---

# What is NOT covered in this Workshop?

<style scoped>section {font-size: 22px;}</style>

- This workshop is not a deep dive into each and every topic. It is covering some advanced concepts, but you may need additional documentation and training to understand every topic in details.  
  For additional information please refer to the following resources:
  - [Ansible AVD Documentation](https://avd.arista.com/)
  - [VSCode Documentation](https://code.visualstudio.com/docs)
  - [Git Documentation](https://git-scm.com/doc) - Pro Git book is a good start
  - Container Trainings by [@jpetazzo](https://github.com/jpetazzo):
    - [Github repository](https://github.com/jpetazzo/container.training)
    - [Training materials](https://container.training/)
- We are not going to use Arista CloudVision Portal (CVP) in this workshop. It provides a lot of advantages, but is not essential to understand the concepts covered in this workshop.
- If you will not find something you expect in this workshop, there can be 2 reasons:
  - It is not covered in this workshop
  - It is waiting for your contribution to this repository! 🤝

---

# Requirements

<style scoped>section {font-size: 24px;}</style>

- You **MUST** have a Github account❗
  Register [here](https://github.com/join).

![bg left](img/pexels-towfiqu-barbhuiya-11412596.jpg)

---

# References

<style scoped>section {font-size: 22px;}</style>

- If you are not using ATD, the functionality of this repository will rely on many amazing open source projects:
  - [ContainerLab](https://containerlab.srlinux.dev/)
  - [VSCode](https://code.visualstudio.com/)
  - [DevContainers](https://code.visualstudio.com/docs/remote/containers)
  - [Marp](https://marp.app/)
  - [Excalidraw VSCode](https://github.com/excalidraw/excalidraw-vscode)
- This repository is also relying on following free/commercial Github features:
  - [Github Actions](https://github.com/features/actions)
  - [Github Pages](https://pages.github.com/)
  - [Github Codespaces](https://github.com/features/codespaces)
- All photos are taken from [Pexels](https://www.pexels.com/) and [Unsplash](https://unsplash.com/). Excellent free stock photos resources. It's not possible to reference every author individually, but their work is highly appreciated.

---

# Introducing The Tools

<style scoped>
section {background: linear-gradient(to bottom, #000000, #434343);}
ul {font-size: 12px;}
</style>

![bg left](img/pexels-pixabay-159591.jpg)

`Section 1.1`

> - The bird view on the tools we are going to use in this workshop.
> - No details, they will come in a later sections. Just and overview.

---

# What is Git?

![bg right fit](img/Git-Logo-1788C.png)

- **In Short**:
  > Git is a distributed version control system that tracks changes to a set of files and enables collaborative work.
- **Fun Fact**:
  > [Git was created](https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git) by Linus Torvalds in 2005 to develop Linux kernel.

---

# What is GitHub?

![bg right fit](img/github-mark-white.png)

- GitHub is a Git repository hosting platform.
- Allows to coordinate multiple local copies of the same repository and more.

---

# VSCode

<style scoped>section {font-size: 24px;}</style>

![bg right fit](img/code-stable.png)

- Visual Studio Code is an extensible source-code editor developed by Microsoft and free to use.
- This will be our main tool to work with Ansible AVD and interact with Git repositories in the workshop and production.
- We are not going to cover VSCode installation and customization in this workshop. Check [VSCode documentation](https://code.visualstudio.com/docs) for details.

---

# Before We Start

<style scoped>
section {background: linear-gradient(to bottom, #000000, #434343);}
ul {font-size: 12px;}
</style>

![bg left](img/pexels-pixabay-159591.jpg)

`Section 1.2`

> - How to get your lab environment up and running

---

# How to use this Workshop?

<style scoped>section {font-size: 24px;}</style>

- To try all practical examples you need to have access to the lab environment. There are 3 possible options:
  - Use Github Codespaces. This is the preferred option, but double check that you understand all the costs and free tier limits.
  - Use Arista Test Drive - Single DC topology. Please ask your Arista SE to create an ATD lab for you.
  - Build your own lab environment: Ubuntu LTS + Docker + ContainerLab. This option is not described in detail, but the devcontainer used to build Codespaces environment will work on any machine with Docker installed. Please contact your SE if you need help.

---

# Lab Topology

<style scoped>section {font-size: 22px;}</style>

- This workshop is using Arista Test Drive Single DC topology.
- To match minimize resources and fit default Codespaces 4-core machine, the topology was reduced by removing leaf3, leaf4, host1 and host2.
- Feel free to adjust Ansible inventory and group variables if you are using ATD lab and would prefer to activate them all. But it's not essential for this workshop.
- CVP is not used as it's not required for this workshop.

![bg right fit](img/atd-topo.png)

---

# Github Repository Import

<style scoped>section {font-size: 24px;}</style>

![bg vertical right fit](img/import-github-repository.png)
![bg right width 640](img/pexels-realtoughcandycom-11035544.jpg)

- Create a copy of this repository on your Github account. That will allow you to make any changes without impacting the original repository.
- Alternatively you can fork this repository, but in this case you must **NOT** (❕) open any pull requests to the original repository.
- To make a copy of the repository click ➕ button in the top right corner of the Github page and select `Import repository` option.

---

# Github Repository Import, Step 2

<style scoped>section {font-size: 20px;}</style>

![bg right fit](img/import-github-repository-step-2.png)

- Enter the following URL in `Your Old Repository's Clone URL` field:
  - `https://github.com/arista-netdevops-community/avd-extended-workshop`
- Use your own account in `Owner` field and `avd-extended-workshop` or another name in the `Repository Name` field.
- Create `Public` repository. That will simplify interaction with this repo and allow use of Github free features.
- Wait until the import is completed.
- Your clone will now be referenced as `<your-copy-of-this-repository>` in this workshop.

---

# Github Repository Import, Step 3

<style scoped>section {font-size: 20px;}</style>

![bg right fit](img/import-github-change-default-branch.png)

- Confirm that `main` is the default Git branch after the import.
- Click `Settings` tab in the top right corner of the Github page.
- Click `General` on the left panel.
- Scroll down to `Default branch` section, click `Switch to another branch` button and select `main` branch.
- All set! 🎉

---

# How to Setup ATD Environment

<style scoped>
section {background: linear-gradient(to bottom, #000000, #434343);}
ul {font-size: 12px;}
</style>

![bg left](img/pexels-pixabay-159591.jpg)

`Section 1.3`

> - skip hands on in this section if you are using Codespaces
> - still read the slides as they explain AVD installation process

---

# How to setup Ansible AVD in Arista Test Drive environment?

- We could use a script to setup required Ansible collections and tools in Arista Test Drive environment, but it's a good opportunity to discuss what are the requirements but installing them manually.
- For details please check [AVD documentation](https://avd.arista.com/) `Installation > Collection Installation` section.

---

# Open Programmability IDE

<style scoped>section {font-size: 20px;}</style>

![bg vertical right width:640px](img/atd-access-lab-topology.png)
![bg right width:640px](img/atd-click-programmability-ide.jpg)
![bg right width:640px](img/atd-coder-password.png)

- Use the lab token provided by Arista representative to access the lab environment.
- Check the status of the lab environment. If it's `Shutdown` - click `Start` button.
- Click `Programmability IDE` button to open VSCode in the browser:
  - To access `Programmability IDE` use the password listed on the starting Web page.
  - The VSCode functionality in the Web browser is provided by [ATD Code server container](https://github.com/aristanetworks/atd-public/blob/nested-release/nested-labvm/atd-docker/coder/Dockerfile)
- Click `Yes, I trust the authors` button to continue. 🕵️
- Open new terminal in VSCode: `Top Left Corner (3 parallel lines) > Terminal > New Terminal`

---

# Install Ansible AVD

<style scoped>section {font-size: 20px;}</style>

```bash

# 1. Update package index files
sudo apt-get update

# 2. Install iputils as life is hard without ping
sudo apt-get install -y --no-install-recommends iputils-ping

# 3. Add .local/bin in home folder to PATH
export PATH=$PATH:/home/coder/.local/bin

# 4. Upgrade pip and install Ansible core
#    If you get errors, ignore. This bug will be fixed soon.
pip install --upgrade pip
pip3 install "ansible-core>=2.13.1,<2.14.0"

# 5. Install Arista AVD collection
ansible-galaxy collection install arista.avd:==4.1.0

# 6. Install AVD collection requirements
pip3 install -r /home/coder/.ansible/collections/ansible_collections/arista/avd/requirements.txt
```

For additional details check Arista Ansible AVD [Collection installation docs](https://avd.arista.com/4.1/docs/installation/collection-installation.html).

---

# Ansible Installation Warnings

<style scoped>section {font-size: 20px;}</style>

![bg right](img/pexels-danne-555709.jpg)

- Double check that the path to Ansible collection is correct. Normally it is expected to be in `/home/coder/.ansible/`
- You `PATH` environment variable must be set correctly!
- Never install Ansible as root user!
- Watch out for environments with a long history, conflicting Python installations etc.
- Containers make it simple! Use containers! 🐳
  > The Codespaces environment is based on a container with all requirements installed.

---

# Setup Ansible AVD Repository

<style scoped>section {font-size: 20px;}</style>

```bash
# 1. install yq to adjust AVD yaml files - https://github.com/mikefarah/yq
#    you can certainly edit yaml files manually, but there would be no fun 👎
export VERSION="v4.34.1" BINARY="yq_linux_amd64"
sudo wget https://github.com/mikefarah/yq/releases/download/$VERSION/$BINARY -O /usr/bin/yq \
    && sudo chmod +x /usr/bin/yq
# 2. Clone your copy of this repository
cd labfiles
git clone https://github.com/<gh-handle>/<your-copy-of-this-repository>.git avd-extended-workshop
# 3. switch to the repository directory
cd avd-extended-workshop
# 4. confirm that you are working with the `main` branch
#    if not, type following command to change the branch
git checkout main
#    you should see the following prompt
➜  avd-extended-workshop git:(main)
# 5. update ansible.cfg to match ATD container user
cp extras/ansible-avd.cfg avd_inventory/ansible.cfg
# 6. set Ansible password to your AVD environment password
yq -i '.all.vars.ansible_password = "<your-password>"' avd_inventory/inventory.yml
```

---

# Commit Changes to Git

<style scoped>section {font-size: 26px;}</style>

![bg right fit](img/commit-atd-passwd-changes.png)

- Click VSCode `Source Control` icon in the left panel.
- Click `+` button to stage all changes. Alternatively you can accept VSCode suggestion to do that automatically every time by selecting `Always` option.
- Enter a *meaningful* commit message in the `Message` field.
- Click `Commit` button.

---

# Prepare Github Codespaces Environment

<style scoped>
section {background: linear-gradient(to bottom, #000000, #434343);}
ul {font-size: 12px;}
</style>

![bg left](img/pexels-pixabay-159591.jpg)

`Section 1.4`

> - you can skip this section if you are using ATD lab
> - still read the slides as they explain how to use Codespaces

---

# Before You Create Codespaces Environment

<style scoped>section {font-size: 20px;}</style>

![bg right fit](img/github-billing.png)

- Codespaces is a paid feature. Please check [Github Codespaces pricing](https://docs.github.com/en/billing/managing-billing-for-github-codespaces/about-billing-for-github-codespaces)
- It has a free tier for personal accounts:
  - 120 core-hours per month -> will be 30 hours on a 4-core machine
  - 15 GB storage per month -> this will be a bottleneck for the workshop container image
- The free tier is enough to complete this workshop, but don't forget to delete the Codespaces environment after the workshop.
- Check `your account > Settings > Billing and plans > Spending limits` to make sure that if you exceed the limit, there will be no charges. The default limit of `0.00` will avoid any extra expenses.

---

# Start a Codespace

<style scoped>section {font-size: 20px;}</style>

![bg right](img/start-codespaces.jpg)

- Click `Code` button in the top right corner of the Github page.
- Click `Create codespace on main` button.
- Wait until the codespace environment is created.
- Once codespace container is ready the VSCode will open automatically in your browser.

> WARNING❕:
>
> - Check `paid for by` field and make sure that you are using your personal account. If you are using a company account, you may be charged for the Codespaces usage. Also double-check previous slide and make sure that you understand the costs and limits.
> - Do not use pre-builds. They consume storage across regions and can quickly exceed the free tier limit.

---

# Open Existing Codespace

<style scoped>section {font-size: 20px;}</style>

![bg right fit](img/codespaces-open-in.jpg)

- Once the Codespace is created, you can open it again by clicking `Code` button in the top right corner of the Github page and clicking 3 dots next to codespace name.
- Alternatively you can open it from the [Github Codespaces page](https://github.com/codespaces)
- If you have VSCode installed locally, pick `Open in Visual Studio Code` option. Otherwise use `Open in browser` option. The codespace container will always run remotely.

> WARNING❕: Do not forget to delete the Codespace after the workshop.

---

# Using Codespaces Container

<style scoped>section {font-size: 22px;}</style>

<div class="columns">
<div>

- Codespaces container is ready to use.
- All required tools and dependencies are already installed. Check `ansible-galaxy collection list` output to confirm.
- Nevertheless:
  - The ContainerLab topology must be started and stopped manually.
  - cLab requires cEOS image to be uploaded first.

</div>
<div>

```zsh
👋 Welcome to Codespaces! You are on a custom image defined in your devcontainer.json file.

🔍 To explore VS Code to its fullest, search using the Command Palette (Cmd/Ctrl + Shift + P)

📝 Edit away, then run your build command to see your code running in the browser.
@ankudinov ➜ /workspaces/temp-repo (main) $ ansible-galaxy collection list

# /home/vscode/.ansible/collections/ansible_collections
Collection        Version
----------------- -------
ansible.netcommon 5.1.1  
ansible.utils     2.10.3 
arista.avd        4.1.0  
arista.cvp        3.6.1  
arista.eos        6.0.1 
@ankudinov ➜ /workspaces/temp-repo (main) $ clab version

                           _                   _       _     
                 _        (_)                 | |     | |    
 ____ ___  ____ | |_  ____ _ ____   ____  ____| | ____| | _  
/ ___) _ \|  _ \|  _)/ _  | |  _ \ / _  )/ ___) |/ _  | || \ 
( (__| |_|| | | | |_( ( | | | | | ( (/ /| |   | ( ( | | |_) )
\____)___/|_| |_|\___)_||_|_|_| |_|\____)_|   |_|\_||_|____/ 

    version: 0.37.1
     commit: 570cd7af
       date: 2023-02-24T11:35:35Z
     source: https://github.com/srl-labs/containerlab
 rel. notes: https://containerlab.dev/rn/0.37/#0371
```

</div>
</div>

---

# Uploading cEOS Image

<style scoped>section {font-size: 20px;}</style>

<div class="columns">
<div>

- The cEOS image is not included in the Codespaces container and must be uploaded manually.
- 1st, download the image from [Arista Software Download Center](https://www.arista.com/en/support/software-download). Go to cEOS-lab section and download the image. Latest 4.29 image is recommended.
- To upload the image to the Codespaces container [GitHub CLI](https://cli.github.com/) must be used:
  - To install GitHub CLI go to: `https://cli.github.com/`
  - Check [GH CLI installation instructions](https://github.com/cli/cli#installation) for additional details.
- GitHub CLI allows you to control your Github account from the command line. Including Github Codespaces.

</div>
<div>

```zsh
╭─pa@pa ~
╰─$ gh codespace --help
Connect to and manage codespaces

USAGE
  gh codespace [flags]

AVAILABLE COMMANDS
  code:        Open a codespace in Visual Studio Code
  cp:          Copy files between local and remote file systems
  create:      Create a codespace
  delete:      Delete codespaces
  edit:        Edit a codespace
  jupyter:     Open a codespace in JupyterLab
  list:        List codespaces
  logs:        Access codespace logs
  ports:       List ports in a codespace
  rebuild:     Rebuild a codespace
  ssh:         SSH into a codespace
  stop:        Stop a running codespace
  view:        View details about a codespace

INHERITED FLAGS
  --help   Show help for command

LEARN MORE
  Use 'gh <command> <subcommand> --help' for more information about a command.
  Read the manual at https://cli.github.com/manual
```

</div>
</div>

---

# Configure GitHub CLI

```bash
# 1. Follow https://github.com/cli/cli#installation instructions to install GH CLI
# 2. Authenticate with GH CLI
gh auth login
#    Select `GitHub.com` option and pick `Login with a web browser`
#    Follow the instructions to login to your Github account
# 3. Authenticate with Codespaces
gh auth refresh -h github.com -s codespace
# follow the instructions
# 4. Check that you can access Codespaces
gh codespace list
# 5. Confirm that you can SSH to your codespace
gh codespace ssh
#    Pick the codespace you want to connect to
# 6. While connected to the codespace via SSH create a directory to upload cEOS image
#    The directory name must be listed in .gitignore to avoid committing the image to the repository
<your-codespace-in-ssh> (main) $ mkdir .gitignored
# 7. Exit SSH session
<your-codespace-in-ssh> (main) $ exit
# 8. Upload cEOS image to the Codespaces container
gh codespace cp <path-to-ceos-image> -c <your-codespace-name> remote:/workspaces/avd-extended-workshop/.gitignored
```

---

# Import cEOS Image and Start cLab Topology

- Open VSCode terminal and run the following command to import cEOS-lab image: `docker import .gitignored/<ceos-image-name> ceos-lab:latest`
- Start cLab topology: `make start`
- To stop the lab use `make stop` at any time.
- If codespace is deactivated by timeout - redeploy the lab.

```bash
@ankudinov ➜ /workspaces/temp-repo (main) $ sudo clab inspect -t clab/topology.clab.yml 
INFO[0000] Parsing & checking topology file: topology.clab.yml 
+---+----------------------------+--------------+-----------------+------+---------+-----------------+--------------+
| # |            Name            | Container ID |      Image      | Kind |  State  |  IPv4 Address   | IPv6 Address |
+---+----------------------------+--------------+-----------------+------+---------+-----------------+--------------+
| 1 | clab-simple-avd-lab-leaf1  | dc2a660f739b | ceos-lab:latest | ceos | running | 192.168.0.12/24 | N/A          |
| 2 | clab-simple-avd-lab-leaf2  | 08768ea19617 | ceos-lab:latest | ceos | running | 192.168.0.13/24 | N/A          |
| 3 | clab-simple-avd-lab-spine1 | 79bf7978a336 | ceos-lab:latest | ceos | running | 192.168.0.10/24 | N/A          |
| 4 | clab-simple-avd-lab-spine2 | 45855e4687d6 | ceos-lab:latest | ceos | running | 192.168.0.11/24 | N/A          |
+---+----------------------------+--------------+-----------------+------+---------+-----------------+--------------+
```

---

# Use The Local VSCode and Dev Container

<style scoped>section {font-size: 20px;}</style>

![bg right fit](img/architecture-containers.png)

- It's possible to run exactly the same container locally on a machine with Docker installed and use local VSCode Remote Containers feature to connect to it.
- Obviously there are no charges for this option. It's completely free, except the electricity bill.
- It is not covered in this workshop for one single reason: there are too many different environments and it's impossible to cover them all.
- Check [VSCode Dev Containers documentation](https://code.visualstudio.com/docs/devcontainers/containers) for details.

---

# Coffee Break ☕️

![bg left](img/pexels-valeriia-miller-3020919.jpg)

`5 min`

---

# Run AVD Playbooks

<style scoped>
section {background: linear-gradient(to bottom, #000000, #434343);}
ul {font-size: 12px;}
</style>

![bg left](img/pexels-pixabay-159591.jpg)

`Section 1.5`

> - Just build an EVPN network with Ansible AVD and enjoy the result!

---

# What is Ansible AVD?

<style scoped>section {font-size: 22px;}</style>

- AVD stands for Arista Validated Design
- Documentation is available at [avd.arista.com](https://avd.arista.com/)
- Historically it is based on the [EVPN Deployment Guide](https://www.arista.com/custom_data/downloads/?f=/support/download/DesignGuides/EVPN_Deployment_Guide.pdf), but now it's much more advanced and developing fast.
- Ansible AVD repository is available here: [github.com/aristanetworks/ansible-avd](https://github.com/aristanetworks/ansible-avd)
- The Ansible AVD collection is relying on:
  - [EOS foundational modules](https://galaxy.ansible.com/arista/eos) maintained by RedHat: `ansible-galaxy collection install arista.eos`
  - [Ansible CVP modules](https://github.com/aristanetworks/ansible-cvp) to interact with CloudVision Portal when required

---

# Typical Ansible AVD Automation Workflow

<style scoped>section {font-size: 22px;}</style>

<div class="columns">
<div>

- Collect user input from various data sources and aggregate in a single source of truth. For ex. git repository.
- Generate low level variables from abstracted input data using sophisticated fabric logic
- Parse Jinja2 templates to produce plain text configs
- Push plain text configs via CloudVision Portal as change-control "proxy" or directly to devices via eAPI.

</div>
<div>

![ ](excalidraw/provisioning-building-blocks.png)

</div>
</div>

---

# AVD Collection Structure

<style scoped>section {font-size: 20px;}</style>

- Ansible AVD consists of the following key roles:
  - `eos_designs` - an set of modules to produce low level variables from abstracted input data using sophisticated fabric logic
  - `eos_cli_config_gen` - generate Arista EOS cli configuration from a set of templates and variables produced by `eos_designs` role
  - `eos_validate_state` - validate operational state of Arista EOS devices
  - `cvp_configlet_upload` - upload configlets to CloudVision Portal
  - `eos_configlet_deploy_cvp` - deploy configlets to Arista EOS devices via CloudVision Portal

---

# Run Ansible AVD Playbooks

<style scoped>section {font-size: 20px;}</style>

```bash
# 1. switch to AVD inventory directory
#    on ATD:
cd ~/project/labfiles/avd-extended-workshop/avd_inventory
#    on Codespaces:
cd /workspaces/avd-extended-workshop/avd_inventory
# 2. run ansible-playbook to generate configs
#    wait until the playbook will finish execution and check the configs in avd_inventory/intended/configs
ansible-playbook playbooks/atd-fabric-build.yml
# 3. run ansible-playbook to push configs to devices
ansible-playbook playbooks/atd-fabric-provision-eapi.yml
# 4. Done! 🎉 Click on on any lab switch and check `show bgp evpn summary`
```

Playbook execution example:

```zsh
➜  avd_inventory git:(main) ✗ ansible-playbook playbooks/atd-fabric-provision-eapi.yml 

PLAY [Deploy Configs] ***************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************

TASK [arista.avd.eos_config_deploy_eapi : Verify Requirements] **********************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************
AVD version 4.1.0
Use -v for details.
ok: [spine1 -> localhost]

TASK [arista.avd.eos_config_deploy_eapi : Create required output directories if not present] ****************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************
changed: [spine1 -> localhost] => (item=/home/coder/project/labfiles/avd-extended-workshop/avd_inventory/config_backup)
ok: [spine1 -> localhost] => (item=/home/coder/project/labfiles/avd-extended-workshop/avd_inventory/config_backup)

TASK [arista.avd.eos_config_deploy_eapi : Replace configuration with intended configuration] ****************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************
[WARNING]: To ensure idempotency and correct diff the input configuration lines should be similar to how they appear if present in the running configuration on device including the indentation
changed: [spine1]
changed: [spine2]
changed: [leaf1]
changed: [leaf2]

RUNNING HANDLER [arista.avd.eos_config_deploy_eapi : Backup running config] *********************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************
changed: [spine1]
changed: [spine2]
changed: [leaf1]
changed: [leaf2]

PLAY RECAP **************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************
leaf1                      : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
leaf2                      : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
spine1                     : ok=4    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
spine2                     : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

---

# Useful eAPI Troubleshooting Trick

If you are facing any issues when to push configs or collect any data using eAPI, test access with the following command:

```bash
curl --user <login>:<password> --data "show version" --insecure https://<switch-mgmt-ip>:443/command-api --verbose
```

Try it now! 🔨
With `--verbose` it can tell you a lot.

---

# Make Some Changes in AVD Repository

<style scoped>
section {background: linear-gradient(to bottom, #000000, #434343);}
ul {font-size: 12px;}
</style>

![bg left](img/pexels-pixabay-159591.jpg)

`Section 1.6`

> - Change underlay routing protocol
> - Add new tenant
> - Filter VLANs
> - Connect endpoints
> - Validate the network

---

# Change Underlay Routing Protocol to OSPF

- Go to `avd_inventory/group_vars/ATD_FABRIC.yml` and uncomment following line:

  ```yaml
  underlay_routing_protocol: ospf
  ```

- Run `ansible-playbook playbooks/atd-fabric-build.yml` to generate new configs.
- Click `Source Control` icon on the left panel and check the diffs.
- Commit you change with a meaningful commit message.
- (Optional): Run `ansible-playbook playbooks/atd-fabric-provision-eapi.yml` to push the new configs to the lab switches.

---

# Add New Tenant

<style scoped>section {font-size: 20px;}</style>
<style scoped>code {font-size: 14px;}</style>

<div class="columns">
<div>

- The `Tenant` in AVD is an abstraction combining a set of VRFs, VLANs and SVIs to be created on a set of switches.
- Open `avd_inventory/group_vars/ATD_TENANTS_NETWORKS.yml` and uncomment the lines related to `Tenant_B`
- Run `ansible-playbook playbooks/atd-fabric-build.yml` to generate new configs.
- This will generate required EVPN configs for the new VRF, VLANs and SVIs.
- Click `Source Control` icon on the left panel and check the diffs.
- Commit you change with a meaningful commit message.
- (Optional): Run `ansible-playbook playbooks/atd-fabric-provision-eapi.yml` to push the new configs to the lab switches.

</div>
<div>

```yaml
tenants:
  # Tenant_A data will be present above Tenant_B
  # keep it unchanged
  - name: Tenant_B
    mac_vrf_vni_base: 20000
    vrfs:
      - name: Tenant_B_OP_Zone
        vrf_vni: 20
        svis:
          - id: 210
            name: Tenant_B_OP_Zone_1
            tags: ['opzone']
            profile: WITH_NO_MTU
            ip_address_virtual: 10.2.10.1/24
          - id: 211
            name: Tenant_B_OP_Zone_2
            tags: ['opzone']
            profile: GENERIC_FULL
            ip_address_virtual: 10.2.11.1/24
```

</div>
</div>

---

# Filter VLANs Deployed

<style scoped>section {font-size: 20px;}</style>

- Currently all VLANs listed in `AVD_TENANTS_NETWORKS.yml` are deployed on the switches even if there are no client-facing interfaces configured for those VLANs.
- To filter out unused VLANs, open `avd_inventory/group_vars/ATD_FABRIC.yml` and uncomment the following line:

  ```yaml
  l3leaf:
    defaults:
      # ... other defaults
      # keep all the lines above unchanged
      # ...
      filter:
        only_vlans_in_use: true
  ```

- Run `ansible-playbook playbooks/atd-fabric-build.yml` to generate new configs.
- Click `Source Control` icon on the left panel and check the diffs.
- Commit you change with a meaningful commit message.
- (Optional): Run `ansible-playbook playbooks/atd-fabric-provision-eapi.yml` to push the new configs to the lab switches.

---

# Change The Port Configuration

<style scoped>section {font-size: 20px;}</style>
<style scoped>code {font-size: 14px;}</style>

<div class="columns">
<div>

- Currently ports to `host1` are configured as access ports in VLAN110.
- Let's change that to a trunk with VLANs 110 and 160 allowed.
- Open `avd_inventory/group_vars/ATD_SERVERS.yml` and add a new port profile. The change is shown on the right.
- Run `ansible-playbook playbooks/atd-fabric-build.yml` to generate new configs.
- Click `Source Control` icon on the left panel and check the diffs.
- Commit you change with a meaningful commit message.
- (Optional): Run `ansible-playbook playbooks/atd-fabric-provision-eapi.yml` to push the new configs to the lab switches.

</div>
<div>

```diff
vscode ➜ /workspaces/avd-extended-workshop/avd_inventory (main) $ git diff
diff --git a/avd_inventory/group_vars/ATD_SERVERS.yml b/avd_inventory/group_vars/ATD_SERVERS.yml
index 6bc1f49..00a6625 100644
--- a/avd_inventory/group_vars/ATD_SERVERS.yml
+++ b/avd_inventory/group_vars/ATD_SERVERS.yml
@@ -3,6 +3,9 @@ port_profiles:
   - profile: TENANT_A
     mode: access
     vlans: "110"
+  - profile: TENANT_A_TRUNK
+    mode: trunk
+    vlans: "110, 160"
 
 
 servers:
@@ -12,7 +15,7 @@ servers:
       - endpoint_ports: [Eth1, Eth2, Eth3, Eth4]
         switch_ports: [Ethernet4, Ethernet5, Ethernet4, Ethernet5]
         switches: [leaf1,leaf1, leaf2, leaf2]
-        profile: TENANT_A
+        profile: TENANT_A_TRUNK
         port_channel:
           description: PortChannel
           mode: active
(END)
```

</div>
</div>

---

# Validate The Network

<style scoped>section {font-size: 24px;}</style>

- To confirm that network state is correct use AVD network validation role.
- 1st, make sure that you have generated the latest configs and pushed them to the switches:

  ```bash
  ansible-playbook playbooks/atd-fabric-build.yml
  ansible-playbook playbooks/atd-fabric-provision-eapi.yml
  ```

- Run the following command to validate the network state:

  ```bash
  ansible-playbook playbooks/atd-validate-state.yml
  ```

- The validate role has some limitations that are quite critical when building a CI pipeline. But there is some work in progress. For example, check [ANTA library](https://github.com/arista-netdevops-community/anta) for an alternative solution.

---

# End of Section 1

<style scoped>
section {background: linear-gradient(to bottom, #000000, #434343);}
ul {font-size: 12px;}
</style>

![bg left](img/pexels-ann-h-7186206.jpg)

`Questions?`

> - To-be-continued

---

# YAML

<style scoped>
section {background: linear-gradient(to bottom, #000000, #434343);}
ul {font-size: 12px;}
</style>

![bg left](img/pexels-pixabay-159591.jpg)

`Section 2.1`

> - What is YAML?

---

# What is YAML?

<style scoped>section {font-size: 20px;}</style>
<style scoped>code {font-size: 10px;}</style>

<div class="columns">
<div>

- YAML is a data serialization language.
- It is not the only one. There are many others: JSON, XML, TOML, INI, CSV etc.
- Purpose:
  > convert data to a machine-readable format that can be stored or transmitted.
- YAML is generally considered to be a human-readable format. Well, kind of. 🤓 But at least it's possible to add comments, which is not possible in JSON.
- YAML is the default format to write Ansible playbooks, inventory files and group/host variables.

</div>
<div>

The playbook used to generate configs for this workshop in YAML format:

```yaml

```yaml
---
- name: Manage Arista EOS EVPN/VXLAN Configuration
  hosts: ATD_FABRIC
  connection: local
  gather_facts: false
  collections:
    - arista.avd
  vars:
    fabric_dir_name: "{{fabric_name}}"
    execute_tasks: false
  tasks:

    - name: Generate intended variables
      import_role:
        name: eos_designs

    - name: Generate device intended config and documentation
      import_role:
        name: eos_cli_config_gen
```

</div>
</div>

---

# JSON and XML Examples

<style scoped>section {font-size: 20px;}</style>
<style scoped>code {font-size: 10px;}</style>

<div class="columns">
<div>

ATD KVM virtual machine specification in XML:

```xml
arista@devbox:~$ sudo virsh dumpxml cvp1
setlocale: No such file or directory
<domain type='kvm' id='1'>
  <name>cvp1</name>
  <uuid>4675315f-0b93-4798-8598-37d876666df9</uuid>
  <memory unit='KiB'>33554432</memory>
  <currentMemory unit='KiB'>33554432</currentMemory>
  <vcpu placement='static'>24</vcpu>
  <resource>
    <partition>/machine</partition>
  </resource>
  <os>
    <type arch='x86_64' machine='pc-i440fx-rhel7.0.0'>hvm</type>
    <boot dev='hd'/>
  </os>
...
```

> Right code sample is not native JSON format!  
  JSON is not allowing comments as it is only focused on machine readability.  
  JSONC is a JSON with comments. It is not a standard, but it is supported by many tools.

</div>
<div>

The devcontainer specification powering this workshop:

```json
{
  "name": "avd_extended_workshop",
  "build": {
    "dockerfile": "Dockerfile",
    "args": {
      "_AVD_VERSION": "4.1.0",
      "_CLAB_VERSION": "0.37.1"
    }
  },
  "features": {
    "ghcr.io/devcontainers/features/docker-in-docker:1": {
      "version": "latest"
    },
    // add sshd to support gh cli codespace cp
    "ghcr.io/devcontainers/features/sshd:1": {
      "version": "latest"
    }
  },
  // set minimum host requirements for cLab
  "hostRequirements": {
    "cpus": 4,
    "memory": "8gb",
    "storage": "32gb"
  }
}
```

</div>
</div>

---

# YAML Linter

<style scoped>section {font-size: 20px;}</style>

- `Linter` is a tool that checks the code/document for errors, bugs, style violations etc.
- Install YAML-linter on your machine: `pip install --user yamllint`
- Create a minimalistic YAML file: `echo -n "key: value" > test.yaml`
- Run the linter to check errors:

```bash
vscode ➜ /workspaces/avd-extended-workshop (main) $ yamllint test.yaml
test.yaml
1:1       warning  missing document start "---"  (document-start)
1:11      error    no new line character at the end of file  (new-line-at-end-of-file)
```

- Congrats! 🎉 We have two errors in a single line YAML. :upside_down_face:
- Linters are helpful! Always check your YAMLs with a CLI linter or VSCode/other IDE extension.

---

# Every YAML Starts with `---`

<style scoped>section {font-size: 20px;}</style>

- Absolutely every YAML file must start with `---` on the first line.
- YAMLs without `---` are not valid, but will be accepted by many tools in fact.
- Quote from [yaml.org](https://yaml.org/spec/1.2.2/):
  > YAML uses three dashes (“---”) to separate directives from document content. This also serves to signal the start of a document if no directives are present. Three dots ( “...”) indicate the end of a document without starting a new one, for use in communication channels.
- Another `---` in the same yaml file would indicate the start of a new document. It is not used in Ansible data structures normally.
- Every YAML file must end with an empty line.

  > There are many more rules in YAML that are rarely in use, but must be 💯% respected.

---

# JSON vs YAML for Ansible

- Ansible can accept variables in JSON format as well.
- Convert a group var file to JSON with `yq`: `yq --prettyPrint -o=json avd_inventory/group_vars/ATD_SERVERS.yml > avd_inventory/group_vars/ATD_SERVERS.json`
- Delete the YAML file and run the build playbook: `ansible-playbook playbooks/atd-fabric-build.yml`
- New configs will be generated successfully. JSON is faster, YAML is still easier to read and edit at scale.
