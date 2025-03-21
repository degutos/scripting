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

```
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

```
$ cat check_dir.sh 
if [ -d "/home/bob/caleston" ]
then
  echo "Directory exists"
else
  echo "Directory not found"
fi
```

## check greater of 2 numbers

```
$ cat check_greater.sh 
if [ $1 -gt $2 ]
then
  echo "The greatest value is $1"
else
  echo "the greatest value is $2"
fi
```






