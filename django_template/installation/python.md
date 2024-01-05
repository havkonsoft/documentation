# Install Python

We run the project on Ubuntu 22.04 and use Python3.10 for this project.

If you aren't using Ubuntu 22.04, you can instal Python3.10 below or keep your
existing Python version as long as it is working in the project. Installing
Python 3.10 using Apt Repository is the most straightforward solution. For
detailed explanation, please visit this
[website](https://computingforgeeks.com/how-to-install-python-on-ubuntu-linux-system/).
The bash command lines below will install Python3.10.13 in your Linux system.
Press "Enter" or "Y" when input is prompted.

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install software-properties-common -y
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt install python3.10
```

Since we are using Python3.10, we will install `python3.10-venv`, and then
install the `venv` folder inside the project folder.

```bash
sudo apt install python3.10-venv
```
