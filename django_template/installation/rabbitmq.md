# Install RabbitMQ

We will be using RabbitMQ for Django Celery. Follow the steps below to install
RabbitMQ in Ubuntu.

First, ensure your system is up to date. Run the command:

```bash
sudo apt update && sudo apt upgrade -y
```

You need to add the official RabbitMQ signing key and repository, run the
command:

```bash
sudo apt install curl gnupg -y
curl -fsSL https://packages.rabbitmq.com/gpg | sudo apt-key add -
```

Now add the repository:

```bash
sudo add-apt-repository 'deb https://dl.bintray.com/rabbitmq/debian focal main'
```

Install RabbitMQ Server with the commands below:

```bash
sudo apt update && sudo apt install rabbitmq-server -y
```

Depending on your current software development lifecycle, you may need to enable
and start the RabbitMQ Service:

```bash
sudo systemctl enable rabbitmq-server
sudo systemctl start rabbitmq-server
```

Verify the status:

```bash
sudo systemctl status rabbitmq-server
```

You can disable and stop and RabbitMQ Service on startup if you intend to use it
in Docker later on.

```bash
sudo systemctl disable rabbitmq-server
```
