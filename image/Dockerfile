#
# garethhowell/docker-multimarkdown-6
#
# This is an image with an installation of multimarkdown
# Source: http://github.com/garethhowell/docker-multimarkdown-6/
# License: GNU GENERAL PUBLIC LICENSE, Version 3, 29 June 2007
# The license applies to the way the image is built, while the
# software components inside the image are under the respective
# licenses chosen by their respective copyright holders.
#
FROM ubuntu:20.10
LABEL maintainer=https://github.com/garethhowell

ENV LANG=C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive

RUN echo "Initial update." &&\
    apt-get update &&\
# prevent doc and man pages from being installed
# the idea is based on https://askubuntu.com/questions/129566
    echo "Preventing doc and man pages from being installed." &&\
    printf 'path-exclude /usr/share/doc/*\npath-include /usr/share/doc/*/copyright\npath-exclude /usr/share/man/*\npath-exclude /usr/share/groff/*\npath-exclude /usr/share/info/*\npath-exclude /usr/share/lintian/*\npath-exclude /usr/share/linda/*\npath-exclude=/usr/share/locale/*' > /etc/dpkg/dpkg.cfg.d/01_nodoc &&\
# remove doc files and man pages already installed
    rm -rf /usr/share/groff/* /usr/share/info/* &&\
    rm -rf /usr/share/lintian/* /usr/share/linda/* /var/cache/man/* &&\
    rm -rf /usr/share/man &&\
    mkdir -p /usr/share/man &&\
    find /usr/share/doc -depth -type f ! -name copyright -delete &&\
    find /usr/share/doc -type f -name "*.pdf" -delete &&\
    find /usr/share/doc -type f -name "*.gz" -delete &&\
    find /usr/share/doc -type f -name "*.tex" -delete &&\
    (find /usr/share/doc -type d -empty -delete || true) &&\
    mkdir -p /usr/share/doc &&\
    mkdir -p /usr/share/info &&\
# get and update certificates, to hopefully resolve mscorefonts error
    echo "Get and update certificates for mscorefonts." &&\
    apt-get install -f -y --no-install-recommends ca-certificates &&\
    update-ca-certificates &&\
# install utilities
    echo "Installing utilities." &&\
    apt-get install -f -y --no-install-recommends build-essential git cmake apt-utils &&\
# install MultiMarkdown
    cd /tmp/ &&\
    echo "Installing MultiMarkdown-6" &&\
    git clone https://github.com/fletcher/MultiMarkdown-6.git &&\
    cd MultiMarkdown-6 &&\
    make &&\
    cd build &&\
    make install &&\
    echo "Final cleanup." &&\
    apt-get clean -y &&\
    rm -rf /tmp/* /var/tmp/* &&\
    rm -rf /var/lib/apt/lists/* &&\
    rm -f /etc/ssh/ssh_host_* &&\
    find /usr/share/doc -depth -type f ! -name copyright -delete &&\
    find /usr/share/doc -type f -name "*.pdf" -delete &&\
    find /usr/share/doc -type f -name "*.gz" -delete &&\
    find /usr/share/doc -type f -name "*.tex" -delete &&\
    find /usr/share/doc -type d -empty -delete &&\
    rm -rf /usr/share/man &&\
    mkdir -p /usr/share/man &&\
    mkdir -p /usr/share/doc &&\
    echo "All done."


