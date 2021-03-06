# Back data from Mongo on S3

This repo contains script to backup your MongoDB databases and store them on Amazon S3.

It generates a dump from your MongoDB databases, compresses this dump as tar.bz2, generates a hash file for integrity check and then uploads both files to your Amazon S3 bucket.

In order to test it, be sure to have the following dependencies installed on your system:

- MongoDB installed and running
- [yarn](https://yarnpkg.com/)
- [docker](https://www.docker.com)
- [docker-compose](https://docs.docker.com/compose/install/)

Before running anything, please configure your AWS credentials inside the .env file.

You can run the backup script directly on your system and [configure cron by yourself](https://corenominal.org/2016/05/12/howto-setup-a-crontab-file/) or use the Docker config provided. 

In order to start the Docker container and configure cron inside of it to run the script every day at 00:00 CET, run:

```
$ make
```

In order to start this container automatically if your server reboots:

- Change the path inside the file infra/host/etc/systemd/system/mongo-backup.service to be the path where you put the mongo-s3-backup source code.
- As root, copy this file to /etc/systemd/system in your server
- Enable and start it:

```
# systemctl enable mongo-backup
# systemctl start mongo-backup
```

If you don't want to use Docker, just run instead:

```
$ make no-docker
```

And then configure the script directly on your system's cron.