###Creating a Cron Job
* First, you need to open the crontab file. To do this use `env EDITOR=nano crontab -e`. This will open up the crontab file in Nano.
* Then type the timing sequence and the command to execute. The timing sequence works as follows:
* `0 11 * * *` - This will perform the job every day at 11am.
* The first space specifies the minute to run, the second the hour, the third the day of the month (1 - 31), the fourth the month of the year (1 - 12) and the fifth the day of the week (0 - 6, where 0 is Sunday and 6 Saturday).
* After the timing sequence goes your command. ie. `0 11 * * * /Users/juansaldarriaga/Documents/Reference\ Documents/05_Libraries_and_Scripts/./backup_02_Google_Drive.sh`.
* Then save (control-o) and exit nano (control-x). If everything was fine you should see a message that says `installing new crontab`.
* To list the current cron jobs, type `crontab -l`.
* A more detailed explanation can be found [here](http://www.maclife.com/article/columns/terminal_101_creating_cron_jobs).
* _Note: all the commands need to have absolute paths (ie. `/usr/local/bin/gsync`), otherwise cron won't be able to find them. The paths to the files also needs to be absolute._