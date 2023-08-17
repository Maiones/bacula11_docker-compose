FROM alt:p10

RUN \
	apt-get update && \
	apt-get -y install \
	bacula11-client \
	&& apt-get clean \
	; mkdir -p /var/lock \
	; mkdir /var/lock/subsys/
	
EXPOSE 9101:9101 9102:9102

#Меняем по умолчанию имя клиента с fd на fd2..
RUN \
	sed -i '1c\Password = "bacula_boos"' /etc/bacula/bacula-dir-password.conf \
	; 	sed -i '1c\Password = "bacula_1_demon"' /etc/bacula/bacula-fd-password.conf \
	;  sed -i 's/Name = fd/Name = fd2/g' /etc/bacula/bacula-fd.conf

CMD  service bacula-fd start && bash

#(!проверить разрешение примонтируемой папки root:bacula)
#docker run -d -p 9101:9101 -p 9102:9102 -v /home/user/docker/bacula11_clent/bacula/:/mnt/ --name bacula_11_client -it IMAGE_ID