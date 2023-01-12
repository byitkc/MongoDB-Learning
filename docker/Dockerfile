# syntax=docker/dockerfile:1
FROM amazonlinux:2022.0.20221207.4
WORKDIR /code
RUN yum -y install python3 python3-pip zip
# RUN pip3 install --upgrade pip
COPY requirements.txt requirements.txt
WORKDIR /code/python
RUN pip install -r /code/requirements.txt -t .
RUN zip -r layer.zip .
ENTRYPOINT [ "/bin/bash" ]