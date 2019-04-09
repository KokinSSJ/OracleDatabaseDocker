# OracleDatabaseDocker

HOW TO RUN Oracle database and setup HR sample database on docker
1. Create volume: 
	docker volume create oracle12c-test
2. build image 
	a. download repo https://github.com/oracle/docker-images
	b. go to OracleDatabase/SingleInstance/dockerfiles
	c. download database (12c / 11g, EE/SE/XE) and put into appriopriate catalog
	d. run buildDckerImages.sh 
3. Run image and wait for initialization
	docker run --name oracle12c-test -e ORACLE_PWD=admin123 -p 1521:1521 -p 5500:5500 -v oracle12c-test:/opt/oracle/oradata oracle/database:12.2.0.1-ee
4. Install perl on container (via dockerfile can be done too)
	docker exec -it -u root --workdir / oracle12c-test /bin/sh
	yum install perl
5. setup ORACLE_PID and ORACLE_PID for sqlplus connected from container (this can be done also via env when docker run)
	docker exec -it oracle12c-test bash
	export ORACLE_SID=ORCLCDB
	export ORACLE_PID=ORCLPDB1
6. install / add HR sample user + database
	sqlplus / as sysdba
	@hr_main.sql  --> https://github.com/oracle/db-sample-schemas https://docs.oracle.com/database/121/COMSC/installation.htm#COMSC00004
7. connect via sqldeveloper
	a. to whole database -> username: sys as sysdba / pass: check $ORACLE_PWD / SID: ORCLCDB
	b. to hr database -> username: hr / pass: during creation / user SERVICE rather than SID -> SERVICE=ORCLPDB1
 
 
 
 
