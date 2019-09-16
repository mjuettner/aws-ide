fffff# AWS IDE

This is a basic AWS development environment running on Ubuntu.  It is intended to help save people some time setting up their own development environment and start playing with the AWS CLI, CloudFormation, and various complementary tools.  Once you are more familiar with what you want in your development environment you can go off and build your own.

## Components

This basic AWS development environment installs the following components:

- AWS
  - [AWS CLI](https://aws.amazon.com/cli/)
  - [Session Manager Plugin for the AWS CLI](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html)
  - [AWS EC2 Instance Connect CLI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-connect-set-up.html#ec2-instance-connect-install-eic-CLI)
- Python
  - [Python 3](https://www.python.org/downloads/)
  - [Python 3 PIP](https://pypi.org/project/pip/)
  - [Boto 3](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html)
- Visual Studio Code
  - [Visual Studio Code](https://code.visualstudio.com/)
  - [cfn_nag tool](https://github.com/stelligent/cfn_nag) and [cfn_nag VSCode Extension](https://marketplace.visualstudio.com/items?itemName=eastman.vscode-cfn-nag)
  - [cfn-lint tool](https://github.com/aws-cloudformation/cfn-python-lint) and [cfn-lint VSCode Extension](https://marketplace.visualstudio.com/items?itemName=kddejong.vscode-cfn-lint)
  - [Python VSCode Extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
  - [Azure Repos VSCode Extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
  - [GitLens VSCode Extension](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
  - [Cloudformation YAML Snippets VSCode Extension](dsteenman.cloudformation-yaml-snippets)

Please visit each components page to learn about their use.

## Getting Started

### Prerequisites

- Install [VirtualBox](https://www.virtualbox.org/)
- Install [Vagrant](https://www.vagrantup.com/)

## Installation Overview

The installation really just involves picking a location on your system to place the Vagrantfile.  You will then just navigate to that location and issue the 'vagrant up' command, which will parse the Vagrantfile and build the Ubuntu AWS IDE VirtualBox VM.

One thing to consider regarding the location you choose is that that location will be mounted inside the VirtualBox VM on the path /vagrant.

If I place my Vagrantfile in C:\vagrant, once the Ubuntu image is built and running, that path will be mounted to /vagrant in Ubuntu.  While on the Ubuntu VM, if I write files to /vagrant, I will be able to view them on my host operating system at C:\vagrant.

This is just an easy and convenient way to share files between your host OS and the VM and to also provide protection from losing files if something happens to the Ubuntu VM.  If you're always saving your work to Git or some other location outside of the VM, this is less important.

## Customization

- You can set vb.gui to false if you're not interested in using the Gnome GUI
- Configure memory and cpu settings by setting vb.memory and vb.cpus to settings you feel are appropriate for your system

## Installation

- Create a folder somewhere on your system and place the Vagrantfile there
- Navigate to that folder via command line and issue the 'vagrant up' command
- Wait for everything to download and build
    - You will know it's done when your command console where you executed 'vagrant up' returns back to the command prompt
    - The VirtualBox VM should reboot as a final step and boot up displaying the Gnome GUI
    - In my tests it takes 20 - 30 minutes

## Default Ubuntu Credentials

- The default credentials are vagrant / vagrant

## Connecting

- Vagrant should have enabled the Gnome GUI (for using Visual Studio Code), so you should see a VirtualBox window with that GUI that you can log into.
- Alternately, you can try executing 'vagrant ssh' from the command line to access the VM directly.

## Usage

- Right-click on the desktop and select 'Open Terminal', you can check the AWS CLI is available by executing `aws help`
- In the Terminal window, launch Visual Studio Code by executing `code`

## Continuing Usage

- Vagrant configured a VirtualBox VM for you, so you can always just go into the VirtualBox console to stop/start the VM, however this isn't recommended.
- You should continue to use the 'vagrant up' command to launch your VirtualBox VM. Vagrant configures multiple things when starting up the VM, like mounting the /vagrant filesystem and verifying the VirtualBox Guest Plugin is on the correct version.
- You can always add or install more components into the Ubuntu VM as you want, but consider instead adding them to the Vagrantfile so you can maintain your development environment as code.
