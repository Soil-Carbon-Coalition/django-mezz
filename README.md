# django-mezz

#installing django-mezzanine on Ubuntu 16.04

#decide on a project name and directory

sudo mkdir yourproject 

sudo chown yourusername yourproject

#cd to it and create virtualenv such as env

. env/bin/activate

pip install --upgrade pip

pip install mezzanine

mezzanine-project yourproject



#in local_settings.py set up for postgresql database:

    DATABASES = {

    "default": {

        "ENGINE": "django.contrib.gis.db.backends.postgis",

        "NAME": "yourproject",

        "USER": "yourproject",

        "PASSWORD": "",

        }}

#make sure postgresql permissions /etc/postgresql/9.5/main/pg_hba.conf are allowing access



#create database and user

createuser -Upostgres yourproject

createdb -Upostgres -Oyourproject yourproject

psql -Upostgres yourproject -c "create extension postgis" 

cd yourproject

python manage.py migrate

python manage.py createsuperuser

#make sure ssl and apache are properly set up

python manage.py collectstatic

cd static

sudo chown -R www-data media


#THUMBNAIL SIZING ISSUE: use Pillow==4.1.1 instead of 4.3




