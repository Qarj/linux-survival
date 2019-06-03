# crontab

list
```
crontab -l
```

edit
```
crontab -e
```

changed editor
```
select-editor
```

delete all
```
crontab -r
```

edit for another user
```
crontab -u username -l r
```

fields
```
Minute  Hour    Date    Month           DOW(Day of Week)
0-59    0-23    1-31    1-12 JAN-DEC    0-7 SUN-SAT
*       *       *       *               *
12,46   1,2,20  7,29    MAR,AUG         3,5
34-56/2
```
/2 is step value, every 2 minutes from 34 to 56 minutes

Every hour
```
0       *       *       *               *
```

Run script every hour
```
22      *       *       *               *   /home/tim/git/addons/TSM4/AppData.lua_updater.sh
```


Every 5 mins
```
*/5     *       *       *               *
```

Note that Date and Day Of Week fields are logically ORd i.e. if one true, job will be run

Every 90 minutes
```
0       */3     *       *               *
30      1/3     *       *               *
```

23:30 on the last day of every month
```
test $(date -d tomorrow +%d) -eq 1 && echo "tomorrow is the first day of the month"
```
```
30      23      28-31   *               *   test $(date -d tomorrow +%d) -eq 1 && /usr/local/run_my_script.sh
```


Debug
```
echo $(whoami)
echo $SHELL
echo $PATH
env
```

Set env variables in crontab
```
PATH=path1:path2:path3
SHELL=/bin/bash
MAILTO=me@email.com
```

Launch FireFox from cron
```
export DISPLAY=:0
firefox
```

Location of crontabs
```
sudo cat /var/spool/cron/crontabs/tim
```

Activity log
```
grep cron /var/log/syslog | tail -n 2
```

System wide crontab
```
vim /etc/crontab
```

Optional Allow & Deny lists for cron jobs - one username per line
```
vim cron.allow
vim cron.deny
```

For crontabs that need to run as root - put them in `/etc/cron.d`
This means you can change shell and path on a case by case basis without affecting the system wide one.

Edit the crontab for the root user
```
sudo crontab -e
```