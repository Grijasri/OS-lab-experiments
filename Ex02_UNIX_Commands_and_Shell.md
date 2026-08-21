# Experiment 2: Illustrate UNIX Commands and Shell Programming

## Ex. No: 2

---

## 2.1 Installation of Kali Linux on a Laptop

### Aim
To install Kali Linux operating system on a laptop and verify its successful installation and operation.

### Requirements
- Laptop/Desktop Computer
- Minimum 4 GB RAM (8 GB recommended)
- Minimum 20 GB free disk space
- USB Flash Drive (8 GB or higher)
- Kali Linux ISO Image
- Bootable USB Creation Tool (Rufus / Balena Etcher)

### Theory
Kali Linux is a Debian-based Linux distribution designed for penetration testing, cybersecurity research, digital forensics, and ethical hacking. It contains numerous security tools and utilities that assist in vulnerability assessment and network security analysis. Installing Kali Linux provides a secure environment for learning Linux commands, shell scripting, networking, and cybersecurity concepts.

### Procedure

#### Step 1: Download Kali Linux
1. Visit the official Kali Linux website (`https://www.kali.org`).
2. Download the latest Kali Linux Installer ISO image.

#### Step 2: Create a Bootable USB Drive
1. Insert the USB drive into the system.
2. Open Rufus or Balena Etcher bootable USB creation tool.
3. Select the downloaded Kali Linux ISO file.
4. Select the target USB device.
5. Click **Start** and wait for the process to complete.

#### Step 3: Configure BIOS/UEFI Settings
1. Restart the laptop.
2. Enter BIOS/UEFI Setup by pressing `F2`, `F12`, `DEL`, or `ESC` during startup.
3. Set the USB drive as the first boot device.
4. Save changes and restart.

#### Step 4: Start Kali Linux Installation
1. Boot from the USB drive.
2. Select **Graphical Install**.
3. Choose Language, Location, and Keyboard Layout.
4. Configure hostname and domain name if required.
5. Create a user account name and password.

#### Step 5: Disk Partitioning
1. Select **Guided - Use Entire Disk** or Manual Partitioning.
2. Allocate disk space for Kali Linux.
3. Confirm partition settings and write changes to disk.

#### Step 6: Install Base System
1. Wait for files to be copied.
2. Configure package manager settings.
3. Install the GRUB bootloader to the primary drive.

#### Step 7: Complete Installation
1. Finish installation and remove the USB drive.
2. Restart the system.
3. Log in using the created username and password.

---

### Commands Used for Verification

#### 1. Display Kernel Information
```bash
uname -a
```

#### 2. Display Operating System Details
```bash
cat /etc/os-release
```

#### 3. Display Current Logged-in User
```bash
whoami
```

#### 4. Display System Hostname
```bash
hostname
```

#### 5. Display CPU Hardware Information
```bash
lscpu
```

#### 6. Display Disk Space Usage
```bash
df -h
```

---

### Verification Output

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

### Inference (2.1)
- The Kali Linux operating system was successfully installed on the laptop.
- The system booted correctly, user accounts were created successfully, and Linux commands executed without errors.

---

## 2.2 UNIX Commands Reference & Execution

### General & System Commands
- `date`: Displays current system date and time (`date`, `date "+%H-%M-%S"`).
- `cal`: Displays calendar (`cal 2026`, `cal 6 2026`).
- `echo`: Prints text or messages (`echo Hello World`).
- `who`: Displays users currently logged in (`who`, `who -H`, `who -b`).
- `whoami`: Displays effective user ID (`whoami`).
- `tty`: Displays terminal name (`tty`).
- `bc`: Performs arbitrary precision calculator math.
- `clear`: Clears terminal screen (`clear`).
- `man`: Displays manual page (`man ls`).
- `tput`: Controls terminal display (`tput clear`, `tput smso`).

### Directory Related Commands
- `pwd`: Print working directory.
- `mkdir`: Create directory (`mkdir demo`).
- `cd`: Change directory (`cd demo`).
- `rmdir`: Remove empty directory (`rmdir demo`).

### File Related Commands
- `cat`: Create/view files (`cat > file.txt`, `cat file.txt`).
- `cp`: Copy file (`cp src.txt dst.txt`).
- `mv`: Move/rename file (`mv old.txt new.txt`).
- `rm`: Remove file (`rm file.txt`).
- `wc`: Word, line, char count (`wc -l file.txt`, `wc -w file.txt`).
- `sort`: Sort lines of text (`sort names.txt`).

### Filters, Pipes & Communication
- `head`: First N lines (`head -n 5 file.txt`).
- `tail`: Last N lines (`tail -n 5 file.txt`).
- `grep`: Pattern search (`grep "keyword" file.txt`).
- `|` (Pipe): Pass output of one command to another (`ls | wc -l`).
- `tr`: Translate/delete characters (`echo unix | tr "[a-z]" "[A-Z]"`).
- `wall`: Broadcast message (`wall "Server restart in 10 mins"`).

---

## 2.3 Shell Programming

### Program 1: Greatest Among Three Numbers (`greatest.sh`)

#### Aim
To write and execute a shell program to find the greatest among three given numbers.

#### Algorithm
1. Start.
2. Read three numbers `a`, `b`, and `c`.
3. Compare `a` with `b` and `c`. If `a` is greater than both, display `a`.
4. Else compare `b` with `c`. If `b` is greater, display `b`.
5. Otherwise display `c`.
6. Stop.

#### Shell Script
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

#### Sample Output
```text
ENTER THREE NUMBERS
25 40 18
40 is greater
```

---

### Program 2: Factorial of a Given Number (`factorial.sh`)

#### Aim
To write and execute a shell program to find the factorial of a given number.

#### Algorithm
1. Start.
2. Read a number `n`.
3. Initialize `fact = 1`.
4. Repeat while `n > 1`:
   - `fact = fact * n`
   - `n = n - 1`
5. Display `fact`.
6. Stop.

#### Shell Script
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

#### Sample Output
```text
ENTER THE NUMBER:
5
FACTORIAL OF THE GIVEN NUMBER IS 120
```

---

### Program 3: Sum of Odd Numbers up to N (`oddsum.sh`)

#### Aim
To write and execute a shell program to find the sum of odd numbers up to N.

#### Algorithm
1. Start.
2. Read the value of `N`.
3. Initialize `x = 1` and `sum = 0`.
4. While `x <= N`:
   - Add `x` to `sum`.
   - Increment `x` by 2.
5. Display `sum`.
6. Stop.

#### Shell Script
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

#### Sample Output
```text
ENTER THE RANGE:
10
SUM = 25
```

---

### Program 4: Generation of Fibonacci Numbers (`fibonacci.sh`)

#### Aim
To write and execute a shell program to generate Fibonacci numbers up to a given limit.

#### Algorithm
1. Read limit `n`.
2. Initialize `p = -1`, `q = 1`, `i = 1`.
3. Repeat while `i <= n`:
   - `r = p + q`
   - `p = q`
   - `q = r`
   - Display `r`
   - `i = i + 1`
4. Stop.

#### Shell Script
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

#### Sample Output
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

### Program 5: Arithmetic Calculator (`calculator.sh`)

#### Aim
To write and execute a shell program to implement an arithmetic calculator using the case statement.

#### Algorithm
1. Read values `a` and `b`.
2. Display the operation menu.
3. Read the user's option (`op`).
4. Perform the corresponding arithmetic operation using a case statement.
5. Display result and stop.

#### Shell Script
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

#### Sample Output
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

### Program 6: Largest Digit of a Number (`largestdigit.sh`)

#### Aim
To write and execute a shell program to find the largest digit in a given number.

#### Algorithm
1. Read a number `a`.
2. Initialize `max = 0`.
3. Extract each digit using modulo operator (`r = a % 10`).
4. If `r > max`, set `max = r`.
5. Reduce number (`a = a / 10`).
6. Repeat until `a == 0`.
7. Display `max`.

#### Shell Script
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

#### Sample Output
```text
ENTER THE NUMBER
58392
THE LARGEST DIGIT OF THE NUMBER: 9
```

---

### Program 7: Palindrome String Check (`palindrome.sh`)

#### Aim
To write and execute a shell program to check whether a given string is a palindrome.

#### Algorithm
1. Read a string `str`.
2. Find length `len` of string.
3. Compare `i`-th character from start and `len`-th character from end.
4. Move towards center.
5. If any pair differs, display not a palindrome and exit.
6. Otherwise display string is a palindrome.

#### Shell Script
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

#### Sample Output
```text
ENTER THE STRING TO CHECK PALINDROME
madam
madam is a palindrome
```

---

### Program 8: Reverse of a Given Number (`reverse.sh`)

#### Aim
To write and execute a shell program to find the reverse of a given number.

#### Algorithm
1. Read a number `n`.
2. Initialize `rnum = 0`.
3. Repeat while `n != 0`:
   - `remainder = n % 10`
   - `rnum = rnum * 10 + remainder`
   - `n = n / 10`
4. Display `rnum`.
5. Stop.

#### Shell Script
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

#### Sample Output
```text
ENTER THE NUMBER
12345
REVERSE OF THE NUMBER IS 54321
```

---

### Inference
The various shell programming concepts such as conditional statements, loops, arithmetic operations, string manipulation, process creation, and UNIX commands were studied and implemented successfully. The programs were executed in the Linux environment and the outputs were verified with expected results.

### Result
Thus, Kali Linux installation was verified, UNIX commands were studied and executed, and shell programs for greatest number, factorial, odd sum, Fibonacci series, calculator, largest digit, palindrome, and reverse of a number were executed successfully.
