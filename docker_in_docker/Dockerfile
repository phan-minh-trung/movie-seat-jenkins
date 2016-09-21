FROM jenkins
MAINTAINER trungg.phan@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# Switch user to root so that we can install apps (jenkins image switches to user "jenkins" in the end)
USER root

# Install Docker prerequisites
RUN apt-get update -qq && apt-get install -qqy \
    apt-transport-https \
    apparmor \
    ca-certificates \
    lxc \
    supervisor \
    wget \
    curl \
    git \
    ant

# Create log folder for supervisor, jenkins and docker
RUN mkdir -p /var/log/supervisor
RUN mkdir -p /var/log/docker
RUN mkdir -p /var/log/jenkins

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Install Docker from Docker Inc. repositories.
RUN echo deb https://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list \
  && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9 \
  && apt-get update -qq \
  && apt-get install -qqy lxc-docker

# Add jenkins user to the docker groups so that the jenkins user can run docker without sudo
RUN gpasswd -a jenkins docker

# Install the magic wrapper
ADD ./wrapdocker /usr/local/bin/wrapdocker
RUN chmod +x /usr/local/bin/wrapdocker

# Install PHP packages
RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get update -q \
    && apt-get install -yq php5-cli php5-mysql php5-gd php5-intl php5-curl php5-xcache \
    && rm -rf /var/lib/apt/lists/* && rm -rf /var/cache/apt/*
RUN sed -i 's/xcache.size = 60M/xcache.size = 0/' /etc/php5/mods-available/xcache.ini

RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get update && apt-get install -y -f mysql-server mysql-client \
    && service mysql start \
    && mysqladmin -u root -h localhost password 'root' \
    && apt-get clean

# Install composer phar
RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer

CMD /usr/bin/supervisord -c /etc/supervisor/conf.d/supervisord.conf
