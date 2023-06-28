---
marp: true
theme: default
class: invert
author: Petr Ankudinov
# size 16:9 1280px 720px
size: 16:9
paginate: true
math: mathjax
style: |
    img[alt~="custom"] {
      float: right;
    }
    .columns {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 1rem;
    }
# style: |
#     :root {
#         background: #004643;
#         color: #abd1c6
#     }
#     footer {
#         font-size: 12px;
#     }
---

# AVD Extended Workshop

<!-- Do not add page number on this slide -->
<!--
_paginate: false
-->

```Intro into Ansible, Ansible AVD, Git and VSCode for new and existing AVD users```

![bg left fit](img/avd-logo.webp)

<!-- backgroundImage: "linear-gradient(to bottom, #1e3744, #301B29)" -->

---

# What is this Workshop about?

<!-- Add footer starting from this slide -->
<!--
footer: 'Arista Ansible AVD Extended Workshop'
-->

<style scoped>section {font-size: 14px;}</style>

- Git basics
- VSCode basics
- Ansible basics
- Containers basics and using container to build Ansible AVD environment
- Building simple L3LS network with Ansible AVD

This workshop is using Arista Test Drive Single DC topology (drawing on the right side).

![bg right fit](img/atd-topo.png)

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

# How to use this Workshop?

<style scoped>section {font-size: 24px;}</style>

- To try all practical examples you need to have access to the lab environment. There are 3 possible options:
  - Use Github Codespaces. This is the preferred option, but double check that you understand all the costs and free tier limits.
  - Use Arista Test Drive - Single DC topology. Please ask your Arista SE to create an ATD lab for you.
  - Build your own lab environment: Ubuntu LTS + Docker + ContainerLab. This option is not described in detail, but the devcontainer used to build Codespaces environment will work on any machine with Docker installed. Please contact your SE if you need help.

---

# References

<style scoped>section {font-size: 24px;}</style>

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

---

# How to setup Ansible AVD in Arista Test Drive environment?

- We could use a script to setup required Ansible collections and tools in Arista Test Drive environment, but it's a good opportunity to discuss what are the requirements but installing them manually.
- For details please check [AVD documentation](https://avd.arista.com/) `Installation > Collection Installation` section.

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
