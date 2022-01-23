# base image
FROM python:3.8
# set build arg
ARG HOST_IP
# working directory in docker
WORKDIR /backend
# install python requerinments
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
# copy backend project files
COPY . /backend/
# setup host IP address
RUN for i in $(grep -ir localhost:3000 .| cut -f1 -d ":"); do sed -i "s/localhost:3000/$HOST_IP/" $i;done \
    && sed -i "s/ALLOWED_HOSTS = \[\]/ALLOWED_HOSTS = \[\'*\'\]/g" lib_catalog/settings.py
# expose port
EXPOSE 8000
