---
description: Manage schedule in magento2
---

# Install Phar File

Download and Install Phar File

open wsl

```
cd ~/Documents/magento2
```

```
docker compose run deploy
```

Download the latest stable N98-Magerun phar-file from the file-server:

```
curl -O https://files.magerun.net/n98-magerun2.phar
```

Now you can make the phar-file executable:

```
chmod +x ./n98-magerun2.phar
```

The base-installation is now complete and you can verify it:

```
./n98-magerun2.phar --version
```

The command should execute successfully and show you the version number of N98-Magerun like:

```
n98-magerun2 version 4.8.0 by netz98 GmbH
```

If you want to use the command system wide you can copy it to /usr/local/bin.

```
sudo cp ./n98-magerun2.phar /usr/local/bin/
```

You can list all available commands by:

```
./n98-magerun2.phar list
```

**Note:**

* using `./n98-magerun2.phar sys:cron:list` to watch list schedule.
* using `service cron status` to check cron is running ?
* using `service cron start` to run cron
* using `service cron stop` to stop cron.

**Scheduling Cron Jobs with Crontab:** [https://linuxize.com/post/scheduling-cron-jobs-with-crontab/](https://linuxize.com/post/scheduling-cron-jobs-with-crontab/)
