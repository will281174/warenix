# Quickstart #

1) Create an account at http://openshift.redhat.com/

2) Create a python application and attach mongodb to it:

rhc app create -a gcm -t python-2.6
rhc app cartridge add -a gcm -c mongodb-2.0

3) Add this upstream repo

cd gcm
git remote add upstream -m master git://github.com/openshift/gcm.git
git pull -s recursive -X theirs upstream master

4) Then push the repo upstream

git push

5) That's it, you can now browse to your application at:

http://gcm-$yournamespace.rhcloud.com

# Testing locally #

1) cd gcm

2) virtualenv venv develop

3) source venv/bin/activate

4) export locals
```
export OPENSHIFT_APP_NAME="gcm"
export OPENSHIFT_GEAR_NAME="gcm"
export OPENSHIFT_NOSQL_DB_HOST="<your_mongo_db_ip>"
export OPENSHIFT_NOSQL_DB_PASSWORD="<your_mongo_db_password>"
export OPENSHIFT_NOSQL_DB_PORT="27017"
export OPENSHIFT_NOSQL_DB_TYPE="mongodb"
export OPENSHIFT_NOSQL_DB_URL="mongodb://admin:<your_mongo_db_password@<your_mongo_db_ip>:27017/"
export OPENSHIFT_NOSQL_DB_USERNAME="admin"
```

5) rhc-port-forward -a gcm

6) python wsgi/app.py

# Web APIs #
## Apps ##
```
/gcm/apps/register?app_id=<app_id>&api_key=<api_key>
```

## Devices ##
```
/gcm/devices/register?app_id=<app_id>&reg_id=<reg_id>
/gcm/devices/unregister?app_id=<app_id>&reg_id=<reg_id>
/gcm/devices/unpdate?app_id=<app_id>&reg_id=<reg_id>&new_reg_id=<new_reg_id>
```

## GCM ##
```
/gcm/send/?app_id=<app_id>
POST body:
Content-Type: application/json
{
"data":"hello",
"reg_id_list":["<reg_id_1>", "<reg_id_2>"]
}
```