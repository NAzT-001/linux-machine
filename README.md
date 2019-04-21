# Development Linux Setup

| Branch  | Status |
|---------|--------|
| master  | [![Build Status](https://travis-ci.org/markosamuli/linux-machine.svg?branch=master)](https://travis-ci.org/markosamuli/linux-machine)
| develop | [![Build Status](https://travis-ci.org/markosamuli/linux-machine.svg?branch=develop)](https://travis-ci.org/markosamuli/linux-machine)

This is a collection of Ansible roles and tasks to setup a Linux development
machine.

See [markosamuli/macos-machine] for my macOS setup.

[markosamuli/macos-machine]: https://github.com/markosamuli/macos-machine

## Requirements

- Ubuntu 16.04, 18.04 or another supported operating system
- Git installed
- Bash shell
- Ansible 2.7
- Python 2.7 or 3.7 required by Ansible

### Ubuntu

This setup has been tested on the [Ubuntu] [16.04 LTS (Xenial Xerus)]
and [18.04 LTS (Bionic Beaver)] releases.

Travis CI builds are running on Ubuntu 16.04.

[Ubuntu]: https://www.ubuntu.com/
[16.04 LTS (Xenial Xerus)]: http://releases.ubuntu.com/16.04/
[18.04 LTS (Bionic Beaver)]: http://releases.ubuntu.com/18.04/

### Ubuntu on WSL

I've also used this playbook to install packages on Ubuntu running on
[Windows Subsystem for Linux] on Windows 10.

Some packages are known not to work so I've added custom fact `is_wsl`
that can be used to check if we're running Linux on Windows and these
will be skipped during the set up.

[Windows Subsystem for Linux]: https://docs.microsoft.com/en-us/windows/wsl/install-win10

### Pengwin on WSL

I've tried installing some of the packages on [Pengwin] distribution.

Ansible installation should be compatible with [pengwin-setup] as found
in the `development` branch.

Tested packages:

- [Neovim]
- Node.js with NVM

Known conflicts:

- Pengwin installs Terraform in `/usr/bin/terraform`
- Pengwin installs Node.js with [n npm] instead of NVM

[Pengwin]: https://github.com/WhitewaterFoundry/Pengwin
[pengwin-setup]: https://github.com/WhitewaterFoundry/pengwin-setup
[Neovim]: https://neovim.io/
[n npm]: https://github.com/tj/n

## Install

Install Git and curl:

```bash
sudo apt update
sudo apt install curl git
```

You can run the installer script that will clone the code from GitHub and run the `setup` script.

```bash
curl -s https://raw.githubusercontent.com/markosamuli/linux-machine/master/install.sh | bash -
```

## Getting Started

Clone this project locally and run the `./setup` script.

```bash
git clone https://github.com/markosamuli/linux-machine
cd linux-machine
./setup
```

## Local options

You can pass custom variables to the Ansible playbook and roles by creating
a `machine.yaml` file to customise your configuration.

```bash
cp machine.yaml.example machine.yaml
```

The `setup` script will detect if this file exists and passes it to the
Ansible Playbook with `--extra-vars`.

## Software installed by the playbooks

### Installation tools

The following tools are prequiresites and always installed during setup if not
already found on the system.

- [Ansible](https://www.ansible.com/) from [Ansible PPA](https://launchpad.net/~ansible/+archive/ubuntu/ansible)

### Desktop applications

- [Terminator](https://gnometerminator.blogspot.com/p/introduction.html)
- [Slack](https://snapcraft.io/slack) via Snap package
- [Hyper](https://hyper.is/)

### Command line tools

- [GNU Wget](https://www.gnu.org/software/wget/)
- [curl](https://curl.haxx.se/)
- [jq](https://stedolan.github.io/jq/) command-line JSON processor
- [The Silver Searcher](https://github.com/ggreer/the_silver_searcher) code
  searcing utility similar to `ack`
- [htop](https://hisham.hm/htop/)

### Editors

- [Visual Studio Code](https://code.visualstudio.com/) via Snap package
- [Vim](https://www.vim.org/)
- [Neovim](https://neovim.io/)

### Programming languages and version managers

- [Python]((https://www.python.org/)) and [pip](https://pypi.org/project/pip/) from Ubuntu packages
- [virtualenv](https://virtualenv.pypa.io/en/latest/) from PyPI
- [Node Version Manager](https://github.com/creationix/nvm) (NVM)
- [Node.js](https://nodejs.org/en/) LTS installed with NMV
- [virtualenv](https://virtualenv.pypa.io/en/latest/)
- [pyenv](https://github.com/pyenv/pyenv)
- [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)
- [Python](https://www.python.org/) v2.7 and v3.7 installed with pyenv
- [Go programming language](https://golang.org/)

### Developer tools

- [Git](https://git-scm.com/)
- [Docker Engine](https://docs.docker.com/engine/) Community Edition
- [VirtualBox](https://www.virtualbox.org/)
- [Vagrant](https://www.vagrantup.com/)

### DevOps and Cloud tools

- [Terraform](https://www.terraform.io/)
- [Packer](https://packer.io/)
- [Google Cloud SDK](https://cloud.google.com/sdk/)
- [AWS CLI](https://aws.amazon.com/cli/)
- [aws-shell](https://github.com/awslabs/aws-shell) - interactive shell for
  AWS CLI
- [AWS Vault](https://github.com/99designs/aws-vault) - a vault for securely
  storing and accessing AWS credentials in development environments
- [cli53](https://github.com/barnybug/cli53) - command line tool for Amazon
  Route 53

## Changes to existing configuration

The installer creates empty `~/.bash_profile` and `~/.bashrc` files and makes
sure `~/.bashrc` is loaded from `~/.bash_profile`.

The installer makes changes to your `~/.bashrc` and `~/.zshrc` files, so take
backup copies of them before running the script.

## Ansible Roles

The following external Ansible roles are installed and used. See
[requirements.yml] file for the installed versions.

| Role | Build status |
|------|--------------|
| [markosamuli.aws-tools] | [![Build Status](https://travis-ci.org/markosamuli/ansible-aws-tools.svg?branch=master)](https://travis-ci.orgmarkosamuli/ansible-aws-tools) |
| [markosamuli.gcloud] | [![Build Status](https://travis-ci.org/markosamuli/ansible-gcloud.svg?branch=master)](https://travis-ci.orgmarkosamuli/ansible-gcloud) |
| [markosamuli.golang] | [![Build Status](https://travis-ci.org/markosamuli/ansible-golang.svg?branch=master)](https://travis-ci.orgmarkosamuli/ansible-golang) |
| [markosamuli.nvm] | [![Build Status](https://travis-ci.org/markosamuli/ansible-nvm.svg?branch=master)](https://travis-ci.orgmarkosamuli/ansible-nvm) |
| [markosamuli.packer] | [![Build Status](https://travis-ci.org/markosamuli/ansible-packer.svg?branch=master)](https://travis-ci.orgmarkosamuli/ansible-packer) |
| [markosamuli.pyenv] | [![Build Status](https://travis-ci.org/markosamuli/ansible-pyenv.svg?branch=master)](https://travis-ci.orgmarkosamuli/ansible-pyenv) |
| [markosamuli.terraform] | [![Build Status](https://travis-ci.org/markosamuli/ansible-terraform.svg?branch=master)](https://travis-ci.orgmarkosamuli/ansible-terraform) |
| [markosamuli.vagrant] | [![Build Status](https://travis-ci.org/markosamuli/ansible-vagrant.svg?branch=master)](https://travis-ci.orgmarkosamuli/ansible-vagrant) |
| [markosamuli.hyper] | [![Build Status](https://travis-ci.org/markosamuli/ansible-hyper.svg?branch=master)](https://travis-ci.orgmarkosamuli/ansible-hyper) |

[markosamuli.aws-tools]: https://github.com/markosamuli/ansible-aws-tools
[markosamuli.gcloud]: https://github.com/markosamuli/ansible-gcloud
[markosamuli.golang]: https://github.com/markosamuli/ansible-golang
[markosamuli.hyper]: https://github.com/markosamuli/ansible-hyper
[markosamuli.nvm]: https://github.com/markosamuli/ansible-nvm
[markosamuli.packer]: https://github.com/markosamuli/ansible-packer
[markosamuli.pyenv]: https://github.com/markosamuli/ansible-pyenv
[markosamuli.terraform]: https://github.com/markosamuli/ansible-terraform
[markosamuli.vagrant]: https://github.com/markosamuli/ansible-vagrant
[requirements.yml]: requirements.yml

## References

This is based on my previous setup [markosamuli/machine] that was forked off
from  [caarlos0/machine] to suit my needs.

[markosamuli/machine]: https://github.com/markosamuli/machine
[caarlos0/machine]: https://github.com/caarlos0/machine

## License

[MIT](LICENSE)

## Authors

- [@markosamuli](https://github.com/markosamuli)
