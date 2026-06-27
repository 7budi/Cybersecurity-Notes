- To start every bash scripts use a shebang
	- #!/bin/bash
	- #!/bin/sh
- To display output on bash:
	- echo "your text"
- To make a break line use empty echo
	- echo
- To make a variable do it like this 
	- Name="7budi"
- To call the variable 
	- echo "My name is $Name"  <- needs space before writing anything after calling, or ${Name} <- doesn't need space.
- The set command can be used to assign values to positional parameters.
	- set 1budi  2budi 3budi 4budi 5budi
	-            $1        $2       $3        $4      $5
- There are variables we can't use called system variable.
	- echo $USER <- prints the user name and cannot assign to it.
	- echo $SHELL <- prints the terminal shell type.
- To make arrays in bash we use 
	- var=("list1" "list2" "list3" "list4")
	- to display : echo ${var\[0]}
	- to get all : echo ${var\[@]}
	- to get index number : echo ${!var\[@]}
	- to get the length : echo ${#var\[@]}
	- to add element to the array: var\[4]="list5" 
	- to remove from array : unset var\[2]
- On bash there is 2 ways to accept input from user
	1. Read Function
	2. Arguments
1. for bash read the read command is used to accept input while the script is running
	- read -p " text here" var , the -p will make the input visible , and at the end we add a variable name.
	- read -sp " Password:" var , the -sp will make the input invisible.
	- read -a var , this make it accept arrays.
2. Arguments helps to get input before the script start.
	- echo " first argument : $1" , then just before running the script we add the value.
- The sleep command makes it to delay what ever the script is running.
- To do mathematical operations you have to do $((expersion))
	1. Arithmetic operation
		- $(( a + b ))
		- $(( a - b ))  , let "z=$((a - b))" , echo "z=$z"
		- $(( a * b))
		- $(( a / b))
		- $(( a ** b))
		- $(( a % b))
	2. Assignment Operations
		- a +=3
		- a-=3
		- a*=3
		- a/=3
	3. Comparison Operarors
		- Greater than -> -gt  ,  >
		- less than -> -lt  ,  <
		- Greater than and equal to -> -ge   ,  >=
		- Less than and equal to -> -le  , <=
		- Equal -> eq , ==
		- Not equal -> ne  ,  !=
- If else condition are to make a choice or check,
	- if \[ condition ]
	- then
	- echo " text"
	- elif \[ condition ]
	- then
	- echo "text "
	- else 
	- echo " text"
	- fi <- closing 
	- something to consider is if \[ ] is used and number we have to use the alphabetic comparison ,  \[ 2 -gt 1 ] , if it is a string its ok to use the sign comparison and if (( )) is used we use the sign comparison (( 3 > 2)).  
- There is also something called loop which can do this repeatedly.
	- For loop is given a certain number of time to do a task.
		- For num in {1..10}
		- do
		- echo $num
		- done
	- While loop is a kind where it will run until the condition becomes false.
		- while \[condition]
		- do 
		- echo " txt"
		- done
	- Until loop is the same as while it just run until it becomes true.
- We can make a function to to make a certain commands inside it and call it whenever we want
	- function () {
	- echo " Text"
	- }
	- function

NOTE:
Shebang
#!/bin/bash

Variables
name="7budi"
echo "$name"
echo "${name}Bud"

Arrays
arr=("one" "two" "three")
echo "${arr[0]}"
echo "${arr[@]}"

 User input
read -p "Enter IP: " ip

If/else
if [ "$ip" == "127.0.0.1" ]; then
    echo "Localhost"
elif [ "$ip" == "192.168.1.1" ]; then
    echo "Gateway"
else
    echo "Other"
fi

 Loops
for i in {1..10}; do
    echo "$i"
done

while [ $count -lt 5 ]; do
    echo "$count"
    ((count++))
done

Exit code
ping -c 1 8.8.8.8 > /dev/null 2>&1
if [ $? -eq 0 ]; then
    echo "Up"
fi