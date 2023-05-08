# 42_IC_Ring01_Born2beRoot
### Preface:
- This is a guide to the Born2beRoot project, and it was written using resources from several other guides, therefore the credit is to them.
- The purpose of re-writing this updated guide is to edit some errors that I've come across using some of the guides, and to help prevent issues that I've had to troubleshoot.
- Debian is the chosen Operating System for this project.
- The Mandatory part of the subject.pdf involves using the Guided Partitioning Method of the Debian installation. The Bonus part of the subject.pdf involves using the Manual Partitioning Method. This guide has instructions for the Manual Partitioning Method, which I recommend you do from the start, thus passing you both the Mandatory part, and 1/3 of the Bonus part of Born2beRoot. 

## Outline of Steps:
- Step 1: Download the Debian installer for your Virtual Machine (VM)
- Step 2: Installing your VM
- Step 3: Starting your VM
- Step 4: Setting up your VM
- Step 5: Connecting to SSH
- Step 6: Configuring your VM - Password Policy
- Step 7: Creating Groups & Users
- Step 8: Configuring your VM - User Priviledges
- Step 9: Configuring your VM - Script Monitoring & Crontab
- Step 10: Evaluation Checklist & Testing
- Step 11: Retrieve the Signature of your machine’s virtual disk
- Step 12: Evaluation Questions & Answers

## Step 1: Download the Debian installer for your Virtual Machine (VM)
### 1.1: Debian
1. [Click here to download Debian GNU/Linux](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/)
2. Scroll to the bottom of the page and select `debian-mac-xx.x.x-amd64-netinst.iso`

### 1.2: VM Directory (For 42Adelaide Students)**
1. In iTerm2:
- `cd sgoinfre/students`
- `mkdir <your_intra_usename>`
- `chmod 700 <your_intra_usename>`
2. Find your Debian download from Step 1.1 and put that download in this `sgoinfre/students/<your_intra_usename>` directory that you have just created (in iTerm2, `open .` to open/find the directory, and drag/drop your Debian download in there). 

### 1.3: Virtual Box
1. Open the Virtual Box application

## Step 2: Installing your VM
1. Select `New`

2. Name and operating system:
- Name: e.g. `Born2beRoot`
- Machine Folder: `/sgoinfre/students/<your_intra_usename>` (Do not type this in, use the drop down option.)
- Type: `Linux `
- Version: `Debian (64-bit)
- `continue`

3. 
