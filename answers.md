//
# answers.md — Linux Fundamentals & DevSecOps Lab


### Q1
pwd
whoami
uname -a
### Q2
ls /
### Q3
ls ~
ls -la ~
### Q4
mkdir -p ~/projects/cyphercore/{configs,logs/{access,errors,archive},reports}
tree ~/projects/cyphercore
### Q5
cd ~/projects/cyphercore/
touch configs/app.conf configs/db.conf logs/access/access.log logs/errors/error.log reports/weekly_report.txt
### Q6
ls -lh configs/
### Q7
 cd /projects/cyphercore
### Q8
echo "2025-06-02 08:14:33 INFO  Application started successfully" >> logs/access/access.log
echo "2025-06-02 08:14:55 WARN  High memory usage detected: 87%" >> logs/access/access.log
echo "2025-06-02 08:15:10 ERROR Database connection timeout — retrying (attempt 1/3)" >> logs/access/access.log
cat logs/access/access.log

overwrite test run
echo "2025-06-02 08:14:33 INFO  Application started successfully" > logs/access/access.log
cat logs/access/access.log

 
echo "2025-06-02 08:14:55 WARN  High memory usage detected: 87%" >> logs/access/access.log
echo "2025-06-02 08:15:10 ERROR Database connection timeout — retrying (attempt 1/3)" >> logs/access/access.log

### Q9
cat logs/access/access.log
tac logs/access/access.log
tail logs/access/access.log

### Q10
cat << 'EOF' >> logs/errors/error.log
2025-06-02 08:15:10 ERROR    Database connection timeout — retrying (attempt 1/3)
2025-06-02 08:15:13 ERROR    Database connection timeout — retrying (attempt 2/3)
2025-06-02 08:15:16 CRITICAL Database connection failed — all retries exhausted
2025-06-02 08:15:16 CRITICAL Triggering failover to secondary DB at 10.0.0.52
EOF
cat logs/errors/error.log

 
DBNAME=cyphercore

 
cat << EOF
The target deployment database name is $DBNAME
EOF
 
cat << 'EOF'
The target deployment database name is $DBNAME
EOF
### Q11
more logs/errors/error.log
less logs/errors/error.log

### Q12
cp logs/errors/error.log logs/archive/error_2025-06-02.log
mv logs/access/access.log logs/access/access_2025-06-02.log
ls -l logs/access/

### Q13
mkdir reports/temp_drafts
rmdir reports/temp_drafts
rmdir logs/
### Q14
tree ~/projects/cyphercore

### Q15
cat << 'EOF' > configs/db.conf
DB_HOST=10.0.0.10
DB_PORT=5432
DB_NAME=cyphercore_prod
EOF
ln configs/db.conf configs/db_hardlink.conf
ls -li configs/

### Q16
rm configs/db.conf
cat configs/db_hardlink.conf
ls -li configs/

### Q17
echo "APP_ENV=staging" > configs/app.conf
ln -s ~/projects/cyphercore/configs/app.conf ~/projects/cyphercore/app_config_link
ls -l ~/projects/cyphercore/
rm configs/app.conf
cat ~/projects/cyphercore/app_config_link

### Q18
shares inode with original -hard link
works across different filesystems - soft link
survives deletion of original - hard link
can link to a directory - soft link
shows as l in ls-la - soft link
detectable by matching inodes in ls-la - hard link 


### Q19
ls logs/ missing_folder/ > reports/stdout_output.txt 2> reports/stderr_output.txt
cat reports/stdout_output.txt
cat reports/stderr_output.txt

Stream Multiplex Pipeline Run
ls logs/ missing_folder/ 2>&1 

### Q20
cat << EOF > reports/weekly_report.txt
========================================
WEEKLY SECURITY REPORT — CypherCore Systems
Week Ending: 2025-06-06
Prepared By: Kofi
========================================

SUMMARY:
No critical incidents recorded this week.
One WARN: memory usage spike at 08:14 on 2025-06-02.
One CRITICAL: DB connection failure at 08:15 on 2025-06-02.
Failover to secondary DB executed successfully.

RECOMMENDED ACTION:
Review DB connection pool settings before next deployment.
========================================
EOF

cat reports/weekly_report.txt

Post Analyst Verification Run
ANALYST="Kofi"
cat << EOF
Unquoted Test -> Analyst: $ANALYST
EOF

cat << 'EOF'
Quoted Test -> Analyst: $ANALYST
EOF

### Q21
tree ~/projects/cyphercore

