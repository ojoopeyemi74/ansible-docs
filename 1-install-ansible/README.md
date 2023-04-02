## Ansible on ubuntu controller machine. 
```
sudo apt-get update -y

sudo apt install -y software-properties-common

sudo add-apt-repository --yes --update ppa:ansible/ansible

sudo apt update

sudo apt install -y ansible

ansible --version

```
# Install Ansible on RHEL
```

sudo dnf install python3 python3-pip -y

sudo dnf -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

sudo dnf install  --enablerepo epel-playground  ansible

```

# Installing Ansible on CentOS

# Installing the epel-release package using the yum command yum install epel-release
```
yum install epel-release

sudo yum install ansible

```

# On Hosts machines - 
```
sudo apt-get update
sudo apt-get install python

python3 --version

Step 5: Install PIP ( Package Manager )

sudo apt install python3-pip

pip3 --version

```

# Installing Python3 dependencies on Debian
sudo apt update

sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev wget libbz2-dev

sudo apt install python3 -y

wget https://www.python.org/ftp/python/3.11.1/Python-3.11.1.tgz

tar -xvf Python-3.11.1.tgz

cd Python-3.11.1

#Next, The -–enable-optimizations option runs multiple tests and optimizes the Python binary. Then run the make command to compile the Python  source code. This takes quite a while, so you might consider taking a break at this point.

sudo ./configure --enable-optimizations

sudo make -j 2

sudo make altinstall

python3.11 -V

Step 5: Install PIP ( Package Manager )

sudo apt install python3-pip

pip3 --version




# Configure SSH Access from controller to Ansible Hosts machines
```

On the controller, generate ssh key using    -         ssh-keygen

Copy the  id_rsa.pub to the host .ssh/  authorized_keys

And now should be able to ssh into the host from the controller 

```

# Setting up Ansible Host and testing connection 

```
Exit from the host back to the controller 

sudo nano /etc/ansible/hosts  # by default ansible use this file for inventory file

Add to the bottom of the file 
[production]
agent1 ansible_ssh_host=172.31.43.43
```

# test connectivity 
```
ansible -m ping all
```
