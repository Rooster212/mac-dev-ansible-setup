# Mac Dev Playbook

Massive props to Jeff Geerling for teaching me how to use Ansible (with his great YouTube videos and books!) and for this idea! [His Mac Dev Playbook repo](https://github.com/geerlingguy/mac-dev-playbook) inspired me to do my own. I initially forked his but I decided to make it a bit simpler (after learning Ansible recently I thought this was a good next step) and also add a few bits of my own (e.g. using Oh My Zsh).

## Prerequisites

You need Ansible installed to run this playbook.

Before running the first time, I did these steps:

  1. First I installed XCode via the App Store. This means I am logged into the App Store, and it avoid issues in the next step.
  1. On the Mac, ensure Apple's command line tools are installed (`xcode-select --install` to launch the installer). This can take a few minutes.
  1. Then, you need to accept the XCode license agreement. You can do this by running `sudo xcodebuild -license` then reviewing the license and typing `agree` at the end, then pressing enter.

To run remotely:
  1. Ensure you can remotely access your Mac. You can do this through System Preferences > Sharing > tick Remote Login. Or you can run `sudo systemsetup -setremotelogin on` on your CLI.
  1. Allow for passwordless SSH access to the Mac by running `ssh-copy-id jamie@192.168.0.20` from your source machine (for you this would mean replacing the IP with the correct IP) and using my Mac's password to allow copying of the key. You could also run with the `-k` flag and enter your password.
  1. Then I can run the playbook by running `ansible-playbook -i inventory_remote -K main.yml` (in my case the `inventory_remote` file contains the local IP to connect to my Mac).

To run locally first time:
  1. [Install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/index.html):

     1. Run the following command to add Python 3 to your $PATH: `export PATH="$HOME/Library/Python/3.8/bin:/opt/homebrew/bin:$PATH"`
     2. Upgrade Pip: `sudo pip3 install --upgrade pip`
     3. Install Ansible: `pip3 install ansible`

  3. Clone or download this repository to your local drive.
  4. Run `ansible-galaxy install -r requirements.yml` inside this directory to install required Ansible roles.
  5. Run `ansible-playbook main.yml -K` inside this directory. Enter your macOS account password when prompted for the 'BECOME' password.

Then when I re-run I can just run `ansible-playbook -i inventory main.yml -K`.

> Note: If some Homebrew commands fail, you might need to agree to Xcode's license or fix some other Brew issue. Run `brew doctor` to see if this is the case. I ran into an issue where the Command Line Tools for Xcode had an update that had to come through softare update.

## Ansible Galaxy roles/collections used:

* Oh My Zsh installation role from @ctorgalson: https://galaxy.ansible.com/ctorgalson/oh-my-zsh
* OSX Command Line tools installation role from @elliotweiser:  https://galaxy.ansible.com/elliotweiser/osx-command-line-tools
* Mac roles collection from @geerlingguy: https://galaxy.ansible.com/geerlingguy/mac
* Dotfiles installation role from @geerlingguy: https://galaxy.ansible.com/geerlingguy/dotfiles
* Ansible role (to install Ansible on the Mac!): https://github.com/geerlingguy/ansible-role-ansible