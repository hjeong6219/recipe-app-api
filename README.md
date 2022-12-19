# Recipe API project

API to add recipes with images and tags.

# Deployment

Deployment on AWS EC2 Instance:

Install dependencies:

  - Install Git:
  ```sh
  sudo yum install git -y
  ```
  
  - Install Docker, enable the service, and give permission to the `ec2-user`:
   ```sh
  sudo amazon-linux-extras install docker -y
  sudo systemctl enable docker.service
  sudo systemctl start docker.service
  sudo usermod -aG docker ec2-user
  ```
  
  - Install Docker Compose
  ```sh
  sudo curl -L "https://github.com/docker/compose/releases/download/1.29.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  sudo chmod +x /usr/local/bin/docker-compose
  ```
 
  - Clone the project
  ```sh
  git clone git@github.com:hjeong6219/recipe-app-api.git
  ```
 
  - Create a copy of the .env.sample file and modify the `DB_NAME`, `DB_USER`, `DB_PASS`, `DJANGO_SECRET_KEY`, `DJANGO_ALLOWED_HOSTS`
  ```sh
  cp .env.sample .env
  
  ```
  `DJANGO_ALLOWED_HOSTS` should be the Public IPv$ DNS address of the AWS EC2 instance.
 
  - Once the dependencies are installed, the appliction can be ran with:
  ```sh
  docker-compose -f docker-compose-deploy.yml up -d
  ```
  
  - Create a superuser for the API
  ```sh
  docker-compose -f docker-compose-deploy.yml run --rm app sh -c "python manage.py createsuperuser"
  ```
  
# Accessing the API

The login page can be can be accessed using the `DJANGO_ALLOWED_HOSTS` field configured previously
```sh
example_host/admin
```

The API has a GUI generated using Swagger at the host/api/docs

![image](https://user-images.githubusercontent.com/96016979/208331897-9b1ceec0-36c1-4d12-88ab-0defe05b5e05.png)
