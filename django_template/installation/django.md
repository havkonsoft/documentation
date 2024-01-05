# Install Django

To install Django, we will need to set up Python virtual environment first. If
you are pulling the
[django project template repository](https://github.com/havkonsoft/django_template),
then you can skip the Django installtion below. Since we are using Python3.10,
we will install Python3.10-venv, and then install the `venv` folder inside the
project folder.

```bash
sudo apt install python3.10-venv
python3.10 -m venv venv
```

Activate the virtual environment and install Django and its dependency packages
by reading the `init_req.txt` file [here](/django_template/files/init_req.txt).

```bash
. venv/bin/activate
pip install -r files/init_req.txt
```

Export the packages to `requirements.txt` file:

```bash
pip freeze > requirements.txt
```

Create the project `server` with the following command line and move the folder
`server` and file `manage.py` to the root folder.

```bash
django-admin startproject server
```

Start the server with the following command lines.

```bash
python manage.py makemigrations
python manage.py migrate
python manage.py runserver
```

Navigate to [URL](http://localhost:8000) to observe Django is running.
