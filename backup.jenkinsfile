pipeline {
agentany
stages {
stage("BACKUP"){ steps{
sh """#!/bin/bash
pushdbackup_config
sudogitconfig --local user.email "kiranforprivate@gmail.com"
sudogitconfig --global user.name "kiranaaditya"
find .|xargsgitrm
popd
cp -v var/lib/jenkins/*xml $WORKSPACE/backup_config
pushdvar/lib/jenkins/
fori in \$( find jobs|grep config.xml ); do
mkdir -p $WORKSPACE/backup_config/`dirname \$i`
cp \$i $WORKSPACE/backup_config/`dirname \$i`
done
popd
cp -rfvvar/lib/jenkins/secret* $WORKSPACE/backup_config/
cp -rfvvar/lib/jenkins/user* $WORKSPACE/backup_config/
pushdbackup_config
find .|xargsgit add
sudogit commit -a -m"Jenkins Backup Job"
"""
}} //steps // stage
stage("PUSH"){ steps{
sshagent(["$GIT_CREDENTIAL_ID"]) {
sh "cdbackup_config&&git push origin HEAD:$BACKUP_BRANCH"
} // sshagent
}} //steps // stage
}} //stages // pipeline