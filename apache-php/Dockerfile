# =============================================================================
#
# CentOS-7, Apache 2.4, PHP-FPM 7.2,
#
# =============================================================================
FROM centos:7

LABEL maintainer="henry@cajanegra.com.ec"

# -----------------------------------------------------------------------------
# Additional repositories
# -----------------------------------------------------------------------------
RUN yum -y install \
    http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
    http://rpms.famillecollet.com/enterprise/remi-release-7.rpm \
    yum-utils yum-plugin-ovl nss curl ethtool hostname man man-pages man-db mlocate rsync tar unzip htop vim vimdiff which wget && \
    yum-config-manager --enable remi, remi-php72, remi-php72-debuginfo

# -----------------------------------------------------------------------------
# Apache
# -----------------------------------------------------------------------------
RUN yum install -y httpd

# -----------------------------------------------------------------------------
# PHP
# -----------------------------------------------------------------------------
RUN yum install -y \
    php \
    php-bcmath \
    php-cli \
    php-common \
    php-devel \
    php-gd \
    php-gmp \
    php-imap \
    php-mbstring \
    php-mcrypt \
    php-mysqlnd \
    php-newrelic \
    php-pdo \
    php-pear \
    php-pecl-imagick \
    php-pecl-jsonc \
    php-pecl-jsonc-devel \
    php-pecl-memcache \
    php-pecl-ssh2 \
    php-pecl-zip \
    php-process \
    php-runtime \
    php-soap \
    php-tcpdf \
    php-tidy \
    php-xml \
    php-xmlrpc

# -----------------------------------------------------------------------------
# GIT
# -----------------------------------------------------------------------------
RUN yum install -y git 

# -----------------------------------------------------------------------------
# Composer
# -----------------------------------------------------------------------------
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer

# -----------------------------------------------------------------------------
# Install NodeJS
# -----------------------------------------------------------------------------
RUN yum install -y yum-plugin-ovl
RUN yum install -y gcc gcc-c++ make
RUN curl -sL https://rpm.nodesource.com/setup_6.x | bash -
RUN yum install -y nodejs

# -----------------------------------------------------------------------------
# Phantomjs configuration
# -----------------------------------------------------------------------------
COPY config/phantomjs /bin/phantomjs
RUN chmod 777 /bin/phantomjs
RUN chmod 777 /tmp

# -----------------------------------------------------------------------------
# Remove packages, reduces container size
# -----------------------------------------------------------------------------
RUN rm -rf /var/cache/yum/* && yum clean all

# -----------------------------------------------------------------------------
# Timezone
# -----------------------------------------------------------------------------
ENV TIMEZONE America/Guayaquil
RUN rm -f /etc/localtime && \
    ln -s /usr/share/zoneinfo/${TIMEZONE} /etc/localtime

# -----------------------------------------------------------------------------
# Project root
# -----------------------------------------------------------------------------
RUN mkdir -p /var/www/leadsgenerator && \
    rm -rf /var/www/html && \
    ln -s /var/www/leadsgenerator /var/www/html

# -----------------------------------------------------------------------------
# Virtual host configuration
# -----------------------------------------------------------------------------
COPY config/httpd.conf /etc/httpd/conf/httpd.conf
COPY config/hosts /etc/hosts

# -----------------------------------------------------------------------------
# PHP ini
# -----------------------------------------------------------------------------
COPY config/php.ini /etc/php.ini

# -----------------------------------------------------------------------------
# DB-select txt
# -----------------------------------------------------------------------------
COPY config/db-select.txt /var/www/db-select.txt

# -----------------------------------------------------------------------------
# Listen ports
# -----------------------------------------------------------------------------
EXPOSE 80 3000 3002 3003 3004 3005

# -----------------------------------------------------------------------------
# Workdir
# -----------------------------------------------------------------------------
WORKDIR /var/www/leadsgenerator

# -----------------------------------------------------------------------------
# Run container
# -----------------------------------------------------------------------------
RUN rm -rf /run/httpd/* /tmp/httpd*
CMD [ "apachectl", "-D", "FOREGROUND"]