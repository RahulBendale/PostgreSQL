Step 1: Install pgbouncer

yum install pgbouncer

Step 2: change ownership root into postgres user

cd /etc/
chown -R postgres:postgres pgbouncer

cd pgbouncer
ls -lrth
chmod 775 *
ls -lrth


Step 3: Edit pgb file through and change parameters

su postgres
vi /etc/pgbouncer/pgbouncer.ini

touch /etc/pgbouncer/userlist.txt

psql
\du
list of available db users shown here

select md5('postgres');

select md5('postgres MD5');

vi userlist.txt
"postgres" "--------"
"ram" "----------"

sudo systemctl start pgbouncer

check the pgb status

ps -ef|grep pgb

[databases]
YOUR-DBNAME = host=YOUR-HOST port=5432 dbname=YOUR-DBNAME
*=host=localhost port=5432 ==> all database
[pgbouncer]
listen_addr = *
listen_port = 6432

auth_type = md5
auth_file = /etc/pgbouncer/userlist.txt

admin_users = postgres
stats_users = postgres

pool_mode = transaction/session
server_reset_query =DISCARD ALL

max_client_conn = 1000 default =100
default_pool_size = 20 default=20
log_connections = 1
log_disconnections = 1
log_poooler_errors = 1

server_reset_query = DISCARD ALL;
server_check_query = select 1
server_check_delay =10


Step 4: Create a userlist file

/etc/pgbouncer/userlist.txt


step 5: Connect DB and create MD5 file 

\du

select md5 ('username MD5');

