FROM alt:p10

RUN \
	apt-get update && \
	apt-get -y install \
	bacula11-director-postgresql \
	bacula11 \
	&& apt-get clean \
	; mkdir /var/lock/subsys
	
RUN \
	sed -i -e '15c\  dbname = bacula' /etc/bacula/bacula-dir.conf \
	; sed -i -e '16c\  user = bacula' /etc/bacula/bacula-dir.conf \
	; sed -i -e '17c\  password = pg_bacula_db' /etc/bacula/bacula-dir.conf \
	; sed -i -e '18i\  dbport = 5432' /etc/bacula/bacula-dir.conf \
	; sed -i -e '19i\  dbaddress = 192.162.42.2' /etc/bacula/bacula-dir.conf \
	; sed -i '1c\Password = "bacula_boos"' /etc/bacula/bacula-dir-password.conf \
	; sed -i '1c\Password = "bacula_1_demon"' /etc/bacula/bacula-fd-password.conf \
	; sed -i '1c\Password = "bacula_frute_demon"' /etc/bacula/bacula-sd-password.conf
   	
RUN \
	apt-get install -y baculum11-postgresql \
	baculum11-apache2 \
	sudo

RUN \
	a2ensite baculum-api \
	; a2ensite baculum-web \
	; cd '/etc/httpd2/conf/mods-enabled/' \
	; a2enmod auth_basic \ 
	; a2enmod authn_core \
	; a2enmod authn_file \ 
	; a2enmod authz_core \
	; a2enmod authz_host \
	; a2enmod authz_user \
	; a2enmod mod_php7 \
	; a2enmod negotiation \
	; a2enmod rewrite \
	; a2enmod setenvif \
	; usermod -a -G bacula apache2 \
	; control sudo public \
	; echo "Defaults:apache2 "'!'"requiretty" > /etc/sudoers.d/baculum \
	; echo "apache2 ALL=NOPASSWD: /usr/bin/bconsole" >> /etc/sudoers.d/baculum \
	; echo "apache2 ALL=NOPASSWD: /usr/sbin/bdirjson" >> /etc/sudoers.d/baculum \
	; echo "apache2 ALL=NOPASSWD: /usr/sbin/bsdjson" >> /etc/sudoers.d/baculum \
	; echo "apache2 ALL=NOPASSWD: /usr/sbin/bfdjson" >> /etc/sudoers.d/baculum \
	; echo "apache2 ALL=NOPASSWD: /usr/sbin/bbconsjson" >> /etc/sudoers.d/baculum
	
EXPOSE 9101:9101 9102:9102 9095:9095 9096:9096

CMD  service bacula-dir start; service bacula-fd start; service bacula-sd start; service httpd2 start && bash





