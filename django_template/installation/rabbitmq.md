# Install RabbitMQ

We will be using RabbitMQ for Django Celery. Follow the steps below to install
RabbitMQ in Ubuntu.

First things first, let’s install the prerequisites:

```bash
sudo apt-get install curl gnupg apt-transport-https -y
```

We are now ready to add repository signing keys for RabbiMQ main, ErLang, and
RabbitMQ PackageCloud repositories respectively:

```bash
curl -1sLf "https://keys.openpgp.org/vks/v1/by-fingerprint/0A9AF2115F4687BD29803A206B73A36E6026DFCA" | sudo gpg --dearmor | sudo tee /usr/share/keyrings/com.rabbitmq.team.gpg > /dev/null
curl -1sLf "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0xf77f1eda57ebb1cc" | sudo gpg --dearmor | sudo tee /usr/share/keyrings/net.launchpad.ppa.rabbitmq.erlang.gpg > /dev/null
curl -1sLf "https://packagecloud.io/rabbitmq/rabbitmq-server/gpgkey" | sudo gpg --dearmor | sudo tee /usr/share/keyrings/io.packagecloud.rabbitmq.gpg > /dev/null
```

Create a new file at `/etc/apt/sources.list.d/rabbitmq.list`

```bash
sudo touch /etc/apt/sources.list.d/rabbitmq.list
```

Add the following repositories for ErLang and RabbitMQ respectively that are
suited for Ubuntu 22.04 jammy release:

```bash
sudo vi /etc/apt/sources.list.d/rabbitmq.list
```

```bash
deb [signed-by=/usr/share/keyrings/net.launchpad.ppa.rabbitmq.erlang.gpg] http://ppa.launchpad.net/rabbitmq/rabbitmq-erlang/ubuntu jammy main
deb-src [signed-by=/usr/share/keyrings/net.launchpad.ppa.rabbitmq.erlang.gpg] http://ppa.launchpad.net/rabbitmq/rabbitmq-erlang/ubuntu jammy main
deb [signed-by=/usr/share/keyrings/io.packagecloud.rabbitmq.gpg] https://packagecloud.io/rabbitmq/rabbitmq-server/ubuntu/ jammy main
deb-src [signed-by=/usr/share/keyrings/io.packagecloud.rabbitmq.gpg] https://packagecloud.io/rabbitmq/rabbitmq-server/ubuntu/ jammy main
```

Save the file and you are ready to update your repository listings:

```bash
sudo apt-get update -y
```

After your repository listings are updated, continue with installing required
ErLang packages:

```bash
sudo apt-get install -y erlang-base \
    erlang-asn1 erlang-crypto erlang-eldap erlang-ftp erlang-inets \
    erlang-mnesia erlang-os-mon erlang-parsetools erlang-public-key \
    erlang-runtime-tools erlang-snmp erlang-ssl \
    erlang-syntax-tools erlang-tftp erlang-tools erlang-xmerl
```

Finally, we can install RabbitMQ server and its dependencies:

```bash
sudo apt-get install rabbitmq-server -y --fix-missing
```

If all went well, you should see a rabbitmq-server process up and running:

```bash
sudo systemctl status rabbitmq-server
```

You can disable and stop and RabbitMQ Service on startup if you intend to use it
in Docker later on.

```bash
sudo systemctl disable rabbitmq-server
```

In order to use Celery on local development (opening another terminal), you need
to enable it and start the service

```bash
sudo systemctl enable rabbitmq-server
sudo systemctl start rabbitmq-server
```
