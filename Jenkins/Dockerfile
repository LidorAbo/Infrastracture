FROM jenkins/jenkins:lts
EXPOSE 8080/tcp
EXPOSE 50000/tcp
ENV PACKER_LOG=1
ENV PACKER_LOG_PATH=/var/jenkins_home/packer_log.txt
ARG terraform_version=0.12.13
ARG packer_version=1.4.5
ARG terraform_zip_file=terraform_${terraform_version}_linux_amd64.zip
ARG packer_zip_file=packer_${packer_version}_linux_amd64.zip
USER root
RUN apt update && apt install -y \
    vim \
    locate \
    sudo \
    python3 \
    python3-pip \
    zip \
    less \
    unzip \
    man
RUN pip3 install awscli boto3 botocore
RUN wget https://releases.hashicorp.com/terraform/${terraform_version}/${terraform_zip_file} \
    && unzip ${terraform_zip_file} \
    && mv terraform /usr/bin
RUN rm -rf ${terraform_zip_file}
RUN wget https://releases.hashicorp.com/packer/${packer_version}/${packer_zip_file} \
    && unzip ${packer_zip_file} \
    &&  mv packer /usr/bin
RUN rm -rf ${packer_zip_file}
#RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list \
#    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 && apt update \
#    && apt install -y ansible
RUN pip3 install ansible
USER jenkins

