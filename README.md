# Command_Line

•	Kernel = core app; allocates resources & talks to HW
uname -r (-a)
Latest: dnf list kernel
Install: dnf install kernel-devel --best 
sudo dnf update kernel  reboot sudo dnf –y update = update all 

•	Shell=app that interprets the commands 
Current: ps $$ or echo $0 
Default: echo “$SHELL” 
List: chsh -l or cat /etc/shells 
Change: chsh -s shell_name  log out 


•	Prompt = system symbol of cmd line (#,$,%,:) 
Continuation prompt: > (continuation of previous line) 
Breaking cmd in various lines: \ or | 
Separating 2 commands at one line: ; or && 


Basic Commands:

 
•	’ ’ - single quotes=do not touch this text
•	" " - double=perform shell variable expansión
•	/ = root directory
•	./ = current directory
•	../ = upper (parent) directory
•	~ = user home directory
•	.name = hidden dirs/files start with dot!
•	name~ = backup files
•	\ = escape character (split cmd line, special char) 
•	$ = preceding variable name (“\$” to print $)
•	$0 = name of the running process.
•	$(cmd) = cmd substitution
•	$((...)) = arithmetic expansion operator
•	# sizeof
•	| = pipeuse output of cmd 1 as input to cmd 2 
•	0< = stdin 1> = stdout 2> = stderr &>= stdout&err
stderr by default is going to the console as stdout 
cat < file > file_content 2> error_content 
•	> = stdout redirectionoverwriting the output file
•	>> = stdout redirectionappending to output file
•	< = take stdin from file (wc < file, <file wc, wc file, cat file | wc) 
•	2>&1 = redirect (add) errors to stdout
•	/dev/null = null device; discard all data & ret success 
•	` ` - evaluate & replace=cmd substitution (`≠‘) 
•	== $(cmd) BUT ≠ $cmd 
 








Listing Commands:

 
ls – print the contents of the current dir 
- 1 = 1 output per line
- s = size
- l = long = all information 
- a = all -> hidden directories/files start with dot! 
- H = follow symbolic links
- R = list subdirectories recursively
- d = do not enter inside directories 
- S = sort by file size
- t = sort by modification time, newest first 
- X = sort alphabetically by entry extensión
 - r = reverse order while sorting
Pattern matching @command line
 	* = match all files and subdirectories (show subdir content) 
*x = restrict to files and subdirectories starting with x
*x* = restrict to files and subdirectories containing with x 
*x = restrict to files and subdirectories ending with x The
* = any number of unknown characters,
? = only one unknown character
^ = negation (*(^/) = any pattern not having ”/” inside)
If restriction result is empty NO filter is used 
 

List just directories: ls -d *(/) ; ls -d */ ; echo */ 
List just files: ls -a *(^/)
List hidden dir/files = ls -ld .*
Get files/dirs with abs path: ls -d -1 $PWD/* 
For entering 2nd level: ls -d -1 $PWD/*/* 


Basic Commands

•	who - show who is logged on
•	man – short for manual (notice that zsh doesn’t have help command)
•	whoami - print user id
•	pwd - print current directory (= echo $PWD)
•	man cmd = manual (cmd -h or cmd --help) 
•	type cmd - type of a cmd tool
-a : all occurrences of cmd name 
•	which cmd - which binary are you executing?
•	which cmd vs sudo which python 
•	whereis cmd - location of the binary/source/man files
•	history – last 15 commands 
-100 = last 100 commands
-i = include all information 
	echo $HISTFILE  ~/.history
	!+number_hist_line (!!=repeat last cmd -> sudo !!) 
•	echo - send argument to stdout
-n = doesn’t add new line character 

•	cat - send content of file to stdout
-n = add number to all output lines 
•	head - show 10 first lines of file
-n K = first K lines instead of 10
-c K = first K bytes
-n/c -K = all but the last K lines/bytes 
•	tail - show last 10 lines of file
-n K = the last K lines instead of 10
-c K = last K bytes
-n/c +K = starting with K lines/bytes
-f = output appended data as the file grows; 
•	cd - navigate between dirs
 	= with NO arguments takes us to ~
= toggle between the last two dirs. 
•	mkdir - make a directory
    	-p = make parent directories as needed 
-m = set permission mode
-v = print message for each created directory
•	touch - creates empty file/updates access & modification time
•	cp - copy a file/ directory
-H = follow symlinks on the command line in recursive mode
-L = follow all symlinks in recursive mode
-P = do not follow symlinks in recursive mode (default)
-R = copy directories recursively
-X = don't copy extended attributes or resource forks
-a = archive mode, same as -RpP
-f = force overwriting existing file
-i = confirm before overwriting existing file
-n = don't overwrite existing file
-p = preserve timestamps, mode, owner, flags, ACLs, and extended at
-v = show file names as they are copied
•	mv - move/rename files/directory 
cp/mv -options source destination 
-r : recursive mode used for directories 
-i : interactive confirm file overwriting 
-v : verbose see copy progress
-p: preserve file permission/attributes 
•	rm - eliminate files (**Be careful! No recycle bin in Unix!**)
 	-f : force, never prompt 
-r : recursive mode used for directories 
-i : interactive confirm file overwriting 
-v : verbose see copy progress
•	chmod - change file read/write/execute permissions
ugo = user/group/other (special option a=all)
rwx= read/write/execute
u(rwx )/g(rwx )/o(rwx)->9 binary->3 decimal->ex:737 
ex: u+r+w,g-w,o+wrx (NO space in parameters) 
•	wc - print line, word, and byte counts -c = print the byte counts
-m = print the character counts
-l = print the newline counts 
-w = print the word counts
•	seq - print sequence of numbers (start step stop) 
-f = format ( -f %5.1f, -f%3.1e, -f “Line: %g” )
-s = delimiter (default = \n) 
•	less - interactively show content of a file 
-N = show line number
-S = truncate lines wider than window
Use this while reading: 
G / g = go to end/beginning of file
q = quit
/ = forward Search (? = backward search) 
^pattern : pattern @ beginning of line
pattern$ : pattern @ end of line 
n – next match ; (N = previous match) 
•	find - search for files.    [path] [conditions]   
-type + f=file, d=directory 
-name = find by name 
			(-iname = case insensitive) 
find . -type f -name "text_file*" 
-maxdepth/mindepth = max/min dir levels (Level 1=./) 
-perm p = with permissions p (p is integer ex: 757) 
-not = ! = invert the match
-size +/-n= file larger/smaller than n
-mmin N = files modified within N minutes
-mtime N : files modified within N days
-newermt YYYY-MM-dd = modified on or after date 
-exec cmd = execute command on every found file
-ok cmd = prompt before executing on a file 
find *.txt -exec ls {} \; -exec sh -c "head {} | tr A B” \; 
All occurrences of {} are replaced by the filename. 
•	uniq - report/omit repeated adjacent lines
 	-c = --count = prefix lines by the num of occurrences 
-d = print only duplicate lines 
•	sort - sort lines of text files
 	-d = alphanumeric characters (default)
 	-n = numeric-sort
 	-r = reverse
 	-f = ignore-case
 	-u =remove duplicates, output just unique lines
 	-t "x"= field delimiter "x" (default = white space) 
-k M[,N] =sort field key=part from col M and EOL or col N 
 		sort -t"," -k1,2 -k3n,3 = on 1st and 2nd then on 3rd num 
sort -t"," -k1,1 -u = remove duplicates based on 1st field 

•	cut - slice lines 
 	-d "x"= field delimiter "x" (default = TAB)
-f =select only these fields --output-delimiter=STRING 
-l = list files
(default= same as input) 
•	paste - Concatenate horizontally; Merge lines of files 
= with NO arguments on 1 file = cat command
-s = join all lines in a file
-d "xy"= delimiters "xy" (default = TAB) 
- - - = num of "-" equals num of columns in output 
paste file1 file2 vs <file1 <file2 vs - - <file1 <file2 paste <(seq 10) <(cat text.txt) 
•	tr -option SET1 SET2 = translate/delete chars 
-s = squeeze-repeated chars from SET1 
-d= delete chars in SET1, do not translate 
tr -d "a-z" tr -d "[:digit:]" 
-c = keep just the characters set with -d option 
•	grep “STRING" [files] = print lines matching pattern 
-v = Invert match; select non-matching lines.
-i = case unsensitive
-n = Prefix each line with its line number 
-c = print count of matching lines for each input file 
-w = only lines containing whole word matches
- [A/B/C] +N = print lines after/before/around match 
-H = Print the file name for each match. 
-E = enable regular expression
-o = show just the pattern matched
-b = show byte offset of the starting point of match 
•	sed - line oriented stream editor
 	-i = edit files in place
 	-n = no printing (default:print every line) 
 			s = substitute + delimiter + in + out sed 's/day/night/' 
/g = global -> all occurrences of the pattern
/I = case insensitive sed 's/this/THAT/gI' 
p = print (with “-n” = print modified lines) sed -n '2,4p' 
d= delete line seq5|sed'/3/d’ vsseq5|sed-n'2,4d' 
! = reverse the restriction sed -i '1~3!d' file.txt 
sed -n 's/pattern/&/p' <file = grep pattern 

•	The pipe 
-	The most common way of combining command-line tools is through a so-called pipe. 
-	The output of a command-line tool is by default passed on to the terminal, which displays it on our screen. 
-	We can pipe the output of one command to the input of the second tool by using “|” 
-	A long command can be broken up with either a backslash (\) or a pipe symbol (|) . 
 

Compressing/Uncompressing Files

•	zip out.zip file1.in file2.in = compress several files 
-r = directory 
•	unzip = list, test, extract 
-p = print content 
-c = extract to stdout (print name of each file) 
-p = extract to stdout (without file namea) 
   	   		unzip -p text_files.zip one_file_from_zip|less 
-l = list files
•	zipinfo = list detail information
•	zcat, zless, zgrep = cat, less, grep over zip 
•	gzip = compress one file to file.gz 
-d = decompress 
-f = force = overwrite existing files
-l = list compression info of gz file
-k = keep input file 	(default = compress in-place)
gzip file1 file2 file3 -> produces 3 gz files 
•	gunzip = decompress
•	zcat, zless, zgrep = cat, less, grep over gz 



•	bzip2 = compress one file to file.bz2
Hadoop read, manipulate and slice in blocks (64/128MB) 
-d = decompress
-f = force = overwrite existing files
-k = keep input file (default = compress in-place) 
--best /--fast = compression methods 
•	bunzip2 = decompress
•	bzcat, bzless, bzgrep= cat, less, grep over bz/bz2 
•	tar = archiving files utility -c = create 
-r = add
  		-x = extract
  		-t = list/view
-f [FILE]= file archive (needs to be followed by name) 
-v = verbose
-z = zip
-j = bzip2
-C -destination = extract to destination directory
				tar -czvf opentravel.gz.tar *.csv 
mkdir optd; tar -xzvf ./opentravel.gz.tar -C optd 




Job handling		(per shell) 

•	CTRL+C = kill a job in foreground
•	& = run the command as background job 
•	CTRL+Z = suspend the current foreground job 
•	bg = move suspended job to background. 
•	jobs = lists the active jobs 
-n = show new jobs that changed status from last call 
-r = display running jobs
-s = display stop jobs 
•	fg = bring susp/bkground job to foreground. 
= no arguments = most recent job 
%x = bring to fg the job with ID=x (ID from jobs) 
•	kill = kill the process by ID or PID 
%x= kill bg/susp job from same shell
PID=kill by process ID (shell PID= echo $$, tab to get PID) 
•	xkill = kill a process by selecting a window 
•	pkill = Kill the process by name
•	pgrep = look up process based on name 
•	top = display Linux processes
•	htop = interactive process viewer


•	ps =snapshot of current processes 
-e = select every process
-f = full listing
-U = select process by real user 
•	PPID =parent PID; it started PID (use with zombie processes) 


Numerical operators 	(a=1; b=2) 
-eq 	equal 	[ $a -eq $b ]=F 
-ne 	not equal 	[ $a -ne $b ]=T 
-gt 	greater than 	[ $a -gt $b ]=F 
-lt 	less than 	[ $a -lt $b ]=T 
-ge 	greater than or equal 	[ $a -ge $b ]=F 
-le 	less than or equal 	[ $a -le $b ]=T 
! 	logical negation 	[ ! false ]=T 
-o 	logical OR 	[ $a -lt 2 -o $b -gt 5 ]=T 
-a 	logical AND 	[ $a -lt 2 -a $b -gt 5 ]=F 

String operators 	(a="abc"; b="efg") 
= 	equal 	[ $a = $b ]=F 
!= 	not equal 	[ $a != $b ]=T 
-z 	operand zero size 	[ -z $a ]=F 
-n 	operand non-zero size 	[ -n $a ]=T 
str 	string exists? 	[ $a ]=T 

File test operators 	(test file, rwx+, size 100b) 
-d file 	file is a dir 	[ -d $file ]=F 
-f file 	ordinary file, NOT a dir 	[ -f $file ]=T 
-r file 	file is readable 	[ -r $file ]=T 
-w file 	file is writable 	[ -w $file ]=T 
-x file 	file is execute 	[ -x $file ]=T 
-s file 	file has size > 0 	[ -s $file ]=T 
-e file 	file/dir exists 	[ -e $file ]=T 

ShortCuts

CTRL+shift+n = open shell in new window
CTRL+shift+t = open shell in new tab 
CTRL + l = clear screen
CTRL + r = history block search 
CTRL+D = terminate the shell 
ALT+b/f = move backward/forward word by word 
CTRL + u = cut/erase the whole line
CTRL + k = cut/erase line right from the cursor
CTRL + w = cut/erase word left 
ALT + d = cut/erase word right
CTRL + y = paste (1st buff)
CTRL+SHIFT+c = copy highlight text (2nd buff)
CTRL+SHIFT+v = paste 2nd buff; after usage=1st buff 
ALT + c = capitalize first letter of the word 
ALT + u = uppercase the rest of the word 
ALT + l = lowercase rest of the word
