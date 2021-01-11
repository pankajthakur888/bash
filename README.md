# shell
   #Linux shell scripts

#1. Check File Existence
   # The following Bash shell script code-snippet gets the filename with its absolute path, and checks if the file exists or not and it throws the appropriate information.

exist.sh
$ cat exist.sh
#! /bin/bash
file=$1
if [ -e $file ]
then
	echo -e "File $file exists"
else
	echo -e "File $file doesnt exists"
fi

$ ./exist.sh /usr/bin/boot.ini
File /usr/bin/boot.ini exists

#2. Compare Numbers
   # The below script reads two integer numbers from user, and checks if both the numbers are equal or greater or lesser than each other.
   
numbers.sh
#!/bin/bash
echo "Please enter first number"
read first
echo "Please enter second number"
read second

if [ $first -eq 0 ] && [ $second -eq 0 ]
then
	echo "Num1 and Num2 are zero"
elif [ $first -eq $second ]
then
	echo "Both Values are equal"
elif [ $first -gt $second ]
then
	echo "$first is greater than $second"
else
	echo "$first is lesser than $second"
fi

$ ./numbers.sh
Please enter first number
1
Please enter second number
1
Both Values are equal

$ ./numbers.sh
Please enter first number
3
Please enter second number
12
3 is lesser than 12

#3. Basic Arithmetic Calculator
  # This examples reads input, which is a type of arithmetic operation wants to perform on bash variables (inp1 and inp2). The arithmetic operation could be addition, subtraction or multiplication..

$ cat calculator.sh
#!/bin/bash
inp1=12
inp2=11
echo "1. Addition"
echo "2. Subtraction"
echo "3. Multiplication"
echo -n "Please choose a word [1,2 or 3]? "
read oper

if [ $oper -eq 1 ]
then
	echo "Addition Result " $(($inp1 + $inp2))
else
	if [ $oper -eq 2 ]
	then
		echo "Subtraction Result " $(($inp1 - $inp2))
	else
		if [ $oper -eq 3 ]
		then
			echo "Multiplication Result " $(($inp1 * $inp2))
		else
			echo "Invalid input"
		fi
	fi
fi

$ ./calculator.sh
1. Addition
2. Subtraction
3. Multiplication
Please choose a word [1,2 or 3]? 4
Invalid input

#4. Read and Ping IP address
  # The following script is used to read the IP address and check whether the IP address is reachable, and prints the appropriate message.

$ cat ipaddr.sh
#!/bin/bash
echo "Enter the Ipaddress"
read ip

if [ ! -z $ip ]
then
	ping -c 1 $ip
	if [ $? -eq 0 ] ; then
		echo "Machine is giving ping response"
	else
		echo "Machine is not pinging"
	fi
else
	echo "IP Address is empty"
fi

$ ./ipaddr.sh
Enter the Ipaddress
10.176.191.106

Pinging 10.176.191.106 with 32 bytes of data:

Reply from 10.176.191.106: bytes=32 time&lt;1ms TTL=128

Ping statistics for 10.176.191.106:
    Packets: Sent = 1, Received = 1, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
Machine is giving ping response

#5. Installer Script
  # Installer script of most of the packages will not allow to execute those as a root user. Script checks the user who is executing and throws the error.

The following script, allows you to execute the oracle installer script only if the user who is executing is non root.

$ cat preinstaller.sh
#!/bin/bash
if [ `whoami` != 'root' ]; then
	echo "Executing the installer script"
	./home/oracle/databases/runInstaller.sh
else
	echo "Root is not allowed to execute the installer script"
fi

Executing the script as a root user,
# ./preinstaller.sh
Root is not allowed to execute the installer script
In this example the output of the command whoami is compared with the word “root”. For string comparison ==, !=, &lt; and should be used and for numeric comparison eq, ne,lt and gt should be used.

#6. Enhanced brackets
  # In all the above examples, we used only single brackets to enclose the conditional expression, but bash allows double brackets which serves as an enhanced version of the single-bracket syntax.
  
  $ cat enhanced.sh
#!/bin/bash
echo "Enter the string"
read str
if [[ $str == *condition* ]]
then
	echo "String "$str has the word \"condition\"
fi

$ ./enhanced.sh
Enter the string
conditionalstatement
String conditionalstatement has the word "condition"

[ is a synonym for test command. Even if it is built in to the shell it creates a new process.
[[ is a new improved version of it, which is a keyword, not a program.
[[ is understood by Korn and Bash.
In the above example, if the variable $str contains the phrase “condition” anywhere, the condition is true.
This is the shell globbing feature, which will be supported only when you use [[ (double brackets) and therefore many arguments need not be quoted.
