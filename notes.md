# Linux training
```
shebangs run from root context

/usr/local/bin - System wide scripts


~/.bashrc is $profile
```

# Typeset, typing shell variables? 
```
lg@centos01:~/linuxlab$ typeset -i count=21^C                                                                           
lg@centos01:~/linuxlab$ count="test"
lg@centos01:~/linuxlab$ echo $count                                                                                     
0
```
# Setting an array in a shell script. 
```
lg@centos01:~/linuxlab$ A="{test test1 test2}"^C
lg@centos01:~/linuxlab$ A=(Test Test1 Test2)
lg@centos01:~/linuxlab$ echo ${A[0]}
Test
lg@centos01:~/linuxlab$ echo ${A[1]}                                                                                    
Test1
lg@centos01:~/linuxlab$ echo ${A[2]}                                                                                    
Test2
```
# String Slicing? 
```
lg@centos01:~/linuxlab$ A="MyString REMOVEME"
lg@centos01:~/linuxlab$ echo ${A%REMOVEME}
MyString
```
# String Length
```
lg@centos01:~/linuxlab$ 
lg@centos01:~/linuxlab$ echo ${#A}
17
```
# Reading input
```
lg@centos01:~/linuxlab$ echo "Enter your name"
Enter your name
lg@centos01:~/linuxlab$ read name
Luke
lg@centos01:~/linuxlab$ echo $name
Luke
```
# Command substitution (SubExpression)
```
A = $(echo "My Output")
```

# Date Strings 
```
lg@centos01:~/linuxlab$ date '+%m%d'
0326

$ man date # For more detailed documentation
```
# Evaluating calculations
```
lg@centos01:~/linuxlab$ (( i = 1 + 2 ))
lg@centos01:~/linuxlab$ echo $i
3
```
# Exit codes can be checked with $?
```
lg@centos01:~/linuxlab$ tail shellarguments.sh -c 10
"

exit 1
lg@centos01:~/linuxlab$ sh shellarguments.sh 
  0$&lg@centos01:~/linuxlab$ echo $?
1
```
# Exit codes on grep

Use exit codes with silent grep to find match 

```
lg@centos01:~/linuxlab$ grep -q exit shellarguments.sh
lg@centos01:~/linuxlab$ echo $?
0
lg@centos01:~/linuxlab$ grep -q blagh shellarguments.sh
lg@centos01:~/linuxlab$ echo $?
1
lg@centos01:~/linuxlab$ cat shellarguments.sh 



printf "$1 $2 $3"

printf "$#"

printf "$*"



exit 1

```

# If Statments

use the "[[" command finished with "]]" to evaluate conditions.

```
lg@centos01:~/linuxlab$ if [[ 1 == 1 ]] ; then echo "Hello"; fi
Hello
```

# OR as a simple if then.

They've used the OR || pipe to stop as soon its true.

command execution like

command || command

if first pipe is true, wont execute the remaining as logically the condition is already true 

```
lg@centos01:~/linuxlab$ echo 1
1
lg@centos01:~/linuxlab$ echo 1 || echo 2
1
lg@centos01:~/linuxlab$ echo 0 || echo 2
0
lg@centos01:~/linuxlab$ 0 || echo 2
-bash: 0: command not found
2
lg@centos01:~/linuxlab$ ping 8.8.8.8 || echo 2
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=63 time=11.9 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=63 time=12.7 ms
^C
--- 8.8.8.8 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1011ms
rtt min/avg/max/mdev = 11.941/12.347/12.753/0.406 ms
lg@centos01:~/linuxlab$ ping 8.8.8.8 -c 1 || echo 2
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=63 time=11.6 ms

--- 8.8.8.8 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 11.626/11.626/11.626/0.000 ms
lg@centos01:~/linuxlab$ ping 888.8.8.8 -c 1 || echo 2
ping: 888.8.8.8: Name or service not known
2

```

if the command executes, second part of the pipe is not executed, due to the OR.

This is order of precedence? using C presence.

Alternatively, you can use and (&&) to only execute a command if is completes 

```
lg@centos01:~/linuxlab$ ping 888.8.8.8 -c 1 $$ echo 2
ping: 888.8.8.8: Name or service not known
lg@centos01:~/linuxlab$ ping 8.8.8.8 -c 1 && echo 2
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=63 time=14.0 ms

--- 8.8.8.8 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 14.065/14.065/14.065/0.000 ms
2
```


# Swich / Case 

end of a line is ";;" break, or ";&" to drop through

```
case $var in 
    big*) echo "Tiger!" ;;
    tabby) ccho "CAT!" ;& # Dont break, keep going
    ....
```