### Prevent the computer from sleeping
* `caffeinate` - This will keep the computer awake even if you close the lid. **Do not do this with computer inside a bag as it might get too hot**.
* `caffeinate -u -t 500` - This will keep the computer awake for 500 seconds.
* `caffeinate -i "make"` - This will keep your computer awake till it finishes with the "make" command.

### Create a local server
* `python -m SimpleHTTPServer` - this will create a local server. To access it, just open a browser window and go to `http://localhost:8000/`

### Check uptime
* `uptime` - this will return current time, plus uptime.

### Measure time of an operation
* Add `time` at the beginning of the command.

### Math operations
* `bc` - allows you to do math calculations.

### Rebuild the locate database
* `sudo /usr/libexec/locate.updatedb` - this will do it. It will take some time.

### Miscellaneous
* try this sometime `telnet towel.blinkenlights.nl`

### Monitor activity
* `top -o cpu -s 2 -i 5` will show the top processes ordered by cpu usage (`o`), refreshed every 2 seconds (`-s 2`) using 5 second intervals (`-i 5`)

### Printing from terminal
* The basic command is `lp document_name`
* To print to a specific destination (printer) use `lp -d printer_name document_name`