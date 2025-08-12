FROM python:3.10

RUN apt-get update && apt-get upgrade -y
ENV DEBCONF_NOWARNINGS=yes

RUN /usr/local/bin/python -m pip install --upgrade pip

# Utils
RUN apt-get install -y gitk less cloc

# Creating a non-root user
# https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user#_creating-a-nonroot-user
# 1. ARGs
ARG USERNAME=user
ARG USER_UID=1000
ARG USER_GID=$USER_UID
# 2. Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    # && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
# ********************************************************
# * Anything else you want to do like clean up goes here *
# ********************************************************
# 3. [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME
