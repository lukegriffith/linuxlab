# Linux training

shebangs run from root context

/usr/local/bin - System wide scripts


~/.bashrc is $profile


# Typeset, typing shell variables? 

lg@centos01:~/linuxlab$ typeset -i count=21^C                                                                           
lg@centos01:~/linuxlab$ count="test"
lg@centos01:~/linuxlab$ echo $count                                                                                     
0

# Setting an array in a shell script. 
lg@centos01:~/linuxlab$ A="{test test1 test2}"^C
lg@centos01:~/linuxlab$ A=(Test Test1 Test2)
lg@centos01:~/linuxlab$ echo ${A[0]}
Test
lg@centos01:~/linuxlab$ echo ${A[1]}                                                                                    
Test1
lg@centos01:~/linuxlab$ echo ${A[2]}                                                                                    
Test2

# String Slicing? 
lg@centos01:~/linuxlab$ A="MyString REMOVEME"
lg@centos01:~/linuxlab$ echo ${A%REMOVEME}
MyString

# String Length

lg@centos01:~/linuxlab$ 
lg@centos01:~/linuxlab$ echo ${#A}
17

# Reading input

lg@centos01:~/linuxlab$ echo "Enter your name"
Enter your name
lg@centos01:~/linuxlab$ read name
Luke
lg@centos01:~/linuxlab$ echo $name
Luke

