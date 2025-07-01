FROM mcr.microsoft.com/devcontainers/base:ubuntu

RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
RUN echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list

RUN echo "Installing aws-nuke"
RUN wget -O aws-nuke-linux-amd64.tar.gz https://github.com/ekristen/aws-nuke/releases/download/v3.29.5/aws-nuke-v3.29.5-linux-amd64.tar.gz 
RUN tar -xzf aws-nuke-linux-amd64.tar.gz
RUN mv aws-nuke /usr/local/bin/
RUN chmod u+x /usr/local/bin/aws-nuke
RUN echo "Validating version for nuke" | /usr/local/bin/aws-nuke -h

# Install Terraform and other dependencies
RUN apt-get update && apt-get install -y \
    terraform \
    python3-pip \
    curl \
    unzip \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/lib/apt/lists.d/* \
    && apt-get autoremove \
    && apt-get clean \
    && apt-get autoclean

# Install AWS CLI
RUN	curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip && ./aws/install

# Install Azure CLI
RUN	curl -sL https://aka.ms/InstallAzureCLIDeb | bash