# Basic commands for virtual environments and Docker

## Virtual Environments

Install pipenv (be sure to have python 3.7)

```bash
pip install pipenv
```

Install libaries inside pipenv

```bash
pipenv install numpy scikit-learn==0.24.2 flask gunicorn
```

Two files are created `Pipfile` and `Pipfile.lock`

Launch shell with virtual environment

```shell
pipenv shell
```

Run application using `gunicorn` inside virtual environment

```shell
pipenv run gunicorn --bind 0.0.0.0:9696 python_file:app_name
```

List installed virtual environment

```bash
pipenv --venv
```

Remove installed virtual environment

```shell
pipenv --rm
```

Use pipefile to reproduce virtual environment (Pipfile and Pipefile.lock must be inside).

```shell
pipenv install
```

## Docker

Example of using a docker container with python 3.8.

```bash
docker run -it --rm --entrypoint=bash python:3.8-slim
```

- `-it` -> interactive and terminal
  
- `--rm` -> remove after finish
  
- `--entrypoint` -> start docker with application
  
- `python:3.8-slim` -> `image:tag`
  

Build docker image using Docker file

```shell
docker build -t zoomcamp-test .
```

- `-t zoomcamp-test`-> use tag named zoomcamp
  
- `.` -> use de current directory to get Dockerfile
  

Run built docker image with entrypoint

```bash
docker run -it --rm --entrypoint=bash zoomcamp-test
```

Run built docker image with port mapping

```shell
docker run -it --rm -p 9696:8080 zoomcamp-test
```

- `-p 9696:8080` -> use port mapping with `host_port:docker_port`

## AWS Elastic Beanstalk

Create virtual environment with AWS Elastic Beanstalk CLI

```shell
pipenv install awsebcli --dev
```

`--dev` -> used for developing purposes

Create application (locally) `churn-serving`

```shell
eb init -p docker -r us-east-1 churn-serving
```

- `-p`-> platform
  
- `-r` -> region
  

Run locally

```shell
eb local run --port 8080
```

Create environment (cloud) `churn-serving-env`

```shell
eb create churn-serving-env
```
