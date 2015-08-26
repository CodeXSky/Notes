### Backing up files to another drive
* `rsync -avzh --delete` - Synchronizes in archive form, verbose and keeps attributes. If you want to see the progress of each file you can add the flag `P` (although this is mostly useful when dealing with large files).
**Careful cause it overwrites.**
* The flag `n` is to do a "dry run".
* Also, the trailing `/` is important, otherwise you might create another folder within the destination folder and duplicate everything. An example of a correct usage is `rsync -avzh --delete SIDL/01_Personal_Projects/ destination/SIDL/01_Personal_Projects/`
* An example of this using a remote destination would look like this: `rsync -a ~/dir1 username@remote_host:destination_directory`

### Backing up to Google Drive
* First, download `gsync` which acts like `rsync` but communicates with Google Drive. You can find it [here](https://github.com/iwonbigbro/gsync).
* I had to do two fixes before it would work fine: issue [#69](https://github.com/iwonbigbro/gsync/issues/69) with the fix provided by Jeztucker and issue [#66](https://github.com/iwonbigbro/gsync/issues/66).
* `time gsync -p -o -g -v -r -l -s --delete ~/Documents/File/To/Transfer/ drive://Location/To/Transfer/To` - This is the command that I'm using. `-p` is permissions, `-o` is owner, `-g` is group, `-v` is verbose, `-r` is recursive, `-l` copies symlinks as symlinks (don't know what that is...), `-s` protects the arguments, `--progress` shows progress, and `--delete` deletes anything that's not there.