# backup-mongo-to-s3
A module that makes database backup and uploads to s3.

# INTRODUCTION

This module involves the following steps.
1. Make DB backup on disk.
2. Make a zip file out of localbackup.
3. Delete the local-backup directory.
4. Upload the zip file to s3.
5. Delete zip file, if '***keepLocalBackups***' parameter is not set to true.
6. Delete outdated cloud backup zip files, outdated refers to zip files older than the latest '***noOfTotalBackups***'.

# USAGE

1. Require the module.
2. Use the init method to pass argument object.
3. Use the start method to start the process.
4. Compatible with cron-job to schedule backup-process.


# PARAMETERS

* ***mongodbUri***       : MANDATORY | <string>    | e.g. "localhost:27017"
* ***backupDir***        : MANDATORY | <string>    | e.g. "/tmp/backupDir"                    => The path to the directory, where localDB will be dumped.
* ***zipPath***          : MANDATORY | <string>    | e.g. '/tmp/backup.zip'                   => The path where the backupDir is zipped to.
* ***key***              : MANDATORY | <string>    | e.g. "jfdasdlkfjfdak3al2lkasdfjlk"       => aws s3 key value.
* ***secret***           : MANDATORY | <string>    | e.g. "fdjaksdf_e34jk53wlksdj2092jk"      => aws s3 secret value.
* ***region***           : MANDATORY | <string>    | e.g. 'us-southwest-01'                   => the region name of the s3 bucket. 
* ***bucket***           : MANDATORY | <string>    | e.g. 'scheduled-backups'                 => The name of the bucket, where backup zips will be posted to.
* ***dir***              : MANDATORY | <string>    | e.g. 'backupDir'                         => The directory in the bucket, where zips are stored into.
* ***name***             : OPTIONAL  | <string>    | default : 'backup'                       => The alias with which we want to store our backup.zip by.
* ***debugMode***        : OPTIONAL  | <boolean>   | default : false                          => Enable logs from module, if false, module simply throws.
* ***keepLocalBackups*** : OPTIONAL  | <boolean>   | default : false                          => retain or delete localBackup.
* ***noOfTotalBackups*** : OPTIONAL  | <number>    | default : 7                              => The no. of latest n-backup to keep, older ones are automatically deleted.


# EXAMPLE

```
const module = require ('backup-mongo-to-s3');

// Take note of the MANDATORY and OPTIONAL parameters.
const config = {
		mongodbUri       : <string>,
		backupDir        : <string>,
		zipPath          : <string>,
		keepLocalBackups : <boolean>,
		noOfTotalBackups : <number>,
        debug            : <boolean>,

		s3         : {
			key     : <string>,
			secret  : <string>,
			region  : <string>,
			bucket  : <string>,
			name    : <string>,
			dir     : <string>,
		},
	};

module.init (config);

module.start ();
```
