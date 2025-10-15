---
share: true
---
<!-- Table of Contents -->
# Table of Contents
1. [[Notes_BashScript# Day 1:|Day 1:]]
	1. [[Notes_BashScript## ### local variable|### local variable]]
		1. [[Notes_BashScript### local variable|local variable]]
		2. [[Notes_BashScript### environmental variable|environmental variable]]
		3. [[Notes_BashScript### for making alias|for making alias]]
		4. [[Notes_BashScript### Command Substitution|Command Substitution]]
		5. [[Notes_BashScript### Print the sum|Print the sum]]
		6. [[Notes_BashScript### Redefine variables|Redefine variables]]
	2. [[Notes_BashScript## Steps To Create and Run Bash Script Code.|Steps To Create and Run Bash Script Code.]]
	3. [[Notes_BashScript## Task  Day 1|Task  Day 1]]
		1. [[Notes_BashScript### Task 1|Task 1]]
2. [[Notes_BashScript# Day 2|Day 2]]
	1. [[Notes_BashScript## Cut|Cut]]
3. [[Notes_BashScript# |]]
	1. [[Notes_BashScript## Sed|Sed]]
	2. [[Notes_BashScript## AWK|AWK]]
	3. [[Notes_BashScript## Sort |Sort ]]
	4. [[Notes_BashScript## If Condition|If Condition]]
	5. [[Notes_BashScript## Case|Case]]
	6. [[Notes_BashScript## Select Loop|Select Loop]]
	7. [[Notes_BashScript## Tasks Day 2|Tasks Day 2]]
		1. [[Notes_BashScript### Task 2|Task 2]]
		2. [[Notes_BashScript### Task 3|Task 3]]
4. [[Notes_BashScript# Day 3|Day 3]]
	1. [[Notes_BashScript## While Loop:|While Loop:]]
	2. [[Notes_BashScript## Until Loop|Until Loop]]
	3. [[Notes_BashScript## For|For]]
	4. [[Notes_BashScript## Tasks Day 3|Tasks Day 3]]
		1. [[Notes_BashScript### Task 4 |Task 4 ]]

<!-- End of TOC -->





# Day 1:

### local variable

commands:
	From terminal
	name=tester
	country=Egypt
	echo "My Name is $name, I'm from $country."

### environmental variable

command:
	echo $SHELL
	echo $HOME
	echo $USER
	echo $PATH

### for making alias

Command
	`alias 1="ls -la"`
	when you press 1 you default make the ls -la
	when you close this tab this alias to work

In the same terminal to delete the alias from the terminal  
	`unalias 1`
	and this can not shown with the journal --since 10:00

### Command Substitution

Command:
	`echo date`
	`echo "Today is date"`
	`echo "Today is $date"`
	`echo "Today is $(date)"`    ===   `echo "Today is `date`"`

### Print the sum

Command:
	`echo "The SUM of 1 & 2 is $((1+2))"`
	`echo "The SUM of 1 & 2 is $[1+2]"`

### Redefine variables

Command:
	`root@root:~ $0 $1 $2 $3`
Example:
	`root@root:~ sudo apt install thing`
	`root@root:~ $0    $1   $3     $4  `

---
## Steps To Create and Run Bash Script Code.

To Write the First simple bash script steps to make this:
1. Create the file myFile.sh
	- `touch myfile.sh`
2. Opening the file you created
	- `vim myfile.sh`
3. Change the file permission to be execution
	- `chmod +x myfile.sh`
4. Install any service and enable it automatically
```bash
	#!/bin/bash
	echo "Hello,Wrold"
```

---

Example: Install Any Service Any Enable it With Simple Bash Script
```Bash
#!/bin/bash

sudo apt install http -y
systemctl enable --now http
```
Example: Make backup for any file to any place
```bash
#!/bin/bash

 #tar [-option] Desctinitation Source
tar -cf /root/bacup_test.tar /home/user

 # script can more realabile
tar -cf /home/user/Desktop/backup$(date +%F).tar /home/user/Desktop/Task1.txt
```

## Task  Day 1

### Task 1
```txt
Write the Bash Script Take Name, Age and Country From The User and Print to Him the Message With This Inputs. 
```
Method 1
```bash
#!/bin/bash

echo "Please Enter Your Name: ";read name
echo "Please Enter Your age:"; read age
echo "Please Enter Your Country";read country

echo "hi $name, you are $age years old, your country is $country"
```
Method 2
```bash
#!/bin/bash

read -p "Please Enter Your Name: " name
read -p "Please Enter Your age: " age
read -p"Please Enter Your Country: " country

echo "hi $name, you are $age years old, your country is $country"
```



---
----

# Day 2

## Cut
```txt
1- Cut :
	Options: [-b Byte] [-c Character] [-f Field] [-d Determinate]
```
Example: Cut
```Bash
# 
cut -d ":" -f 1 /etc/passwd
cut -d ":" -f 1,2 /etc/passwd
```

## Sed
```txt
2- Sed :
	- non interactive text editor
	- Edit data based on rules (insert, delete, search,replace)
	- Supports regex
	- Addressing is used to determiniate whisch lines to be edited
	- The addressing fromst can be : [number > line number, regex, both]
	- The sed command tell sed what to do [print it, remove it, change it]
```

```txt
  # sed command filename
Sed :
	Options: [p for Print],[g for Global],[d for Delete],[s for Silent],[-e for Regular Expression] [n Quit mode]
```

```CSV
// names.csv
first name,last name,email
Yasmin,Muhamed,yasminmahmoud@gmail.com
ahmed,mostafa,ahmedmostafa@gmail.com
rafat,Morad,rafatmorad@gmail.com
davd,amer,davadamer@gmail.com
hambola,test,hambolatest@gmail.com
mahmoud,ahmed,mahmoudahmed@gmail.com
Ahmed,morad,ahmedmorad@gmail.com
osama,amr,Osamaamr@gmail.com
ali,ibramhim,aliibrahim@gmail.com
```
Example: Sed
```Bash
sed -n '/Ahmed/p' names.csv
  # sed -n '/Ahmed/amer/p' names.csv

  # get from 2-4 with use , with the name 
sed -n '/Yasmin/,/hambola/p' names.csv
sed -n '2,/hambola/p' names.csv

  # Replacing  [`g` for global]
sed 's/Ahmed/Hassan/g' names.csv

  # Delete from logs
sed '4d' names.csv
  # delete From line 4 to the end
sed '4,$d' names.csv

  # Delete Line that has the name 'Ahmed'
sed '/Ahmed/d' names.csv

  # Delte the fourth line (-e Regular Expresstion) and Replace Ahmed with Hossam
sed -e '4d' -e 's/Ahmed/Hossam/g' names.csv 
```

## AWK
```txt
3- awk:
	- Programming language used for manipulation data & generating reports
	- awk scan a file line by line, searching for lines that match a specified pattern performing selected actions
	- The awk utility consists of:
		  - awk 'instructions' filename
		  - each line is called a record
		  - Record separation are by default 'return'
		  -
```
Example: AWK
```Bash
  # awk -F [field]

  # Get all entire record
awk -F : '{print $0}' /etc/passwd
cat -n /etc/passwd

  # print first record.
awk -F : '{print $1}' /etc/passwd
  # print secons record.
awk -F : '{print $2}' /etc/passwd
 # print third record.
awk -F : '{print $3}' /etc/passwd

 # Get first record the first column first.
awk -F : 'NR==1{print $1}' /etc/passwd

  # print the number in the first and print the records
awk -F : '{print NR,$0}' /etc/passwd

 # Number it and print the Range from 45 <= NR >= 50
awk -F : 'NR>=45&&NR>=13{print $0}' /etc/passwd
awk -F : 'NR>=45&&NR>=13{print $1}' /etc/passwd
 # you can do this with the 
awk -F : 'NR==45,NR==13{print $0}' /etc/passwd
awk -F : 'NR==45,NR==13{print $1}' /etc/passwd

 # To run the single column 
awk -F : 'NR==45||NR==13{print $0}' /etc/passwd

 # Print Number of Fileds for the Record
awk -F : '{print NF,$0}' /etc/passwd
awk -F : '{print NF}' /etc/passwd
```

## Sort 
```txt
Sort:
	Sort file content in a specified order: alphabetical,reverse order, number order,or month
	- -o write the output to a file
	- sort file.txt (sort file.txt > newfile.txt)
	- -r reverse order
	- -n sort numerically if the file contents numbers
	-  -k sort according to the kth column(if the file is formattedas a table)
	- -u removes the duplicates
	- -t for delimiter
```
Example: Sort
```Bash
sort names.csv
sort -r names.csv # -r for reverse
 # sort -determinate seberate with : -k for the Kth column 3 with number
sort -t : -k 3n /etc/passwd # 

```

```txt
Operators:
	+
	-
	*
	/
	%
	=
	==
	!=
	>		
    >
	=
	<
	<=
	-gt
	-lt
	-eq
	-ge # greater or equal
	-le # less than or equal
```

## If Condition
```txt
Condition Statement "IF"

if[ Condition ]
then
	Command
fi


if[ Condition ]
then
	command
elif [ 2nd Condition ]
then
	Command
else
	Command
fi
```
Example: If Condition
```Bash
#!/bin/bash

read -p "Please Enter The Number: " number

if [ $number -gt 0 ]
then
        echo "Number $number is Positive"
elif [ $number -lt 0 ]
then
        echo "Number $number is Negative"
else
        echo "Number $number = Zero"
fi
```
Example: If Condition
```Bash
#!/bin/bash

read -p "Are You OK? [y OR n]: " answer

if [ $answer == 'y' ]
then
        echo "Gald To hear That! "
elif [ $answer == 'n' ]
then
        echo "Sorry To hear That!"
else
        echo "Bye "
fi
```

## Case
```Bash
#!/bin/bash

read -p "Choose From Any Case From Cases[1,2,3]: " var
case "$var" in
        "1")
                echo "Thing about case 1."
                ;;
        "2")
                echo "Thing about case 2."
                ;;
        "3")
                echo "Thing about case 3."
                ;;
esac
```
Example: Case
```Bash
#!/bin/bash

read -p "Enter you favourite fruit: apple or banana or kiwi: " var
case "$var" in
        "apple")
                echo "Apple pie is so tasty."
                ;;
        "banana")
                echo "I like Banana bread."
                ;;
        "kiwi")
                echo "I like Kiwi."
                ;;
esac
```

## Select Loop
```Bash
select varname in option1, option2, option3, option4
do
	case $varname in
		option1)
			echo ""
			;;
		option2)
			echo ""
			;;
		option3)
			echo ""
			;;
		option4)
			echo ""
			;;
		*)
			echo ""
			;;
	esac
done
```
Example: Select Loop
```Bash
#!/bin/bash

PS3="Please Make Your Choise: "; export PS3
select Drink in tea coffee water juice appe all none
do
        case $Drink in
                tea|coffee|water|all)
                        echo "Go To the Canteen."
                        ;;
                juice|appe)
                        echo "Available at home"
                        ;;
                none)
                        break
                        ;;
                *)
                        echo "ERROR: Invalid Input!!"
                        ;;
        esac
done
```


## Tasks Day 2

### Task 2
```txt
Make a Simple Calculator 
```
Solution: Task 1
```Bash
#!/bin/bash

read -p "Enter the first Num: " number1
read -p "Enter the operator: " operator
read -p "Enter the second Num: " number2

echo "[$number1 $operator $number2]"

if [ "$operator" == "+" ]; 
then
    result=$(( number1 + number2 ))
elif [ "$operator" == "-" ]; 
then
    result=$(( number1 - number2 ))
elif [ "$operator" == "*" ]; 
then
    result=$(( number1 * number2 ))
elif [ "$operator" == "/" ]; 
then
    if [ "$number2" -eq 0 ]; 
    then
        echo "Not Exist"
        exit
    else
        result=$(( number1 / number2 ))
    fi
elif [ "$operator" == "**" ]; 
then
    result=$(( number1 ** number2 ))
elif [ "$operator" == "^" ]; 
then
    result=$(( number1 ^ number2 ))
else
    echo "You Are Joking"
    exit
fi

echo "Result = $result"
```
### Task 3
```txt
Task with If Condition that tell the student If he pass in the exam or not?
	Condition if the student >= 60 passed < 60 failed.
```
Solution: Task 2
```Bash
#!/bin/bash

read -p "Please Enter Your Grade [0:100]: " Grade

if [[ $Grade -ge 0 && $Greade -le 100 ]]
then
        if [ $Grade -le 59 ]
        then
                echo "Sorry, You are Failed"
        elif [ $Grade -gt 59 -a $Grade -lt 101 ]
        then
                echo "Congratulations, You are Passed "
        else
                echo "Out Of Scope!!"
        fi
else
        echo "Out Of Scope!"
fi
```



---
---

# Day 3

## While Loop:
```txt
while [ condition ]
do
	command
done
```
Example: While Loop
```Bash
#!/bin/bash


read -p "Please Enter you name: " name

while [[ ! $name =~ ^[a-zA-Z]+$ ]]
do
		read -p "Please Enter you name: " name
        echo "Please Enter valid Name!!"
done

echo "Your Registeration Complete Successfully"


```


## Until Loop
```txt
until [ condition ]
do 
	command
done
```

```txt
Your day will be:
	From 6-11   -> Good Morning
	The Time 12 -> Prayer Time
	From 13-16  -> Wrok Time
	OtherThing  -> Good Night
```
Example:Until Loop
```Bash
#!/bin/bash

read -p "Enter the hour(0-23): " hour

until [ $hour -ge 24 ]
do
        case $hour in
                [6-9]|10|11) echo "Good Morning :)"
                        ;;
                12) echo "Prayer Time!"
                        ;;
                1[3-6]) echo "Work Time!"
                        ;;
                *) echo "Good Night"
                        ;;
        esac
read -p "Enter the hour(0-23): " hour
done

echo "Exiting The Script!!"
```


## For
```txt
for var_name in 1 2 3 4 5
do 
	echo $var_name
done 
```
Example: For
```Bash
  #!/bin/bash

for var_name in 1 2 3 4 5
do 
	echo $var_name
done 



for var_name in {1..5}
do 
	echo $var_name
done



for var_name in `seq 1 5`
do 
	echo $var_name
done



for ip in `seq 1 254`
do
	ping -c 1 $1.$ip
done



for ip in `seq 1 254`
do
	ping -c 1 $1.$ip | grep "64 bytes"
done



for ip in `seq 1 254`
do
	ping -c 1 $1.$ip | grep "64 bytes" |cut -d " " -f 4
done



for ip in `seq 1 254`
do
	ping -c 1 $1.$ip | grep "64 bytes" |cut -d " " -f 4 | tr -d ":"
done



for ip in `seq 1 254`
do
	ping -c 1 $1.$ip | grep "64 bytes" |cut -d " " -f 4 | tr -d ":" &
done
```

## Tasks Day 3

### Task 4 
```txt
write a guess game with bash script this tool guess number from 1 to 100 and user enter the number if number bigger than the guess_number the tool tell the user the number you guess is bigger with while to get the  



the difination for this task:

( > random function ) => search about this

while [ $value = false]
do 
enter the number :
	if number bigger than or equal 0 and less than or equal 100 and integer
	
		if number not equal $random_value
			
			 if number bigger than $random
				 echo "number is bigger make number small"
				 enter the number less:
				 
			elif number smaller than $random
				 echo "number is smaller make number big"
				 enter the number more:
				 
			elif number equalto $random
				congratulation you got it 
				value = true
			fi
		fi
	else 
		enter the number from (0:100)
	fi
done
```
Solution: Task4
```Bash
#!/bin/bash

random_value=$(( RANDOM % 101 ))

valid=false

while [ "$valid" = false ]
do
    read -p "Enter a number [0:100]: " number
    
    if [[ "$number" =~ ^[0-9]+$ ]] && [ "$number" -ge 0 ] && [ "$number" -le 100 ]; 
    then
        if [ "$number" -gt "$random_value" ]; 
        then
            echo "Number is Big Enter a Number less Than [$number]"
        elif [ "$number" -lt "$random_value" ]; 
        then
            echo "Number is Small Enter a Number More Than [$number]"
        else
            echo "Congratulations! You got it!"
            valid=true
        fi
    else
        echo "Invalid Number :("
    fi
done
```



---
---