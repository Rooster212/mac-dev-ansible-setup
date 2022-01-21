# Mac Dev Playbook

Massive props to Jeff Geerling for teaching me how to use Ansible (with his great YouTube videos and books!) and for this idea! [His Mac Dev Playbook repo](https://github.com/geerlingguy/mac-dev-playbook) inspired me to do my own. I initially forked his but I decided to make it a bit simpler (after learning Ansible recently I thought this was a good next step) and also add a few bits of my own (e.g. using Oh My Zsh).

## Prerequisites

You need Ansible installed to run this playbook.

I'm running this remotely for the first time, so I did this:

  1. First I installed XCode via the App Store. This means I am logged into the App Store, and it avoid issues in the next step.
  1. On the Mac, ensure Apple's command line tools are installed (`xcode-select --install` to launch the installer).
  2. Then, ensure you can remotely access your Mac. You can do this through System Preferences > Sharing > tick Remote Login. Or you can run `sudo systemsetup -setremotelogin on` on your CLI.
  4. I then allowed for passwordless SSH access to the Mac by running `ssh-copy-id jamie@192.168.0.20` (for you this would mean replacing the IP with the correct IP) and using my Mac's password to allow copying of the key.
  5. Then I can run the playbook by running `ansible-playbook -i inventory_remote -K main.yml` (in my case the `inventory_remote` file contains the local IP to connect to my Mac).

> Note: If some Homebrew commands fail, you might need to agree to Xcode's license or fix some other Brew issue. Run `brew doctor` to see if this is the case.

## Ansible Galaxy roles/collections used:

* Oh My Zsh installation role from @ctorgalson: https://galaxy.ansible.com/ctorgalson/oh-my-zsh
* OSX Command Line tools installation role from @elliotweiser:  https://galaxy.ansible.com/elliotweiser/osx-command-line-tools
* Mac roles collection from @geerlingguy: https://galaxy.ansible.com/geerlingguy/mac
* Dotfiles installation role from @geerlingguy: https://galaxy.ansible.com/geerlingguy/dotfiles
* Ansible role (to install Ansible on the Mac!): https://github.com/geerlingguy/ansible-role-ansible