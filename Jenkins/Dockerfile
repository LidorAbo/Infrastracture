FROM jenkins:latest
ARG terraform_version=0.12.13
ARG packer_version=1.4.5
ARG terraform_zip_file=terraform_${terraform_version}_linux_amd64.zip
ARG packer_zip_file=packer_${packer_version}_linux_amd64.zip
USER root
RUN apt update && apt installl -y \
vim \:q
locate \
sudo \
python3 \
python3-pip \
zip \
unzip \
RUN pip3 install awscli --upgrade --user
RUN echo export PATH=~/.local/bin:$PATH >> ~/.bashrc
RUN wget https://releases.hashicorp.com/terraform/${terraform_version}/${terraform_zip_file}
RUN unzip ${terraform_zip_file}
RUN mv terraform /usr/bin
RUN wget https://releases.hashicorp.com/packer/${packer_version}/${packer_zip_file}
RUN unzip ${packer_zip_file}
RUN mv packer /usr/bin
RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 && apt update \
    && apt install -y ansible
USER jenkins


