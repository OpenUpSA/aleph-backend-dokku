Dockerfile deployment to Dokku of Aleph backend components
----------------------------------------------------------

Set the config variables.

`ALEPH_NAME` must be specific to this project because it's used as the ElasticSearch index name.

```
dokku config:set publicpeople-aleph-api \
    ALEPH_APP_NAME=publicpeople-aleph \
    ALEPH_OAUTH=true \
    ALEPH_OAUTH_KEY= \
    ALEPH_OAUTH_SECRET= \
    ALEPH_SECRET_KEY= \
    ALEPH_UI_URL=https://aleph.public-people.techforgood.org.za \
    ALEPH_API_URL=https://alephapi.public-people.techforgood.org.za \
    ALEPH_ADMINS=jbothma@gmail.com \
    AWS_ACCESS_KEY_ID= \
    AWS_SECRET_ACCESS_KEY= \
    ALEPH_ARCHIVE_TYPE=s3 \
    ALEPH_ARCHIVE_BUCKET=public-people-aleph \
    ALEPH_BROKER_URI=sqs:// \
    ALEPH_QUEUE_PREFIX=publicpeople-aleph- \
    ALEPH_DATABASE_URI=postgresql:// \
    ALEPH_ELASTICSEARCH_URI= \
    ALEPH_MAIL_FROM=noreply@public-people.techforgood.org.za \
    ALEPH_MAIL_HOST=smtp.sendgrid.net \
    ALEPH_MAIL_ADMIN=jbothma+publicpeople@gmail.com \
    ALEPH_MAIL_USERNAME=apikey \
    ALEPH_MAIL_PASSWORD= \
    ALEPH_MAIL_PORT= \
    ALEPH_LANGUAGES=en:afr
```

Configure the start command

```
dokku config:set publicpeople-aleph-api DOKKU_DOCKERFILE_START_CMD=gunicorn -w 2 -b 0.0.0.0:5000 --log-level info --log-file - aleph.manage:app
```