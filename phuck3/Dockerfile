FROM ubuntu:latest

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get -y update
RUN apt-get -y install apache2 apt-transport-https curl php libapache2-mod-php vim-common unzip 

ADD webroot /var/www/html/
RUN rm /var/www/html/index.html
RUN chown -R root:root /var/www/html/
ADD flag /
RUN chmod -r /tmp

RUN sed -i '/^disable_functions/ s/$/mail,exec,passthru,shell_exec,system,proc_open,popen,pcntl_exec,posix_mkfifo, pg_lo_import, dbmopen, dbase_open, popen, chgrp, chown, chmod, symlink,apache_setenv,define_syslog_variables, posix_getpwuid, posix_kill, posix_mkfifo, posix_setpgid, posix_setsid, posix_uname, proc_close, pclose, proc_nice, proc_terminate,curl_exec,curl_multi_exec,parse_ini_file,show_source,imap_open,imagecolormatch,fopen,copy,rename,readfile,readlink,tmpfile,tempnam,touch,link,file_put_contents,file,ftp_connect,ftp_ssl_connect,/' /etc/php/7.2/apache2/php.ini
RUN sed -i '/^disable_classes/ s/$/SplFileObject,SplFileInfo,SplTempFileObject,SessionHandler/' /etc/php/7.2/apache2/php.ini
RUN sed -i 's/^;open_basedir =/open_basedir =\/var\/www\/html\//g' /etc/php/7.2/apache2/php.ini

# disable /server-status
RUN a2dismod status

CMD service apache2 start;  /bin/bash
