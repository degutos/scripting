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

