move-all-by-ext
===============

Move all files with a certain file extension to a specific folder.

## Before Use ##

1. The user must indicate which folder s/he wants files moved to. By default it will be ~/Desktop/move-all-by-ext/ but this can be changed by editing the line which begins with `MOVE_TO=`

1. The user must indicate what file extension s/he wishes to search for. By default it will search for JPG but this can be changed by editing the line which begins with `EXT=JPG`

## Usage ##

Usage is very simple. Just invoke `move-all-by-ext.sh` followed by the name of the folder that you want to search. For example, if you wanted to find all JPG files in ~/Downloads/ you would use

	move-all-by-ext.sh ~/Downloads/
	
You can indicate several folders at once. Just separate them with a space.

	move-all-by-ext.sh ~/Downloads/ ~/Desktop/

## Notes ##

* Files will be matched regardless of case. For example, if you tell it to look for files which end with JPG it will find both 'FOO.JPG' and 'bar.jpg' or 'fuBar.JpG' as long as they are in the specified search folders. This is considered a feature.

* Extensions are matched exactly. So if you tell it to look for JPEG it will only find files which end with .JPEG or .jpeg but not .JPG. This is considered a feature.

* This script uses the Unix command `find` instead of Spotlight. This is considered a feature.

* The script will not overwrite files in the destination folder (MOVE_TO) by using the (OS X-specific) `-n` flag to the `/bin/mv` command. (The  `-i` flag would be more 'portable' but that was not a priority for me.) Not overwriting files is considered a feature, but **it should be noted that it is possible to run this script and for it not to move all matching files if moving one of the matching files would have resulting in overwriting existing files.**  The script *does* attempt to warn the user when that has happened by re-checking the search folder *after* moving files to see if any files still remain.

* This script will not tell the user when it did not find any matching files. This could be considered a bug by some, but if the point is to make sure that all matching files from one directory are moved to another, it seems like a fairly tame bug.

* This script uses the `-exec` flag in `find` rather than using `xargs`. This may be slightly less efficient, but it eliminates a potential point of failure and simplifies the core process, so this is considered a feature. 

* This script does not check for permission to move files from A to B. The `mv` command is perfectly capable of informing the user if insufficient privileges are encountered.


## Background ##

This script was written as a response to <http://apple.stackexchange.com/questions/90918/how-can-i-select-all-files-within-a-directory-with-subfolders>.