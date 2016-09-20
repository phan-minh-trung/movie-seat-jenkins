
# Setting for movie-seat-pr
Folder : /var/jenkins_home/workspace/movie-seat-pr
Refs : +refs/pull/*:refs/remotes/origin/pr/*
Branch : origin/pr/${PR_ID}/merge

$ git fetch --tags --progress git@github.com:phan-minh-trung/movie-seat.git +refs/pull/*:refs/remotes/origin/pr/*
From github.com:phan-minh-trung/movie-seat
 * [new ref]         refs/pull/1/head -> origin/pr/1/head
 * [new ref]         refs/pull/1/merge -> origin/pr/1/merge
 * [new ref]         refs/pull/2/head -> origin/pr/2/head
 * [new ref]         refs/pull/2/merge -> origin/pr/2/merge
 * [new ref]         refs/pull/3/head -> origin/pr/3/head
 * [new ref]         refs/pull/3/merge -> origin/pr/3/merge

# Pull jenkins docker image
# https://hub.docker.com/r/library/jenkins/
$ docker pull jenkins

# Run jenkins docker
$ docker run -p 8080:8080 -p 50000:50000 -v /your/home:/var/jenkins_home jenkins

$ docker run -u root -m 4096M -p 8080:8080 -p 50000:50000 -v /Users/PhanMinhTRUNG/vagrant/movie-seat-jenkins/data:/var/jenkins_home minhtrung/movie-seat-jenk

# access ssh with root user
$ docker exec -i -t c376f464ae01 /bin/bash
root@c376f464ae01:/#

Store the jenkins data in folder: /Users/PhanMinhTRUNG/vagrant/movie-seat-jenkins/data

Account: trung|123456

# Show history of docker
$ docker history minhtrung/movie-seat-jenkins
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
a75b4aa6d994        45 seconds ago                                                      422.5 MB            update config movie-seat-master job
1da8e3651ec9        4 hours ago                                                         10.41 MB            add plugins
218a18fe1134        4 hours ago                                                         10.5 MB             init movie-seat-jenkin

# Scripts install composer and config php tools
rm -rf composer.lock
composer install
PROJECTPATH=`pwd -P`
export PATH=$PATH:$PROJECTPATH/vendor/bin    ???

# Check code with PHP tools:
PHP Code Coverage
PHP Code Sniffer
PHP Lines of Code
PHP Copy Past Detector
PHP Mess Detector
PHP Unit

# Global installation of PHP tools with Composer
https://akrabat.com/global-installation-of-php-tools-with-composer/
$ composer require phpunit/phpunit
$ composer require sebastian/phpcpd
$ composer require phploc/phploc
$ composer require phpmd/phpmd
$ composer require squizlabs/php_codesniffer
$ composer require phpunit/php-code-coverage

# Plugins
git
checkstyle
clover php plugin
dry
jdepend plugin
plot plugin
pmd plugin
violations

# Install PHP packages
apt-get update && apt-get install -y python-software-properties software-properties-common
LC_ALL=C.UTF-8 apt-add-repository ppa:ondrej/php
apt-get update
apt-get -y -f install php5-cli php5-dev php5-curl curl php-pear ant

# Install composer phar
php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer

# Install packages
export TERM=xterm
$ apt-get install -y curl sudo nano

# Change the machine from the default 1cpu/2048MB RAM run:

docker-machine stop
VBoxManage modifyvm default --cpus 2
VBoxManage modifyvm default --memory 4096
docker-machine start


