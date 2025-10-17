---
share: true
---
```toc
```

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

  # Simple Way with for
for var_name in 1 2 3 4 5
do 
	echo $var_name
done 
  
  # Another Way with for

for var_name in {1..5}
do 
	echo $var_name
done

  # Another Way with for

for var_name in `seq 1 5`
do 
	echo $var_name
done

  # if you on the network 
  # scan all ips in the same network

for ip in `seq 1 254`
do
	ping -c 1 $1.$ip
done

  # adding the grep with 64 bytes

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


```txt
  # Write the tool that you can use with making information about your target.

with Bash script

The usage for this tool:

Welcome with your tool Tastify:
1) For Tools That Use Domain/URL.
2) For Tools That Use IPs.

If the user Press (1) it show to him the tools that use domain 
1) tool 1
2) tool 2
3) tool 3
4) tool 4
etc...

if the user enter for example (3) it check 
	if this tool found or not 
		if found it use the URL that the user enter to run it.
		if not found it install this tool and use this.
and in all cases it saves the result with the file with the name of the target (e.g.. domain -> test.com  the file will be test.txt)



If the user Press (2) it show to him the tools that use domain 
1) tool 11
2) tool 12
3) tool 13
4) tool 14
etc...

if the user enter for example (12) it check 
	if this tool found or not 
		if found it use the IP that the user enter to run it.
		if not found it install this tool and use this.
and in all cases it saves the result with the file with the name of the target (e.g.. domain -> ip.com  the file will be ip(1).txt)



the tools:
. dig
DNS lookup tool for querying records (A, MX, TXT) and resolving domain details.
2. nslookup
Queries DNS to resolve domains to IPs or perform reverse lookups for IPs
3. host
Simple DNS lookup utility that checks domain records and supports zone transfer testing.
4. whois
Retrieves domain registration data: owner, registrar, creation date, name servers.
5. dnsrecon
Advanced DNS enumeration tool for subdomain discovery, zone transfers, and cache snooping
6. nmap
Network scanner for discovering hosts, open ports, services, and OS fingerprints on IPs
7. traceroute
Maps network path to an IP, showing all hops and latency between nodes.
8. curl
Fetches web content, headers, or interacts with APIs (e.g., crt.sh) for subdomain discovery.
9. crt.sh
Public SSL certificate log search engine to find subdomains linked to a domain
10. Shodan
Search engine for internet-connected devices; reveals exposed services and banners by IP
11. theHarvester
Collects emails, subdomains, and employee names from public sources like search engines and PGP keys.
12. Maltego
Visual OSINT tool that maps relationships between domains, IPs, emails, and social profiles
13. SpiderFoot
Automates OSINT collection from 100+ sources (WHOIS, DNS, SHODAN, breach logs)
14. recon-ng
Web reconnaissance framework with modules for subdomain scanning and API-based data harvesting
15. Censys
Search engine for devices and websites; provides certificate, port, and service data
16. BuiltWith
Identifies technology stack (CMS, frameworks, analytics) used by a website.
17. Wappalyzer
Detects technologies on websites including JavaScript libraries, servers, and CMS platforms.
18. Amass
Performs deep DNS enumeration and subdomain discovery using multiple data sources.
19. Netcraft
Provides site reports: hosting provider, server infrastructure, SSL history, phishing status
20. URLCrazy
Generates typo-squatting domains (e.g., gogle.com) to identify potential phishing threats.


```




```Bash
#!/bin/bash

# Install To Ubuntu 
Install(){
	if ! command -v "$1" &>/dev/null;
	then
		echo "[*] Installing $1...."
		sudo apt install -y "$2"
	fi
}

Ping(){
	read -p "Enter the IP x.x.x : "
	for ip in `seq 1 254`
	do
	ping -c 1 $1.$ip | grep "64 bytes" |cut -d " " -f 4 | tr -d ":" &
	done
}

Recon(){
	Install amass amass
	Install dirb dirb
	
	echo "Select Recon Tool:"
	echo "1) Amass"
	echo "2) Dirb"
	read -p "Choose Tool: " choice
	read -p "Write Target: " target
	case $choice in
		"1") amass enum -d "$target" -o "${target}"_amass.txt ;;
		"2") dirb "https://$target" ;;
		*) echo "Invalid Choice"
	esac
}

Scanning(){
    Install dirsearch dirsearch
    Install gobuster gobuster
    echo "Select Scanning Tool:"
    echo "1) dirsearch"
    echo "2) gobuster"
    read -p "Choose Tool: " choice
    read -p "Enter URL or IP: " target
    case $choice in
        "1") dirsearch -u "$target" -e php,html,js -o "${target}_dirsearch.txt" ;;
        "2") gobuster dir -u "$target" -w /usr/share/wordlists/dirb/common.txt -o "${target}_gobuster.txt" ;;
        *) echo "Invalid choice" ;;
    esac
}

Vulnerability() {
    Install sqlmap sqlmap
    Install zaproxy zaproxy
    echo "Select Vulnerability Tool:"
    echo "1) sqlmap"
    echo "2) zap-cli "
    read -p "Choose Tool:" choice
    read -p "Enter URL: " target
    case $choice in
        1) sqlmap -u "$target" --batch --risk=3 --level=5 --output-dir=./reports ;;
        2) zap-cli quick-scan -s xss,sqli "$target" ;;
        *) echo "Invalid choice" ;;
    esac
}

echo "Welcome with My tool 0x11"
echo "  _____           __   __ "
echo " / ___ \\ \\ \\ / / /_ | /_ |"
echo "| |   | | \\ V /   | |  | |"
echo "| |   | |  > <    | |  | |"
echo "| |___| | / . \\   | |  | |"
echo " \\_____/ /_/ \\_\\  |_|  |_|"

echo "**********************"
echo " Information Gathering"
echo "     More Simple      "
echo "**********************"

echo "Select Your Category: "
echo "1) Ping"
echo "2) Recon"
echo "3) Scanning"
echo "4) Vulnerability"
read -p "Choose: " choice

case $choice in
    "1") Ping ;;
    "2") Recon ;;
    "3") Scanning ;;
    "4") Vulnerability ;;
    *) echo "Invalid category" ;;
esac  
```


```Bash
#!/bin/bash

Install() {
    local cmd="$1"
    local pkg="$2"

    if ! command -v "$cmd" >/dev/null 2>&1; then
        echo "[*] $cmd not found — installing package: $pkg"
        sudo apt update -y
        sudo apt install -y "$pkg"
        echo "[+] Installed $pkg"
    else
        echo "[*] $cmd is already installed."
    fi
}

ensure_seclists() {
    local SECLISTS_DIR="/usr/share/wordlists/SecLists"
    local COMMON_PATH1="$SECLISTS_DIR/Discovery/Web-Content/common.txt"
    local DIRB_DIR="/usr/share/wordlists/dirb"
    local COMMON_PATH2="$DIRB_DIR/common.txt"
    local SECLISTS_GIT="https://github.com/danielmiessler/SecLists.git"
    local RAW_COMMON_URL="https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/common.txt"

    if [[ -f "$COMMON_PATH1" ]]; 
    then
        echo "$COMMON_PATH1"
        return 0
    fi

    if ! command -v git >/dev/null 2>&1; 
    then
        echo "[*] git not found. Installing git..."
        Install git git
    fi

    if [[ ! -d "$SECLISTS_DIR" ]]; 
    then
        echo "[*] Cloning SecLists into $SECLISTS_DIR (this may take a moment)..."
        sudo git clone --depth 1 "$SECLISTS_GIT" "$SECLISTS_DIR" || {
            echo "[!] Git clone failed — will attempt to download single wordlist instead."
            sudo rm -rf "$SECLISTS_DIR" || true
        }
    fi

    if [[ -f "$COMMON_PATH1" ]]; 
    then
        echo "$COMMON_PATH1"
        return 0
    fi

    echo "[*] Attempting fallback: download common.txt to $COMMON_PATH2"
    if [[ ! -d "$DIRB_DIR" ]]; 
    then
        sudo mkdir -p "$DIRB_DIR"
        sudo chmod 755 "$DIRB_DIR"
    fi

    Install curl curl

    tmpfile=$(mktemp)
    if curl -fsSL "$RAW_COMMON_URL" -o "$tmpfile"; 
    then
        sudo mv "$tmpfile" "$COMMON_PATH2"
        sudo chmod 644 "$COMMON_PATH2"
        echo "$COMMON_PATH2"
        return 0
    else
        rm -f "$tmpfile"
        echo "[!] Failed to download wordlist from $RAW_COMMON_URL" >&2
        return 1
    fi
}

sanitize_filename() {
    local s="$1"
    s="${s#http://}"
    s="${s#https://}"
    s="${s%%/*}"
    echo "$s" | sed 's/[^A-Za-z0-9._-]/_/g'
}

Ping() {
    read -r -p "Enter the IP base (e.g. 192.168.1) : " base
    if [[ -z "$base" ]]; 
    then
        echo "[!] Empty input"
        return 1
    fi

    echo "[*] Scanning $base.1-254 ... (this may take a while)"
    for ip in $(seq 1 254); 
    do
        ( ping -c 1 -W 1 "$base.$ip" >/dev/null 2>&1 && echo "$base.$ip is up" ) &
    done
    wait
    echo "[*] Ping sweep finished."
}

Recon() {
    Install amass amass
    Install dirb dirb

    echo "Select Recon Tool:"
    echo "1) Amass"
    echo "2) Dirb"
    read -r -p "Choose Tool [1/2]: " choice
    read -r -p "Write Target (domain or host): " target
    if [[ -z "$target" ]]; 
    then
        echo "[!] Empty target"
        return 1
    fi

    local safe_target
    safe_target=$(sanitize_filename "$target")

    case "$choice" in
        1)
            echo "[*] Running amass enum -d $target"
            amass enum -d "$target" -o "${safe_target}_amass.txt"
            echo "[+] amass results saved to ${safe_target}_amass.txt"
            ;;
        2)
            echo "[*] Running dirb against https://$target"
            dirb "https://$target"
            ;;
        *)
            echo "Invalid Choice"
            ;;
    esac
}

Scanning() {
    Install dirsearch dirsearch
    Install gobuster gobuster

    local WORDLIST
    WORDLIST="$(ensure_seclists)" || {
        echo "[!] Could not obtain SecLists/wordlist. You can provide a custom wordlist later."
        WORDLIST="/usr/share/wordlists/dirb/common.txt"
    }

    echo "Select Scanning Tool:"
    echo "1) dirsearch"
    echo "2) gobuster"
    read -r -p "Choose Tool [1/2]: " choice
    read -r -p "Enter URL or IP (e.g. https://example.com): " target
    if [[ -z "$target" ]]; 
    then
        echo "[!] Empty target"
        return 1
    fi

    local safe_target
    safe_target=$(sanitize_filename "$target")

    case "$choice" in
        1)
            echo "[*] Running dirsearch against $target"
            dirsearch -u "$target" -e php,html,js -o "${safe_target}_dirsearch.txt"
            echo "[+] dirsearch finished. Results: ${safe_target}_dirsearch.txt"
            ;;
        2)
            echo "[*] Running gobuster against $target with wordlist $WORDLIST"
            gobuster dir -u "$target" -w "$WORDLIST" -o "${safe_target}_gobuster.txt"
            echo "[+] gobuster finished. Results: ${safe_target}_gobuster.txt"
            ;;
        *)
            echo "Invalid choice"
            ;;
    esac
}

Vulnerability() {
    Install sqlmap sqlmap
    Install zaproxy zaproxy
    if ! command -v zap-cli >/dev/null 2>&1; 
    then
        if command -v pip3 >/dev/null 2>&1; 
        then
            echo "[*] Installing zap-cli via pip3..."
            sudo pip3 install zap-cli || true
        fi
    fi

    echo "Select Vulnerability Tool:"
    echo "1) sqlmap"
    echo "2) zap-cli (requires ZAP running)"
    read -r -p "Choose Tool [1/2]: " choice
    read -r -p "Enter URL: " target
    if [[ -z "$target" ]]; 
    then
        echo "[!] Empty target"
        return 1
    fi

    case "$choice" in
        1)
            echo "[*] Running sqlmap (this can be noisy and slow). Results under ./reports"
            mkdir -p ./reports
            sqlmap -u "$target" --batch --risk=3 --level=5 --output-dir=./reports
            echo "[+] sqlmap finished. Check ./reports"
            ;;
        2)
            echo "[*] Running zap-cli quick-scan (requires ZAP running locally)."
            zap-cli quick-scan -s xss,sqli "$target" || echo "[!] zap-cli failed or ZAP not running."
            ;;
        *)
            echo "Invalid choice"
            ;;
    esac
}

echo "Welcome with My tool 0x11"
echo "  _____           __   __ "
echo " / ___ \\ \\ \\ / / /_ | /_ |"
echo "| |   | | \\ V /   | |  | |"
echo "| |   | |  > <    | |  | |"
echo "| |___| | / . \\   | |  | |"
echo " \\_____/ /_/ \\_\\  |_|  |_|"
echo

echo "**********************"
echo " Information Gathering"
echo "     More Simple      "
echo "**********************"
echo

echo "Select Your Category: "
echo "1) Ping"
echo "2) Recon"
echo "3) Scanning"
echo "4) Vulnerability"
read -r -p "Choose: " choice

case "$choice" in
    "1") Ping ;;
    "2") Recon ;;
    "3") Scanning ;;
    "4") Vulnerability ;;
    *) echo "Invalid category" ;;
esac
```