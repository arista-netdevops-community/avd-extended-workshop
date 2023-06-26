---
marp: true
theme: default
class: invert
author: Petr Ankudinov
size: 16:9
paginate: true
math: mathjax
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

This workshop is using Arista Test Drive Single DC topology. Please ask your Arista SE to create a topology for you or build your own lab using the topology on the right side.

![bg right fit](img/atd-topo.png)

---

# What is NOT covered in this Workshop?

<style scoped>section {font-size: 24px;}</style>

- This workshop is not a deep dive into each and every topic. It is covering some advanced concepts, but you may need additional documentation and training to understand every topic in details.  
  For additional information please refer to the following resources:
  - [Ansible AVD Documentation](https://avd.arista.com/)
  - [VSCode Documentation](https://code.visualstudio.com/docs)
  - [Git Documentation](https://git-scm.com/doc) - Pro Git book is a good start
  - Container Trainings by [@jpetazzo](https://github.com/jpetazzo):
    - [Github repository](https://github.com/jpetazzo/container.training)
    - [Training materials](https://container.training/)
- We are not going to use Arista CloudVision Portal (CVP) in this workshop. It provides a lot of advantages, but is not essential to understand the concepts covered in this workshop.
