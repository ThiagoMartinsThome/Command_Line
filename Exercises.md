# Exercises:


## File utilities:

1. 	Create a directory “first_dir” in you home folder
2. 	Create an empty file “text_file.txt” inside “first_dir” directory.
3. 	Add execute permissions to group users, and write permissions to other users to “text_file.txt”
4. 	Create 3 subdirectories inside “first_dir”: “sub1”, “sub2”, “text_file”
5. 	Copy the “text_file.txt” file into “sub1” directory.
6. 	Move the “text_file.txt” into sub2 under name “text_file.txt.2” .
7. 	Copy the whole directory “sub1” to “sub3” directory.
8. 	Change file name of “first_dir /sub2/text_file.txt.2” to “first_dir /sub2/text_file.txt.backup”
9. 	Move “first_dir /sub2/text_file.txt.backup” to “first_dir” directory as hidden file
10. 	Delete the “sub2” subdirectory

### Solution:

1.	mkdir first_dir
2.	touch first_dir /text_file.txt	
3.	chmod g+x,o+w text_file.txt
4.	mkdir sub1 sub2 first_dir 
5.	cp text_file.txt sub1/          (or cp -p text_file.txt sub1/)
6.	mv text_file.txt sub2/text_file.txt.2
7.	cp -r sub1/ sub3/
8.	mv sub2/text_file.txt.2 sub2/text_file.txt.backup
9.	mv sub2/text_file.txt.backup ./.text_file.txt.backup
10.	rm -r sub2/

## Content utilities :

1. Save the information (permissions, size, modification date etc.) of the largest file located inside opentraveldata directory into a file largest_file.txt. (hint: use ls with sort option and pipe the result)
2. How many words do first 5 lines of the Finn.txt have?
3. Print first 3 lines of Text_example.txt together with line numbers (hint: use cat and head)

### Solution:

1.	ls -ls | tail -n 1 > largest_file.txt 
2.	head -n 5 Finn.txt|wc -w
3.	cat -n Text_example.txt | head -n 3


## Content utilities 

1.Use Text_example.txt to generate a new file with the same content but with line number at the beginning of each line. 
2.Generate a new file with twice the content of “Text_example.txt” one after another inside the file. (one full text content after another) 
3.Open new shell inside a new terminal tab and using block search execute again the command where we printed the linux details at the beginning of the class (hint: it had "release" in the name) 
4.Generate a file with creation timestamp and name of the user who created it on the first line. Something like this: 
"# This file is created by KSCHOOL on:Sun Nov 26 10:31:06 CET 2017 »
(hint use command date to generate the time stamp, use man to read the date manual if needed) 
5.Save last 20 commands used at command line to a file. (hint use history and redirect the output) 
6.Print content of Text_example.txt except first 2 and last 3 lines. 
7.How many lines does optd_aircraft.csv file have? 

### Solution:

1.	cat -n Text_example.txt > Text_example_line_numbers.txt
2.	cat Text_example.txt Text_example.txt > Text_example_x2.txt 
3.	cmd+T
	       CTRL+R
	       type: relase
	       use CTRL+R to locate the command 
4.	echo "# This file  is created by KSCHOOL on: $(date)” > timestamp_header.txt
5.	history -20 >last_20.
6.	cat -n Text_example.txt | head -n -3 | tail -n +3
7.	wc -l  ~/Data/opentraveldata/optd_aircraft.csv 

## Content utilities 

1.Find all files located inside subdirectories of your home directory which have been modified in last 60min
2.Find all empty files inside subdirectories of your home directory which do NOT have read-write-execute permissions given to all users
3.Expand previous command to grant these permissions using “ok” option.
4.Get top 3 largest files per subdirectory inside ~/Data/ 

### Solution:

1.	find ~ -mindepth 2 -type f -mmin -60 
2.	find ~ -mindepth 2 -type f -empty ! -perm 777
3.	find -type f -empty ! -perm 777 -ok chmod 777 {} \;    (use CTRL+C to kill this command)
4.	find ~/Data/ -type d -exec echo {} \; -exec sh -c "ls -S {} | head -3 " \;


## Sorting and Counting:

1. Find top 10 files by size in your home directory including the subdirectories. Sort them by size and print the result including the size and the name of the file (hint: use find with –size and -exec ls –s parameters) 

2. Create a dummy file with this command : seq 15> 20lines.txt; seq 9 1 20 >> 20lines.txt; echo"20\n20" >> 20lines.txt; (check the content of the file first) 
	a)  Sort the lines of file based on alphanumeric characters 
	b)  Sort the lines of file based on numeric values and eliminate the duplicates 
	c)  Print just duplicated lines of the file 
	d)  Print the line which has most repetitions 

3. Create another file with this command : seq 0 2 40 > 20lines2.txt 
	a)  Create 3rd file combining the first two files (20lines.txt and 20lines2.txt) but without duplicates 
	b)  Merge the content of 20lines.txt and 20lines2.txt into 40lines.txt. Print unique lines together with the number of occurrences of 40lines.txt file and sort the line based on line content. 
	c)  How would you get the same result without passing through the intermediary file 40lines.txt? 

4. Go to ~/Data/opentraveldata Get the line with the highest number of engines from optd_aircraft.csv by using sort. 

### Solution:

1. 	find ~ -type f -size +10M -exec ls -sh {} \; | sort -nr | head
2.
	a) sort -d 20lines.txt
	b) sort -nu  20lines.txt
	c) sort -n  20lines.txt | uniq –d
	d) sort -n  20lines.txt | uniq -d -c | sort -nr | head -1
3.
	a) sort -nu 20lines.txt 20lines2.txt > 20files_no_dupl.txt
	b) sort 20lines2.txt 20lines.txt | uniq -c | sort -k 2n,2 
4. sort -t "^" -k 7nr,7 optd_aircraft.csv |head -1

## Processing and filtering:

Go to ~/Data/opentraveldata
1.Change the delimiter of optd_aircraft.csv to “,”
2.Check if optd_por_public.csv has repeated white spaces
3.How many columns has optd_por_public.csv? (hint: use head and tr)
4.Print column names of optd_por_public.csv  together with their column number. (hint: use paste)
5.Use optd_airlines.csv to obtain the airline with the most flights?
6.Use optd_airlines.csv to obtain number of airlines in each alliance?

### Solution:

1.	cat optd_aircraft.csv | tr "^“ "," | optd_aircraft_comma.csv
2.	cat optd_por_public.csv | tr -s "[:blank:]"  | wc
    		wc optd_por_public.csv
    		Compare the size in bytes!	
3.	head -n 1 optd_por_public.csv| tr "^" "\n" | wc -l
4.	paste <(seq 46) <(head -1 optd_por_public.csv | tr "^" "\n") 
5.	cat optd_airlines.csv | cut -d "^" -f 8,14 | sort -t "^" -k 2nr,2 |head -1
6.	cat optd_airlines.csv| cut -d "^" -f 10 | sort| uniq -c | sort -rn | head

## Processing and filtering:

Go to ~/Data/opentraveldata

1.Use grep to extract all 7x7 (where x can be any number) airplane models from optd_aircraft.csv. 
2.Use grep to extract all 3xx (where x can be any number) airplane models from optd_aircraft.csv. 
3.Use grep to obtain the number of airlines with prefix “aero” (case insensitive) in their name from optd_airlines.csv 
4.How many optd_por_public.csv columns have “name” as part of their name? What are their numerical positions? (hint: use seq and paste)
5.Find all files with txt extension inside home directory (including all sub directories) that have word “Science” (case insensitive) inside the content. Print file path and the line containing the (S/s)cience word. 

### Solution:

1.	cut -d "^" -f 3 optd_aircraft.csv| grep -E "7[0-9]7"
2.	cut -d "^" -f 3 optd_aircraft.csv| grep -E "3[0-9]{2}"
3.	cat optd_airlines.csv | cut -d "^" -f 8 | grep -i -E "^Aero" |wc –l
4.	aste <(seq 50) <(head -n 1 optd_por_public.csv | tr "^" "\n")|grep name
5.	find ~ -type f -iname "*.txt" -exec grep -iwH "Science" {} \;

## Processing and filtering:

Use Text_example.txt

1.Replace every “line” with new line character (“\n”)
2.Print ONLY the lines that DON’T contain the “line” word

### Solution:

1.	sed 's/line/\n/g' Text_example.txt
2.	sed -n '/line/!p' Text_example.txt

## Working with compressed Files:

1.Go to ~/Data/us_dot/otp. Show the content of one of the files. 
2.Use head/tail together with zcat command. Any difference in time execution?
3.Compress “optd_por_public.csv” with bzip2 and then extract from the compressed file all the lines starting with MAD (hint: use bzcat and grep)
4.(On_Time_On_Time_Performance_2015_1.zip): What are the column numbers of columns having “carrier” in the name ? (don't count!) (hint: we have seen this )
5.(On_Time_On_Time_Performance_2015_1.zip) Print to screen, one field per line, the header and first line of the T100 file, side by side.

### Solution:

1.	zless On_Time_On_Time_Performance_2015_1.zip 
2.	zcat On_Time_On_Time_Performance_2015_1.zip |head
       zcat On_Time_On_Time_Performance_2015_1.zip |tail
3.	bzip2 optd_por_public.csv
       bzcat optd_por_public.csv.bz2 | grep -E "^MAD" 
	or
       bzgrep -E "^MAD" optd_por_public.csv.bz2 
4.	paste <(seq 110) <(zcat ./On_Time_On_Time_Performance_2015_1.zip  | head -n 1 | tr "," "\n")|grep -i "carrier"
5.	paste <(seq 110) <(zcat ./On_Time_On_Time_Performance_2015_1.zip  | head -n 1 | tr "," "\n") <(zcat ./On_Time_On_Time_Performance_2015_1.zip  | head -n 2 | tail -1 | tr "," "\n")

## Shell Script:

1.Create a script that will return  column names together with their column number from the csv files. The first argument should be file name and the second delimiter.
2.Create a script that accepts a CSV filename as input ($1 inside your script) and returns the model of the aircraft with the highest number of engines. (use it on  ~/Data/opentraveldata/optd_aircraft.csv) 
3.Repeat script 2, but add a second argument to accept number of a column with the number of engines. If several planes have the highest number of engines, then the script will only show one of them.  (use it on  ~/Data/opentraveldata/optd_aircraft.csv) 
4.Create a script that accepts as input arguments the name of the CSV file, and a number (number of engines) and returns number of aircrafts that have that number of engines. (use it on  ~/Data/opentraveldata/optd_aircraft.csv)  

### Solution:

1.	File: column_name_number.sh                                                    
	#!/usr/bin/bash
	FILE_INPUT=$1
	DELIMITER=$2
	#echo "My name is ${0}"
	#echo "Delimiter= ${DELIMITER}"
	#echo "file=${FILE_INPUT}"
	NUM_COLUMNS=$(cat ${FILE_INPUT} | head -1 | tr ${DELIMITER} "\n" | wc -l)
	#echo "Column Number=${NUM_COLUMNS}"
	paste <(seq ${NUM_COLUMNS}) <(head -1 ${FILE_INPUT} | tr ${DELIMITER} "\n")
2.	File: model_with_most_engines.sh
	#!/usr/bin/bash
	FILE_INPUT=$1
	MODEL=$(sort -t "^" -k 7nr ${FILE_INPUT}|head -1 | cut -d "^" -f 3)
	echo "The model is ${MODEL}"
3.	File: model_with_most_engines2.sh
	#!/usr/bin/bash
	FILE_INPUT=$1
	COLUMN_INPUT=$2
	MODEL=$(sort -t "^" -k ${COLUMN_INPUT}nr ${FILE_INPUT}|head -1 | cut -d "^" -f 3)
	echo "The model is ${MODEL}"
4.	File: num_of_engines2.sh
	#!/usr/bin/bash
	FILE_INPUT=$1
	NUM_ENGINES=$2
	cut -d "^" -f 7 ${FILE_INPUT}|  grep "${NUM_ENGINES}"| uniq -c | tr -s " " | cut -d " " -f 2

## CSVkit:

1.Use csvstat to find out how many different manufactures are in the file
2.Extract the column manufacturer and using pipes, use sort, uniq and wc  find out how many manufacturers are in the file. Why does this number differ to the number reported in csvstat?
3.What are the top 5 manufacturers? 
4.Using csvgrep, get only the records with manufacturer equal to Airbus and save them to a file with pipe (|) delimiter.

Solution:

1.	csvstat -d "^" -c manufacturer optd_aircraft.csv

2.	 csvcut -d '^' -c manufacturer optd_aircraft.csv | tail -n+2 | sort | uniq | wc –l

3.	 tail -n+2 optd_aircraft.csv | cut -d '^' -f 2 | sort | uniq -c | sort -nr | head -5
  	 or
 	 csvcut -d '^' -c manufacturer optd_aircraft.csv |csvsort | tail -n+2 | uniq -c |sort -nr | head -5

4.	csvgrep -d '^' -c manufacturer -m Airbus optd_aircraft.csv | tr "," "|" > airbus.csv 
    	or
    	csvgrep -d '^' -c manufacturer -m Airbus optd_aircraft.csv | csvformat  -D '|' > airbus.csv
