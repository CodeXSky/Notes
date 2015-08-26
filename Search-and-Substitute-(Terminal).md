### Search
* `grep` - full text search (ie. `history | grep "hello"`). You can also use `grep` in a file and it will get the lines containing your search term (ie. `greb “Moby Dick” pg2701.txt`).
* control-r - reverse search through history (? Not sure what this does)

### Substitute
These are substitute commands, or variations of the command, but I haven't used them that much, so I'm not too sure how correct they are.
* `sed` - substitute (ie. `sed ‘s/day/night/’ 24hr.txt` or `sed -i` (in place, so it actually replaces the content of the file) `‘s/day/night/’ 24hr.txt` or `sed -i “” ‘s/day/night/’ 24hr.txt` or `sed -e ‘s/ /\’$’\n/g’ result_animal.txt > result_animal_tokenized.txt`

### Other
* `xargs` - passes the arguments (ie. `find . -name “*.pdf” -print0 | xargs -0 lp -o fit-to-page`).
* `wc` - word count (ie. `grep “whale” pg2701.txt | wc`).
* `uniq - c` - find unique and count.