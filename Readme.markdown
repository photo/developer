<img src="https://github.com/photo/frontend/raw/master/files/creative/logo.png" style="width:234px; height:43px; margin:auto;">

### What is OpenPhoto?

1.  [FAQ](http://theopenphotoproject.org/documentation/faq/Faq), Answers to the most common questions.

### About the environment

The recommended way to set up a developer environment is with the provided [VirtualBox](https://www.virtualbox.org/) VMs using [Vagrant](http://vagrantup.com/). This lets you create a sandboxed environment that's known to work.

The box is based off Ubuntu Lucid32 with all of the packages pre-installed to be up and running. We followed the [installation guide for Ubuntu with Apache](https://github.com/photo/frontend/blob/master/documentation/guides/InstallationUbuntuApache.markdown) with some modifications to make it suitable for development.

----------------------------------------

### Getting set up

Refer to the [Vagrant documentation](http://vagrantup.com/v1/docs/getting-started/index.html) for details.

#### Download and install VirtualBox 4.1.20

Download the appropriate binary.

1. [Windows](http://download.virtualbox.org/virtualbox/4.1.20/VirtualBox-4.1.20-80170-Win.exe)
1. [Mac OSX](http://download.virtualbox.org/virtualbox/4.1.20/VirtualBox-4.1.20-80170-OSX.dmg)
1. [Linux](https://www.virtualbox.org/wiki/Linux_Downloads)

Once downloaded you'll need to install the program. We'll be running Virtualbox headless so this is the last time you'll directly interface with Virtualbox.

You can find a complete list of downloads for 4.1.20 [here](http://download.virtualbox.org/virtualbox/4.1.20/).

#### Download and install Vagrant 1.3.0

You can download the appropiate binary from [Vagrant 1.3.0 download page](http://downloads.vagrantup.com/tags/v1.0.3). Once downloaded you will need to install the program.

There's a complete list of downloads for Vagrant [here](http://downloads.vagrantup.com).

#### Initialize and boot your VM

Using the base box provided by us run the `vagrant box add` command. This is a 600MB file so it may take some time.

    vagrant box add photo http://photo-developer.s3.amazonaws.com/vagrant-photo-developer-1.0.box

Next you'll need to decide which directory you want to set up your files in. We'll assume it's `%HOME%/dev/openphoto`. Open a terminal and `cd` into that directory and copy the contents of our [Vagrantfile](https://raw.github.com/photo/developer/master/vagrant/Vagrantfile) into it.

    curl -s https://raw.github.com/photo/developer/master/vagrant/Vagrantfile > Vagrantfile

Also clone the frontend repository into this folder

    git clone git@github.com:photo/frontend.git
    
or most likely with your repository if you forked it on github

    git clone git@github.com:<username>/frontend.git

Now you can boot your VM and add a host entry pointing to itself.

    vagrant up
    
    # test that it is working by ssh'ing
    vagrant ssh
    
    # add the host entry
    sudo sh -c 'echo "33.33.33.33 local.photo" >> /etc/hosts'

    # return to your host
    exit

That's all. Let's get your local host set up to talk to your VM.

#### Configure your local environment

In order for your local environment to communicate with the virtual environment we're creating you will need to set up an alias in your hosts file.

1. Windows `%SystemRoot%\system32\drivers\etc\hosts`
1. OSX `/etc/hosts`
1. Linux `/etc/hosts`
1. [All others](http://en.wikipedia.org/wiki/Hosts_%28file%29#Location_in_the_file_system)

Append the following to your `hosts` file.

    33.33.33.33 local.photo

What this says is that the VM's IP address is 33.33.33.33 and your local host can access it using the DNS name _local.photo_.

----------------------------------------

### Make magic happen

Now that everything is set up you should be able to load a browser and go to [http://local.photo](http://local.photo).

To use MySql you can enter the following information.

1. Host - _localhost_
1. Username - _root_
1. Password - (empty)
1. Database - _photo_

----------------------------------------

### Troubleshooting

If you have problems, please open an issue and we will aggregate common errors here.
