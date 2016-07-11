FROM debian:jessie
MAINTAINER Mozilla Releng release+nix@mozilla.com
RUN apt-get -y update && apt-get install -y \
    bzip2

RUN useradd -U -d /home/nixbld -s /bin/bash -m nixbld

RUN mkdir -m 0755 /nix && chown nixbld /nix
COPY nix-1.11.2-x86_64-linux.tar.bz2 /nix
RUN cd /nix && tar xjf nix-1.11.2-x86_64-linux.tar.bz2 && su -c nix-1.11.2-x86_64-linux/install nixbld && rm -rf /nix/nix-1.11.2-x86_64-linux*
RUN su -l -c "nix-channel --update" nixbld

ENV     HOME       /home/nixbld
ENV     SHELL      /bin/bash
ENV     USER       nixbld
ENV     LOGNAME    nixbld

RUN su -l -c "nix-env -iA nixpkgs.git" nixbld
RUN su -l -c "cd && git clone https://github.com/escapewindow/signingscript.git && cd signingscript && git checkout nix" nixbld
RUN su -l -c "cd && nix-build signingscript/release.nix -A docker" nixbld
