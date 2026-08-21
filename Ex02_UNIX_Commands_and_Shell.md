# Experiment 2: Illustrate UNIX Commands and Shell Programming

## 2.1 Kali Linux Verification Commands

### Commands
```bash
uname -a
cat /etc/os-release
whoami
hostname
lscpu
df -h
```

### Output
```text
$ uname -a
Linux kali 6.1.0-kali9-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.27-1kali1 (2023-05-12) x86_64 GNU/Linux

$ cat /etc/os-release
PRETTY_NAME="Kali GNU/Linux Rolling"
NAME="Kali GNU/Linux"
VERSION_ID="2023.2"
VERSION="2023.2"
ID=kali
ID_LIKE=debian

$ whoami
kali

$ hostname
kali

$ lscpu
Architecture:            x86_64
  CPU op-mode(s):        32-bit, 64-bit
  Address sizes:         39 bits physical, 48 bits virtual
  Byte Order:            Little Endian
CPU(s):                  4
  On-line CPU(s) list:   0-3

$ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            3.9G     0  3.9G   0% /dev
/dev/sda1        40G  9.8G   28G  26% /
```

---

## 2.2 UNIX Commands

```bash
# System & User Info
date
cal
echo "Hello World"
who
whoami
tty
bc
clear

# Directory Commands
pwd
mkdir demo
cd demo
rmdir demo

# File Commands
cat > file.txt
cat file.txt
cp file.txt copy.txt
mv copy.txt renamed.txt
rm renamed.txt
wc -l file.txt
sort file.txt

# Filters & Pipes
head -n 5 file.txt
tail -n 5 file.txt
grep "pattern" file.txt
ls | wc -l
echo unix | tr "[a-z]" "[A-Z]"
```

---

## 2.3 Shell Programming

### Program 1: Greatest Among Three Numbers

#### Code (`greatest.sh`)
```bash
#!/bin/bash
echo "ENTER THREE NUMBERS"
read a b c

if [ $a -gt $b ] && [ $a -gt $c ]
then
    echo "$a is greater"
elif [ $b -gt $c ]
then
    echo "$b is greater"
else
    echo "$c is greater"
fi
```

#### Output
```text
ENTER THREE NUMBERS
25 40 18
40 is greater
```

---

### Program 2: Factorial of a Given Number

#### Code (`factorial.sh`)
```bash
#!/bin/bash
echo "ENTER THE NUMBER:"
read n

fact=1

while [ $n -gt 1 ]
do
    fact=$((fact * n))
    n=$((n - 1))
done

echo "FACTORIAL OF THE GIVEN NUMBER IS $fact"
```

#### Output
```text
ENTER THE NUMBER:
5
FACTORIAL OF THE GIVEN NUMBER IS 120
```

---

### Program 3: Sum of Odd Numbers up to N

#### Code (`oddsum.sh`)
```bash
#!/bin/bash
echo "ENTER THE RANGE:"
read n

x=1
sum=0

while [ $x -le $n ]
do
    sum=$((sum + x))
    x=$((x + 2))
done

echo "SUM = $sum"
```

#### Output
```text
ENTER THE RANGE:
10
SUM = 25
```

---

### Program 4: Generation of Fibonacci Numbers

#### Code (`fibonacci.sh`)
```bash
#!/bin/bash
echo "ENTER THE LIMIT:"
read n

p=-1
q=1
i=1

while [ $i -le $n ]
do
    r=$((p + q))
    p=$q
    q=$r
    echo "$r"
    i=$((i + 1))
done
```

#### Output
```text
ENTER THE LIMIT:
7
0
1
1
2
3
5
8
```

---

### Program 5: Arithmetic Calculator

#### Code (`calculator.sh`)
```bash
#!/bin/bash
echo "ENTER THE VALUE OF A:"
read a
echo "ENTER THE VALUE OF B:"
read b

echo "ENTER THE OPTION TO PERFORM"
echo "1. ADDITION"
echo "2. SUBTRACTION"
echo "3. MULTIPLICATION"
echo "4. DIVISION"
read op

case "$op" in
    1) echo "Result = $((a + b))" ;;
    2) echo "Result = $((a - b))" ;;
    3) echo "Result = $((a * b))" ;;
    4) echo "Result = $((a / b))" ;;
    *) echo "Invalid Option" ;;
esac
```

#### Output
```text
ENTER THE VALUE OF A:
12
ENTER THE VALUE OF B:
4
ENTER THE OPTION TO PERFORM
1. ADDITION
2. SUBTRACTION
3. MULTIPLICATION
4. DIVISION
3
Result = 48
```

---

### Program 6: Largest Digit of a Number

#### Code (`largestdigit.sh`)
```bash
#!/bin/bash
echo "ENTER THE NUMBER"
read a

max=0

while [ $a -gt 0 ]
do
    r=$((a % 10))
    if [ $r -gt $max ]
    then
        max=$r
    fi
    a=$((a / 10))
done

echo "THE LARGEST DIGIT OF THE NUMBER: $max"
```

#### Output
```text
ENTER THE NUMBER
58392
THE LARGEST DIGIT OF THE NUMBER: 9
```

---

### Program 7: Palindrome String Check

#### Code (`palindrome.sh`)
```bash
#!/bin/bash
echo "ENTER THE STRING TO CHECK PALINDROME"
read str

len=$(echo -n "$str" | wc -c)
i=1
j=$((len / 2))

while [ $i -le $j ]
do
    k=$(echo "$str" | cut -c $i)
    l=$(echo "$str" | cut -c $len)
    
    if [ "$k" != "$l" ]
    then
        echo "$str is not a palindrome"
        exit
    fi
    
    i=$((i + 1))
    len=$((len - 1))
done

echo "$str is a palindrome"
```

#### Output
```text
ENTER THE STRING TO CHECK PALINDROME
madam
madam is a palindrome
```

---

### Program 8: Reverse of a Given Number

#### Code (`reverse.sh`)
```bash
#!/bin/bash
echo "ENTER THE NUMBER"
read n

rnum=0

while [ $n -ne 0 ]
do
    remainder=$((n % 10))
    rnum=$((rnum * 10 + remainder))
    n=$((n / 10))
done

echo "REVERSE OF THE NUMBER IS $rnum"
```

#### Output
```text
ENTER THE NUMBER
12345
REVERSE OF THE NUMBER IS 54321
```
