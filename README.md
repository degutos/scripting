# README

This is my shell script repository to train some shell script commands and program.


## First script

```sh
$ cat create-and-launch-rocket 
mkdir lunar-mission
rocket-add lunar-mission
rocket-start-power lunar-mission
rocket-internal-power lunar-mission
rocket-start-sequence lunar-mission
rocket-start-engine lunar-mission
rocket-lift-off lunar-mission
rocket-status lunar-mission 


$ cat ./create-directory-structure.sh
mkdir /home/bob/countries
mkdir /home/bob/countries/USA
mkdir /home/bob/countries/UK
mkdir /home/bob/countries/India

touch /home/bob/countries/USA/capital.txt
touch /home/bob/countries/UK/capital.txt
touch /home/bob/countries/India/capital.txt

echo "Washington, D.C" >  /home/bob/countries/USA/capital.txt
echo "London" > /home/bob/countries/UK/capital.txt
echo "New Delhi" > /home/bob/countries/India/capital.txt

uptime

$ ./create-directory-structure.sh 
 18:28:47 up 15 min,  0 users,  load average: 0.37, 1.16, 1.47


$ cat backup-file.sh 
# This script creates a backup of a given file by creating a copy as bkp
# For example some-file is backed up as some-file_bkp

file_name="create-and-launch-rocket"

cp $file_name $file_name"_bkp"


$ cat create_files.sh 
FILE01="Japan"
FILE02="Egypt"
FILEO3="Canada"

cd /home/bob

echo "Creating file called $FILE01"
touch $FILE01

echo "Creating file called $FILE02"
touch $FILE02

echo "Creating file called $FILEO3"
touch $FILEO3



$ cat logged_username.sh 
echo "My name is $USER"



```

## script with command line argument (as a variable)

```sh
$ cat create-and-launch-rocket 
mission_name=$1

mkdir $mission_name

rocket-add $mission_name

rocket-start-power $mission_name
rocket-internal-power $mission_name
rocket-start-sequence $mission_name
rocket-start-engine $mission_name
rocket-lift-off $mission_name

rocket-status $mission_name
```

```sh
$ cat print-capital.sh 
country=$1
capital=$2

echo "Capital city of $country is $capital"

$ ./print-capital.sh UK London
Capital city of UK is London

$ ./print-capital.sh Nigeria Abuja
Capital city of Nigeria is Abuja

```

- Another sample:

```sh
$ cat backup-file.sh 
# This script creates a backup of a given file by creating a copy as bkp
# For example some-file is backed up as some-file_bkp
set -e

file_name=$1

cp $file_name ${file_name}_bkp

echo "Done"

$ ./backup-file.sh print-capital.sh
Done
bob@caleston-lp10:~$ ls   
backup-file.sh  create-and-launch-rocket  lunar-mission  media  print-capital.sh  print-capital.sh_bkp

```

- Another sample:

```sh
$ cat update_shell.sh 
new_shell="$2"
user_name="$1"
usermod -s $new_shell  $user_name 
```

## Expression arithmetic

```
➜  scripting git:(main) ✗ expr 6 + 3                                                           
9
➜  scripting git:(main) ✗ expr 6 - 3 
3
➜  scripting git:(main) ✗ expr 6 / 3
2
➜  scripting git:(main) ✗ expr 6 \* 3
18
```

---


> [!Note]
> Note that we must type space between numbers and math signal
> Note that in case multiplication with `*` we must use `\` example:
> `$ expr 6 \* 3`

- Another way is using double parenthesis (( ))
  

```
 ✗ A=6                                  
➜  B=3
➜  echo $((A+B))
9
```

Note: using parenthesis we no longer need add $ to a variable and no need to use `\` backslash to your `*`
multiplication 

#### Increasing variable

```sh
✗ echo $((++A))
7
```

```sh
we can also use --A
A++
A-- 
```

> [!Note]
> Expression doesn't work with float numbers, only with integer.


#### working with float numbers


```
➜  A=6                 
➜  B=3                 
➜  echo $A / $B | bc -l
2.00000000000000000000
```

#### working with expression

```sh
$ cat calculation.sh 
A=20
B=10

echo "Sum is $((A + B)) "

echo "Difference is $((A - B))"

echo "Product is $((A * B))"

echo "Quotient is $((A / B))"


$ ./calculation.sh 
Sum is 30 
Difference is 10
Product is 200
Quotient is 2

```

- Passing parameter at the CLI
  
```sh
$ cat calculation.sh 
A=$1
B=$2

echo "Sum is $((A + B)) "

echo "Difference is $((A - B))"

echo "Product is $((A * B))"

echo "Quotient is $((A / B))"
bob@caleston-lp10:~$ ./calculation.sh 20 10
Sum is 30 
Difference is 10
Product is 200
Quotient is 2
```

```sh
$ cat calculate-price.sh 
A=$1
B=$2

echo "The total price for items is $((A * B)) "
bob@caleston-lp10:~$ ./calculate-price.sh 10 20
The total price for items is 200 
```


```sh
$ cat calculate-price.sh 
price=$(( $1 * $2 ))

echo "The total price for items is ${price} dollars"
bob@caleston-lp10:~$ ./calculate-price.sh 10 20
The total price for items is 200 dollars
```

```sh
$ cat calculate-total-apples.sh 
baskets=4
apples_per_basket=5

total_apples=`expr $baskets \* $apples_per_basket`

echo "Total Apples = ${total_apples}"

$ ./calculate-total-apples.sh 
Total Apples = 20

```

## Condition logic statement

Lets use IF statement:

```sh
$ cat ./create-and-launch-rocket 
mission_name=$1

mkdir $mission_name

rocket-add $mission_name

rocket-start-power $mission_name
rocket-internal-power $mission_name
rocket-start-sequence $mission_name
rocket-start-engine $mission_name
rocket-lift-off $mission_name

rocket_status=$(rocket-status $mission_name)

echo "The status of launch is $rocket_status"

if [[ $rocket_status = "failed" ]] 
then
   rocket-debug $mission_name
fi
```

## Print month 

```sh
$ cat print-month-name.sh 
month_number=$1

if [ -z $month_number ]  ## check if it was passed as parameter
then
  echo "No month number given"
  echo "eg: ./print-month-number 5"
  exit
fi

# check if month_number is between 1 and 12
if [[ $month_number -lt 1 ]] || [[ $month_number -gt 12 ]]
then
  echo "Invalid month number given. Please enter a valid number - 1 to 12"
  exit
fi

if [ $month_number -eq 1 ]
then
  echo "January"
elif [ $month_number -eq 2 ]
then
  echo "February"
elif [ $month_number -eq 3 ]
then
  echo "March"
elif  [ $month_number -eq 4 ]
then
  echo "April"
elif [ $month_number -eq 5 ]
then
  echo "May"
elif [ $month_number -eq 6 ]
then
  echo "June"
elif [ $month_number -eq 7 ]
then
  echo "July"
elif [ $month_number -eq 8 ]
then
  echo "August"
elif [ $month_number -eq 9 ]
then
  echo "September"
elif [ $month_number -eq 10 ]
then
  echo "October"
elif [ $month_number -eq 11 ]
then
  echo "November"
elif [ $month_number -eq 12 ]
then
  echo "December"
fi
```

## check_dir if exists or not

```sh
$ cat check_dir.sh 
if [ -d "/home/bob/caleston" ]
then
  echo "Directory exists"
else
  echo "Directory not found"
fi
```

## check greater of 2 numbers

```sh
$ cat check_greater.sh 
if [ $1 -gt $2 ]
then
  echo "The greatest value is $1"
else
  echo "the greatest value is $2"
fi
```


# FOR looping


```sh
$ cat launch-rockets.sh 
for mission in $(cat /home/bob/mission-names.txt)
do
  bash /home/bob/create-and-launch-rocket $mission 
done
```

```sh
$ cat loop.sh 
for numbers in $(seq 31 40)
do
  echo $numbers
done
```

## For looping to get a list of apps and check the logs:

```sh
$ cat count-requests.sh 
  echo -e " Log name   \t      GET      \t      POST    \t   DELETE "
  echo -e "------------------------------------------------------------"

for system in  $(cat /home/bob/apps.txt)
do
  get_requests=$(cat /var/log/apps/${system}_app.log | grep "GET" | wc -l)
  post_requests=$(cat /var/log/apps/${system}_app.log | grep "POST" | wc -l)
  delete_requests=$(cat /var/log/apps/${system}_app.log | grep "DELETE" | wc -l)
  echo -e " ${system}    \t ${get_requests}    \t    ${post_requests}   \t   ${delete_requests}"
done
```

```sh
$ cat rename-images.sh 
for images in $(ls /home/bob/images/) 
do
  if [[ $images = *.jpeg ]] 
  then 
    new_name=$(echo $images| sed 's/jpeg/jpg/g')
    mv images/$images images/$new_name
  fi
done
```

## While looping 

```sh
$ cat create-and-launch-rocket 
mission_name=$1

mkdir $mission_name

rocket-add $mission_name

rocket-start-power $mission_name
rocket-internal-power $mission_name
rocket-start-sequence $mission_name
rocket-start-engine $mission_name
rocket-lift-off $mission_name

rocket_status=$(rocket-status $mission_name)

echo "The status of launch is $rocket_status"

while [ $rocket_status = "launching" ]
do
  sleep 2
  rocket_status=$(rocket-status $mission_name)
done

if [ $rocket_status = "failed" ]
then
  rocket-debug
fi
```

```sh
$ cat print-numbers.sh 
to_number=$1
number=0
while [ $number -lt $to_number ]
do
  echo $(( number++ ))
done
```

```sh
$ cat print-numbers.sh 
to_number=$1
number=0
while [ $number -lt $to_number ]
do
  echo $(( number++ ))
done
```

### Calculator

```sh
$ cat calculator.sh 
while true
do 
  echo -e "1. Add"
  echo -e "2. Subtract"
  echo -e "3. Multiply"
  echo -e "4. Divide"
  echo -e "5. Quit"
  read -p "Enter with your option" option
  
  if [ $option != 5 ]
  then
    read -p "Enter number1: " number1
    read -p "Enter number2: " number2
  fi

  if [ $option -eq 1 ]
  then
    echo answer=$(( $number1 + $number2 ))
  elif [ $option -eq 2 ]
  then
    echo answer=$(( $number1 - $number2 ))
  elif [ $option -eq 3 ]
  then
    echo answer=$(( $number1 * $number2 ))
  elif [ $option -eq 4 ]
  then
    echo answer=$(( $number1 / $number2 ))
  elif [ $option -eq 5 ]
  then
    break
  fi
  
  
done
```


# Case in

```sh
$ cat print-pkm.sh 

os=$1

case $os in
  "Fedora") echo "Uses RPM package manager"
  ;;
  "RHEL") echo "Uses RPM package manager"
  ;;
  "CentOS") echo "Uses RPM package manager"
  ;;
  "Debian") echo "Uses DEB package manager" ;;

  "Ubuntu") echo "Uses DEB package manager" ;;
esac
```


### Lets convert the script with case in 

```sh
$ cat print-month-name.sh 
month_number=$1

if [ -z $month_number ]
then
  echo "No month number given. Please enter a month number as a command line argument."
  echo "eg: ./print-month-number 5"
  exit
fi

if [[ $month_number -lt 1 || $month_number -gt 12 ]]
then
  echo "Invalid month number given. Please enter a valid number - 1 to 12."
  exit
fi

case $month_number in
  1) echo "January" ;;
  2) echo "February" ;;
  3) echo "March" ;;
  4) echo "April" ;;
  5) echo "May" ;;
  6) echo "June" ;;
  7) echo "July" ;;
  8) echo "August" ;;
  9) echo "September" ;;
  10) echo "October" ;;
  11) echo "November" ;;
  12) echo "December" ;;
esac
```

## Calculator as case in

```sh
$ cat calculator.sh 

while true
do
  echo "1. Add"
  echo "2. Subtract"
  echo "3. Multiply"
  echo "4. Divide"
  echo "5. Quit"

  read -p "Enter your choice: " choice

  case $choice in 
          1) 
            read -p "Enter Number1: " number1
            read -p "Enter Number2: " number2
            echo Answer=$(( $number1 + $number2 ))
            ;;
          2)
            read -p "Enter Number1: " number1
            read -p "Enter Number2: " number2
            echo Answer=$(( $number1 - $number2 ))
            ;;
          3) 
            read -p "Enter Number1: " number1
            read -p "Enter Number2: " number2
            echo Answer=$(( $number1 * $number2 ))
            ;;
          4) 
            read -p "Enter Number1: " number1
            read -p "Enter Number2: " number2
            echo Answer=$(( $number1 / $number2 ))
            ;;
          5) 
            break
            ;;

  esac
done
```

Calculator with average

```sh
$ cat calculator.sh 

while true
do
  echo "1. Add"
  echo "2. Subtract"
  echo "3. Multiply"
  echo "4. Divide"
  echo "5. Average"
  echo "6. Quit"

  read -p "Enter your choice: " choice

  case $choice in 
          1) 
            read -p "Enter Number1: " number1
            read -p "Enter Number2: " number2
            echo Answer=$(( $number1 + $number2 ))
            ;;
          2)
            read -p "Enter Number1: " number1
            read -p "Enter Number2: " number2
            echo Answer=$(( $number1 - $number2 ))
            ;;
          3) 
            read -p "Enter Number1: " number1
            read -p "Enter Number2: " number2
            echo Answer=$(( $number1 * $number2 ))
            ;;
          4) 
            read -p "Enter Number1: " number1
            read -p "Enter Number2: " number2
            echo Answer=$(( $number1 / $number2 ))
            ;;
          5)
            read -p "Enter Number1: " number1
            read -p "Enter Number2: " number2
            echo Answer=$(( ($number1 + $number2) / 2 ))
            ;;
          6) 
            break
            ;;

  esac
done
```

### print color 

```sh
$ cat print-color.sh 
color=$1
red=`tput setaf 1`
green=`tput setaf 2`
reset=`tput sgr0`

    case $color in
        red) echo "${red}this is red${reset}";;
        green) echo "${green}this is green${reset}";;
        *) echo "red and green are the only choices"
    esac
```

## Bash


```
$ cat loop.sh 
for i in {31..40}
do
        echo $i
```

look what happen when we use in bourn shell sh

```sh
donebob@caleston-lp10:~$ sh
$ ./loop.sh
{31..40}
```

To fix the above error we can add a shebang to script

```sh
$ cat loop.sh
#!/bin/bash
for i in {31..40}
do
        echo $i
done
```

Now when we run the script it works:

```sh
$ ./loop.sh
31
32
33
34
35
36
37
38
39
40
```

```sh
$ cat print_number4.sh 
#!/bin/bash
echo {1..10}
```

### Using exit code when error

```
$ cat create-and-launch-rocket 
mission_name=$1

mkdir $mission_name

rocket-add $mission_name

rocket-start-power $mission_name
rocket-internal-power $mission_name
rocket-start-sequence $mission_name
rocket-start-engine $mission_name
rocket-lift-off $mission_name

rocket_status=$(rocket-status $mission_name)

echo "The status of launch is $rocket_status"

if [ $rocket_status = "launching" ]
then
  sleep 2
  rocket_status=$(rocket-status $mission_name)
fi

if [ $rocket_status = "failed" ]
then
  rocket-debug
  exit 25
fi
```

# Functions

```sh
$ cat create-directories.sh 
function prepare-directory-structure() {
  mkdir apps
  cd apps
  mkdir app1 app2 app3
  touch app1/logs app2/logs app3/logs
}

prepare-directory-structure
```


Another example:

```sh
#!/bin/bash
function add(){
  sum=$(( $1 + $2 ))
  echo $sum
}

result=$(add 3 5)
echo "The result is $result"
```

> [!Note]
> The function must echo the result so that it can be captured in the result variable.

---

## Calculator with function

```sh
$ cat calculator.sh 
#!/bin/bash

function read_numbers(){
    read -p "Enter Number1: " number1
    read -p "Enter Number2: " number2
}

while true
do
  echo "1. Add"
  echo "2. Subtract"
  echo "3. Multiply"
  echo "4. Divide"
  echo "5. Quit"

  read -p "Enter your choice: " choice


  case $choice in
    1)
        read_numbers
        echo $(( $number1 + $number2 ))
        ;;
    2)
        read_numbers
        echo $(( $number1 - $number2 ))
        ;;

    3)
        read_numbers
        echo $(( $number1 * $number2 ))
        ;;
    4)
        read_numbers
        echo $(( $number1 / $number2 ))
        ;;
    5)
        break
        ;;
  esac

done
```

Another example with functions:

```sh
$ cat create-and-launch-rocket 
function launch_rocket(){

  mission_name=$1

  mkdir $mission_name

  rocket-add $mission_name

  rocket-start-power $mission_name
  rocket-internal-power $mission_name
  rocket-start-sequence $mission_name
  rocket-start-engine $mission_name
  rocket-lift-off $mission_name

  rocket_status=$(rocket-status $mission_name)

  echo "The status of launch is $rocket_status"

  if [ $rocket_status = "launching" ]
  then
    sleep 2
    rocket_status=$(rocket-status $mission_name)
  fi

  if [ $rocket_status = "failed" ]
  then
    rocket-debug
  fi
}

mission=$1
launch_rocket $mission
```

# ShellCheck

```sh
$ apt-get install shellcheck
$ yum install shellcheck
```


# Project LAMP

This project will deploy a:
- Linux
- Apache
- Mysql
- PHP

```sh
#!/bin/bash
#
# Automate ECommerce Application Deployment
# Author: Mumshad Mannambeth

#######################################
# Print a message in a given color.
# Arguments:
#   Color. eg: green, red
#######################################
function print_color(){
  NC='\033[0m' # No Color

  case $1 in
    "green") COLOR='\033[0;32m' ;;
    "red") COLOR='\033[0;31m' ;;
    "*") COLOR='\033[0m' ;;
  esac

  echo -e "${COLOR} $2 ${NC}"
}

#######################################
# Check the status of a given service. If not active exit script
# Arguments:
#   Service Name. eg: firewalld, mariadb
#######################################
function check_service_status(){
  service_is_active=$(sudo systemctl is-active $1)

  if [ $service_is_active = "active" ]
  then
    echo "$1 is active and running"
  else
    echo "$1 is not active/running"
    exit 1
  fi
}

#######################################
# Check the status of a firewalld rule. If not configured exit.
# Arguments:
#   Port Number. eg: 3306, 80
#######################################
function is_firewalld_rule_configured(){

  firewalld_ports=$(sudo firewall-cmd --list-all --zone=public | grep ports)

  if [[ $firewalld_ports == *$1* ]]
  then
    echo "FirewallD has port $1 configured"
  else
    echo "FirewallD port $1 is not configured"
    exit 1
  fi
}

#######################################
# Check if a given item is present in an output
# Arguments:
#   1 - Output
#   2 - Item
#######################################
function check_item(){
  if [[ $1 = *$2* ]]
  then
    print_color "green" "Item $2 is present on the web page"
  else
    print_color "red" "Item $2 is not present on the web page"
  fi
}






echo "---------------- Setup Database Server ------------------"

# Install and configure firewalld
print_color "green" "Installing FirewallD.. "
sudo yum install -y firewalld

print_color "green" "Installing FirewallD.. "
sudo systemctl start firewalld
sudo systemctl enable firewalld

# Check FirewallD Service is running
check_service_status firewalld

# Install and configure Maria-DB
print_color "green" "Installing MariaDB Server.."
sudo yum install -y mariadb-server

print_color "green" "Starting MariaDB Server.."
sudo systemctl start mariadb
sudo systemctl enable mariadb

# Check FirewallD Service is running
check_service_status mariadb

# Configure Firewall rules for Database
print_color "green" "Configuring FirewallD rules for database.."
sudo firewall-cmd --permanent --zone=public --add-port=3306/tcp
sudo firewall-cmd --reload

is_firewalld_rule_configured 3306


# Configuring Database
print_color "green" "Setting up database.."
cat > setup-db.sql <<-EOF
  CREATE DATABASE ecomdb;
  CREATE USER 'ecomuser'@'localhost' IDENTIFIED BY 'ecompassword';
  GRANT ALL PRIVILEGES ON *.* TO 'ecomuser'@'localhost';
  FLUSH PRIVILEGES;
EOF

sudo mysql < setup-db.sql

# Loading inventory into Database
print_color "green" "Loading inventory data into database"
cat > db-load-script.sql <<-EOF
USE ecomdb;
CREATE TABLE products (id mediumint(8) unsigned NOT NULL auto_increment,Name varchar(255) default NULL,Price varchar(255) default NULL, ImageUrl varchar(255) default NULL,PRIMARY KEY (id)) AUTO_INCREMENT=1;

INSERT INTO products (Name,Price,ImageUrl) VALUES ("Laptop","100","c-1.png"),("Drone","200","c-2.png"),("VR","300","c-3.png"),("Tablet","50","c-5.png"),("Watch","90","c-6.png"),("Phone Covers","20","c-7.png"),("Phone","80","c-8.png"),("Laptop","150","c-4.png");

EOF

sudo mysql < db-load-script.sql

mysql_db_results=$(sudo mysql -e "use ecomdb; select * from products;")

if [[ $mysql_db_results == *Laptop* ]]
then
  print_color "green" "Inventory data loaded into MySQl"
else
  print_color "green" "Inventory data not loaded into MySQl"
  exit 1
fi


print_color "green" "---------------- Setup Database Server - Finished ------------------"

print_color "green" "---------------- Setup Web Server ------------------"

# Install web server packages
print_color "green" "Installing Web Server Packages .."
sudo yum install -y httpd php php-mysqlnd

# Configure firewalld rules
print_color "green" "Configuring FirewallD rules.."
sudo firewall-cmd --permanent --zone=public --add-port=80/tcp
sudo firewall-cmd --reload

is_firewalld_rule_configured 80

# Update index.php
sudo sed -i 's/index.html/index.php/g' /etc/httpd/conf/httpd.conf

# Start httpd service
print_color "green" "Start httpd service.."
sudo systemctl  start httpd
sudo systemctl enable httpd

# Check FirewallD Service is running
check_service_status httpd

# Download code
print_color "green" "Install GIT.."
sudo yum install -y git
sudo git clone https://github.com/kodekloudhub/learning-app-ecommerce.git /var/www/html/
sudo sed -i 's#// \(.*mysqli_connect.*\)#\1#' /var/www/html/index.php
sudo sed -i 's#// \(\$link = mysqli_connect(.*172\.20\.1\.101.*\)#\1#; s#^\(\s*\)\(\$link = mysqli_connect(\$dbHost, \$dbUser, \$dbPassword, \$dbName);\)#\1// \2#' /var/www/html/index.php

print_color "green" "Updating index.php.."
sudo sed -i 's/172.20.1.101/localhost/g' /var/www/html/index.php

print_color "green" "---------------- Setup Web Server - Finished ------------------"

# Test Script
web_page=$(curl http://localhost)

for item in Laptop Drone VR Watch Phone
do
  check_item "$web_page" $item
done
```





