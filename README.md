# Description

This is an Ansible role template that includes [`test-kitchen`](https://github.com/test-kitchen/test-kitchen) basic configuration to develop and run [serverspec](http://serverspec.org/) Acceptance Tests against the corresponding Ansible playbooks on different GNU/Linux systems.

# Requirements

- Ansible 1.9 or higher (can be easily installed via `pip`. E.g: `sudo pip install ansible==1.9.2`)
- [Vagrant](https://www.vagrantup.com) 1.7 or higher
- `sshpass` package which is needed by Ansible if you are using SSH authentication by password. On Ubuntu/Debian: `$ sudo apt-get install sshpass`
- Virtualbox
- [Oh-my-box](https://github.com/abessifi/oh-my-box) tool, optional, if you want to quickly provision a Vagrant box with Ansible and Ruby pre-installed.

# Installation and Setup

- First, clone the project and rename it for the Ansible role you want to develop.
- Then, you maybe want to adapt the Vagrantfile and the inventory variable(s) within the `host_vars/` directory to suit your environment (services ports, IP addresses, etc).
- Install the `kitchen-ansible` gem in your system, along with kitchen-vagrant or some other suitable driver for `test-kitchen` (listed within the Gemfile):


    $ bundler install

# Usage

After installing `test-kitchen` and the other required gems, edit the `.kitchen.yml`, typically the `box` parameter in the `platforms` configuration section. This file describes your testing configuration, what you want to test and on which target platforms. Each of these suite and platform combinations are called instances. By default, the test suite will check if the actual Ansible role creates correctly a **/tmp/baz** file with the right permissions (see the `./test/integration/default/` suite).

Get a listing of your instances with:

    $ kitchen list

    Instance              Driver   Provisioner      Verifier  Transport  Last Action
    default-debian-8-x64  Vagrant  AnsiblePlaybook  Busser    Ssh        <Not Created>

Run Ansible on an instance, in this case **default-debian-8-x64**, with:

    $ kitchen converge default-debian-8-x64

Destroy all instances with:

    $ kitchen destroy

Now you can run the acceptance tests against your Ansible role:

	$ kitchen verify

Whoot! :)

# Useful links

- [Oh-my-box tool](https://github.com/abessifi/oh-my-box)
- [kitchen-ansible](https://github.com/neillturner/kitchen-ansible)
