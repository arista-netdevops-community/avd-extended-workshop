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

Topics:

- Git basics
- VSCode basics
- Ansible basics
- Containers basics and using container to build Ansible AVD environment
- Building simple L3LS network with Ansible AVD

Structure:

- This workshop is split into 3 sections. Each section takes around 2 hours to complete. That can be done as a full day workshop or split into 3 separate sessions.
- Make a break when you see a slide with a coffee cup ☕️
- Ask questions at any time!

![bg right](img/pexels-suzy-hazelwood-1226398.jpg)

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

`Section 1`

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

# Before We Start

<style scoped>
section {background: linear-gradient(to bottom, #000000, #434343);}
ul {font-size: 12px;}
</style>

![bg left](img/pexels-pixabay-159591.jpg)

`Section 2`

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
- All set! 🎉
- Your clone will now be referenced as `<your-copy-of-this-repository>` in this workshop.

---

# How to Setup ATD Environment

<style scoped>
section {background: linear-gradient(to bottom, #000000, #434343);}
ul {font-size: 12px;}
</style>

![bg left](img/pexels-pixabay-159591.jpg)

`Section 3`

> - skip practice this section if you are using Codespaces
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
# 1. Clone your copy of this repository
git clone <your-copy-of-this-repository>

# 2. Update package index files
sudo apt-get update

# 3. Install iputils as life is hard without ping
sudo apt-get install -y --no-install-recommends iputils-ping

# 4. Add .local/bin in home folder to PATH
export PATH=$PATH:/home/coder/.local/bin

# 5. Upgrade pip and install Ansible core
#    If you get errors, ignore. This bug will be fixed soon.
pip install --upgrade pip
pip3 install "ansible-core>=2.13.1,<2.14.0"

# 6. Install Arista AVD collection
ansible-galaxy collection install arista.avd:==4.1.0

# 7. Install AVD collection requirements
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
