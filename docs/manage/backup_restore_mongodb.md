# Managing backup and restore of MongoDB
___

**Issue**: https://github.com/fabmob/e-mission-phone-fabmob/issues/29

## Actual configuration

Since July 22, 2019, every Monday at 6 AM, a script will perform a backup of `Stage_database` into `/var/emission/backup/`. The backup will be compressed in `.gzip` and will be named `Stage_database-<date>.gzip`. 

## How to backup manually

We can use the command `mongodump` to backup all the databases of MongoDB. However, the database might be pretty heavy so it might be interesting to compress the backup. We can compress the backup file using `--gzip --archive=archivename`options.

```bash
$ mongodump --gzip --archive=archivename`
```

## How to backup using the script

To backup using `mongo_backup_weekly.py` we can specify two arguments the output path and the database to backup. If there is no arguments or only one, the script will use a default configuration (`Stage_database`for the database and `/var/emission/backup` for the output file). We can use the script as below: 

```bash
$ python mongo_backup_weekly.py -o /var/emission/backup/ -d Stage_database
```

The output file will be compressed. 

## How to restore

To restore the database, we will use the command `mongorestore` with the same argument as the `mongodump` command.

```bash
$ mongorestore --gzip --archive=archivename --drop
```

The `--drop` is optional but useful if we want a clean restore. 