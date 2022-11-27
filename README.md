# paramount
Seafile with backup 
1. wget https://github.com/haiwen/seafile-server-installer/raw/master/seafile-9.0_ubuntu
2. apt-get update
3. apt-get install -y python3 python3-setuptools python3-pip python3-ldap memcached openjdk-8-jre libmemcached-dev libreoffice-script-provider-python libreoffice pwgen curl nginx libmysqlclient-dev
4. python3 -m pip install --upgrade pip
5. python3 -m pip install Pillow
6. pip3 install --timeout=3600 django==3.2.* future mysqlclient pymysql pylibmc captcha markupsafe==2.0.1 jinja2 sqlalchemy==1.4.3 psd-tools django-pylibmc django-simple-captcha pycryptodome==3.12.0 cffi==1.14.0 lxml
8. bash seafile-9.0_ubuntu 9.0.9
9. Choose CE
10. ssh-keygen -o
11. cp ~/.ssh/id_rsa.pub to server backup
12. backup mysql
13. mysqldump  -uroot -p[pasword] --opt ccnet_db > /opt/seafile/seafile-data/db/ccnet_db.sql.`date +"%Y-%m-%d-%H-%M-%S"`
14. mysqldump  -uroot -p[pasword] --opt seafile_db > /opt/seafile/seafile-data/db/seafile_db.sql.`date +"%Y-%m-%d-%H-%M-%S"`
15. mysqldump  -uroot -p[pasword] --opt seahub_db > /opt/seafile/seafile-data/db/seahub_db.sql.`date +"%Y-%m-%d-%H-%M-%S"`
16. git clone https://github.com/laurent22/rsync-time-backup.git
17. cd rsync-time-backup
18. ./rsync_tmbackup.sh --port 22 --strategy 1:1  /opt/seafile/seafile-data ubuntu@ipserverbackup:/home/ubuntu/seafile
19. crontab -e
20. 0 23 * * * ./rsync_tmbackup.sh --port 22 --strategy 1:1  /opt/seafile/seafile-data ubuntu@ipserverbackup:/home/ubuntu/seafile

In server backup
1. repeat step number 1-9
2. restore mysql
3. mysql -u[username] -p[password] ccnet-db < ccnet-db.sql.2013-10-19-16-00-05
4. mysql -u[username] -p[password] seafile-db < seafile-db.sql.2013-10-19-16-00-20
5. mysql -u[username] -p[password] seahub-db < seahub-db.sql.2013-10-19-16-01-05
6. cd /home/ubuntu/seafile
7. mv * /opt/seafile/seafile-data/
8. crontab -e
9. cd /home/ubuntu/seafile && mv * /opt/seafile/seafile-data/
10. josss
