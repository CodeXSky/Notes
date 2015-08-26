### Getting Notifications from Terminal:
* First you need to install the tool. To do it through [homebrew](http://brew.sh/) just type `brew install terminal-notifier`.
* `terminal-notifier -message "message here" -title "title of message"` - this is the basic command.
* If you want to get a message once a process is finished you will need something like this: `processCommand; notificationCommand`.