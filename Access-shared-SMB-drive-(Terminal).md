### Access shared SMB drive
* To list all the drives available for a specific user user `smbutil view //user@host`.
* Next you have to create a folder where you are going to mount your drive. In my case I do `mkdir /Volumes/driveName`.
* Finally, to mount the drive you do `mount -t smbfs //user@host/driveToMount /Volumes/driveName`.
* To unmount drive use `umount /Volumes/driveName`.