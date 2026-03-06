**Quick Reference Table**

|Topic         |	Key Syntax	                                      |    Example                                                             |
|--------------|----------------------------------------------------|------------------------------------------------------------------------|
|Variable      | VAR="value"                                        | NAME="DevOps"                                                          |
|              |                                                    |                                                                        |
|Argument      | $1, $2                                             | ./script.sh arg1                                                       |
|              |                                                    |                                                                        |
|If            | [ condition ]; then                                | if [ -f file ]; then                                                   |
|              |                                                    |                                                                        |
|For loop      | for i in list;                                     |do	for i in 1 2 3; do                                                   |
|              |                                                    |                                                                        |
|Until         |until [ condition ] do .. done                      |until [ $i -eq 5 ] do echo $i ((i++)) done                              |                                          |
|              |                                                    |                                                                        |
|Function      |name() { ... }                                      |	greet() { echo "Hi"; }                                                 |
|              |                                                    |                                                                        |
|Grep          |grep pattern file                                   |grep -i "error" log.txt                                                 |                       |
|              |                                                    |                                                                        |
|Awk           |awk '{print $1}' file                               |	awk -F: '{print $1}' /etc/passwd                                       |                                 |
|              |                                                    |                                                                        |
|Sed           |sed 's/old/new/g' file                              |sed -i 's/foo/bar/g' config.txt                                         |
|              |                                                    |                                                                        |
|Case          |case variable in a);; b);; *);; esac                |case $num in a);; b);; *);; esac                                        |
|              |                                                    |                                                                        |
|Sort          |sort file                                           |sort -n log.txt                                                         |
|              |                                                    |                                                                        |
|Tr            |tr option [set1] [set2] < file                      |tr [a-z] [A-Z] < file                                                   |
|              |                                                    |                                                                        |
|Wc            |wc option file                                      |wc -wcl log.txt                                                         |
|              |                                                    |                                                                        |
|Head          |head -n file                                        |head -10 log.txt                                                        |
|              |                                                    |                                                                        |
|Tail          |tail -n file                                        |tail -10 log.txt                                                        |


**Task 1: Basics**

Document the following with short descriptions and examples:

1.Shebang (#!/bin/bash) — what it does and why it matters

ans: shebang is used by interpreter to tell the operating system which program should be used to execute the scripts 

2.Running a script — chmod +x, ./script.sh, bash script.sh

ans: 

* chmod +x: permits execute access to all -owner, groups , others

* ./script.sh: used execute the script from terminal, referring the current directory (./) script.sh

* bash script.sh : passing the script to bash and executing it which doesnt require execute permissions

3.Comments — single line (#) and inline

ans:

#echo used to print anything   - single line comment
echo "hello world"

echo "hello world"   #echo is used to print anything  - inline comment 



4.Variables — declaring, using, and quoting ($VAR, "$VAR", '$VAR')

ans:

* declaring a variable:

VAR="TONY"

* using a variable :

echo "HELLO $VAR" --> HELLO TONY  ; prints the string what has been asked to print(echo)

* quoting a variable:

echo '$VAR' --> $VAR  ; directly prints $VAR considering it as a string .


5.Reading user input — read

read -p Enter user name;uname  -  read keyword is used to take input from user prompting the qeustion
                                  and stores in the variable given 'uname'

6.Command-line arguments — $0, $1, $#, $@, $?

* $0 : considers the argument at the 0th index of the command i.e the command itself

     ex: ubuntu$:./practise.sh  -- this is considered $0 value  at the 0th index in a command line argument

* $1 : considers the argument passed at the 1st index in the command line i.e the one passed after the main command 

     ex: ubuntu$:./practise.sh Hello  -- this is considered $0 value passed at  the 1st index in a command line argument 
     
* $# : prints the number of arguments passed 

* $@ : prints all the arguments in separate string ex: "$1" "$2" "$3".....

* $? : last commands exit status 

**Task 2: Operators and Conditionals**

Document with examples:

 String comparisons — =, !=, -z, -n

 a="Hello World"
 
 b="how are you"
 
'='operator : checks if two strings are equal 

 if [[ $a=$b ]];then
 
 echo "they are equal"
 
 else 
 
      echo " not equal"
      
 fi 

'!=' operator: checks if two strings are not equal

 if [[$a != $b ]];then
 
 echo "true"
 
 else 
 
      echo "false"
      
 fi  

'-z' operator: checks if string is empty

if [[ -z $a ]]; then

echo "empty"

else

     echo " not empty" 
fi

-n operator: checks if a string is not empty

if [[-n $b ]]; then

echo "not empty"

else

     echo " empty "
fi

2.Integer comparisons — -eq, -ne, -lt, -gt, -le, -ge

A=125
B=565

-eq: checks if two integers are equal 

if [ $A -eq $B ];then

echo " equal "

else 
      echo " not equal "
fi

-ne: check if the two integers are not equal 

if [$A -ne $B ];then

echo "true"

else 

     echo "false"
     
fi     
      
-lt : compares if A is less than B 

if [ $A -lt $B ];then

echo "lesser"

else 

    echo "greater"

fi    

-gt : compares A is greater than B

if [ $A -gt $B ]; then

echo "greater"

else 
     echo "lesser"
fi

-le : checks if lesser than or equal to 

if [ $A -le $B ]; then 

echo "true"

else 

     echo "false"
fi     

-gt: checks if greater than or equals to 

if [ $A -ge $B ]; then

echo "true"

else 
    echo "false"

fi



3.File test operators — -f, -d, -e, -r, -w, -x, -s

-f = If file exists and it is a regular file.

-d = If file exists and is a directory.

-e = If file exists and is a file/directory.

-r = If file exists and is readable.

-w = If file exists and is writable.

-x = If file exists and is executable.

-s = If file exists and has size greater than 0(Not Empty).

read -p "Enter File Name : " name

files=("-f" "-d" "-e" "-r" "-w" "-x" "-s")

for i in "${files[@]}";do

	if [ $i $name ];then
  
		echo "True"
    
	else
  
		echo "False"
    
	fi
  
done


 4.if, elif, else syntax

a=100

b=1000

if [ a -eq b ]; the 

echo "equal numbers"

    elif [ a -lt b ];
    
       echo "smaller number"
       
else 

    echo "greater number"
    
fi

 Logical operators — &&, ||, !
 
&& operator: 

number=7

if [[ $number -gt 5 && $number -lt 10 ]]; then

    echo "The number $number is between 5 and 10."
    
else

    echo "The number $number is outside the range."
    
fi



|| operator:

file="test_file.txt"

if [[ -r $file || -w $file ]]; then

    echo "The file $file is readable or writable."
    
else

    echo "The file $file is neither readable nor writable."
    
fi

 ! operator :
 
 variable="some value"

 if [[ ! -z "$variable" ]]; then
 
    echo "The variable is not empty."
    
else

    echo "The variable is empty."
    
fi
 
6.Case statements — case ... esac

read -p "enter command ( start, stop, or status )" cmd

case $cmd in

        start)
                echo "system is starting"
                ;;

        stop)
                echo "system is stopping"
                ;;

        status)
                echo "checking status"
                ;;

        *)
                echo "wrong input"
                exit 1
                ;;


esac

output:

$ ./practise.sh

enter command ( start, stop, or status )start

system is starting

$ ./practise.sh

enter command ( start, stop, or status )hello

wrong input


**Task 3: Loops**

Document with examples:

1.for loop — list-based and C-style

* list based style :

animals=( "tiger" "lion" "cheeta" "jaguar" "leopard" "dog" "cat" "hyna" )


for a in $animals;do

        echo "the name of animals are ${animals[@]} "

done

$ ./practise.sh

the name of animals are tiger lion cheeta jaguar leopard dog cat hyna

* C style:

for ((i=0; i<${#animals[@]}; i++));do

        echo "the name of animals are ${animals[i]}"

done

output:

$ ./practise.sh

the animals are tiger

the animals are lion

the animals are cheeta

the animals are jaguar

the animals are leopard

the animals are dog

the animals are cat

the animals are hyna


2.while loop

i=10
while [ $i -gt 0 ]
do
        echo "$i"
        ((i--))
done

OutPut:

./practise.sh 

10

9

8

7

6

5

4

3

2

1

3.until loop

i=5

until [ $i -eq 10 ]

do
	echo $i
  
	((i++))
  
done

OutPut:

./practise.sh 

5

6

7

8

9



4.Loop control — break, continue

read -p "Enter any num between 1-100 : " input

for(( i=$input; i<=100 ; i++ ));do

        if [[ $i -le 0 || $i -gt 100 ]]; then
        
                echo "Breaking loop: $i not between 1-100"
                
                break;
                
        fi
        
        if (( $i%2==0 ));then
        
                echo "$i"
                
                continue;
                
        fi
        
        echo "$i"
        
done

output:

Enter any num between 1-100 :50

50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70
71
72
73
74
75
76
77
78
79
80
81
82
83
84
85
86
87
88
89
90
91
92
93
94
95
96
97
98
99
100

$ ./practise.sh

Enter any num between 1-100 : -1

Breaking loop: -1 not between 1-100



5.Looping over files — for file in *.log

for file in *.sh;do

        echo "$file"
        
done

6.Looping over command output — while read line

cat create_user.sh | while read line;do

echo "$line"

done
      
**Task 4: Functions**

Defining a function — function_name() { ... }

1.Calling a function

2.Passing arguments to functions — $1, $2 inside functions







3.Return values — return vs echo

4.Local variables — local

solution:

sum()

{

        local LocalVariable=" this is a local  variable"

        echo "the sum is : $((a+b))"
        
        return


}

a=40

b=50

sum $a $b

echo "this is local variable:" $LocalVariable

echo "return" $?

output:

$ ./practise.sh

the sum is : 90

this is local variable:

return 0


**Task 5: Text Processing Commands**

1.grep — search patterns

* -i: Case insensitive
  
* -r: Recursive
  
* -c: Count matching lines
  
* -n: Print each line with line number
  
* -v: Inverted match (Exclude pattern)
  
* -E: Extended regex
  
2.awk — 

* print columns: awk '{print $1,$2}'
  
* field separator: awk -F: '{print $1,$7}'
  
* patterns: awk '/error/ {print $0}'
  
* BEGIN : awk 'BEGIN {print "START"}{print $3}'

* END : awk 'END {print "DONE"}{print $3}'

3.sed —  substitution, delete lines, in-place edit

* substitution: sed 's/WARNING/CRITICAL/g' file.log (It only prints the output unless you redirect it to a file. It doesn't change the actual file.)

* delete lines: sed '2,4d' file.log

* in-place edit: sed -i 's/CRITICAL/WARNING/g' file.log (Edits the file and apply the changes.)

4.cut — extract columns by delimiter 

* cut -d: -f1 /etc/passwd

5.sort —

* alphabetical: sort file.txt

* numerical: sort -n file.txt

* reverse: sort -r file.txt

* unique: sort -u file,txt

6.uniq — deduplicate, count

* sort sort.txt | uniq -dc
  
7.tr —

* translate: tr [a-z] [A-Z] < sort.txt
  
* delete characters: tr -d a < sort.txt
  
8.wc —  line/word/char count

* wc -wcl sort.txt

9.head / tail — first/last N lines, follow mode

* head : head -5 sort.txt

* tail : tail -5 sort.txt

**Task 6: Useful Patterns and One-Liners**

* Find and delete files older than N days : find . -mtime +4
  
* Count lines in all .log files : wc -l file.log
  
* Replace a string across multiple files : sed 's/hello/bye/g' *.txt
  
* Check if a service is running : systemctl status ssh
  
* Monitor disk usage with alerts : df -h | awk '$5>80'
  
* Tail a log and filter for errors in real time : tail -f file.log | grep -i "error"


**Task 7: Error Handling and Debugging**

1.Exit codes —

* $? :  Exit status of last command (0/1)

* exit 0 : Exit if success

* exit 1 : Exit if error
  
2.set -e — exit on error

3.set -u — treat unset variables as error

4.set -o pipefail — catch errors in pipes

5.set -x — debug mode (trace execution)

!/bin/bash

set -euo pipefail

set -x

echo "Check set -o pipefail"

cat count.txt | grep "total"

echo "After failing script running without set -o"

echo -e "\n"

echo "Undefined variable -u"

echo $a

echo "After using undefined variable script running without set -u"

echo -e "\n"

echo "Failed command -e"

mkdir ../scripts

echo "After failing command script running without using -e"


  
6.Trap — trap 'cleanup' EXIT

trap 'echo "CleanUp"' EXIT - It means on exit CleanUp will be printed.

You can even define a function cleanup() and write any code you want inside ex: rm /archive/*.gz. 

cleanup function will be executed on EXIT of a script.



     
