# Experiment 3: System Calls - Fork, Exit, Getpid, Wait, Close

## Ex. No: 3

### Aim
To study and implement process management system calls such as `fork()`, `getpid()`, `wait()`, `exit()`, and `close()` using C programming and equivalent shell scripting commands.

---

### System Calls Used

1. **`fork()`**: Used to create a new child process.
   - *Syntax:* `pid_t pid = fork();`
2. **`getpid()`**: Returns the Process ID of the current calling process.
   - *Syntax:* `pid_t pid = getpid();`
3. **`getppid()`**: Returns the Parent Process ID of the current process.
   - *Syntax:* `pid_t ppid = getppid();`
4. **`wait()`**: Suspends execution of the parent process until its child process terminates.
   - *Syntax:* `wait(NULL);`
5. **`exit()`**: Terminates the currently executing process.
   - *Syntax:* `exit(0);`
6. **`close()`**: Closes an opened file descriptor.
   - *Syntax:* `close(fd);`

---

## Program 1: Process Creation using `fork()`, `getpid()`, `wait()`, and `exit()`

### Algorithm
1. Declare a variable `pid` of type `pid_t`.
2. Create a child process using `fork()`.
3. If `pid < 0`, display "Fork Failed" and exit.
4. If `pid == 0`, it is the child process:
   - Display Child PID (`getpid()`) and Parent PID (`getppid()`).
   - Terminate child process using `exit(0)`.
5. If `pid > 0`, it is the parent process:
   - Parent waits for child completion using `wait(NULL)`.
   - Display parent process details.
6. Stop.

### C Program
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main()
{
    pid_t pid;

    pid = fork();

    if(pid < 0)
    {
        printf("Fork Failed\n");
        exit(1);
    }
    else if(pid == 0)
    {
        printf("\nCHILD PROCESS");
        printf("\nChild PID : %d", getpid());
        printf("\nParent PID : %d\n", getppid());
        exit(0);
    }
    else
    {
        wait(NULL);
        printf("\nPARENT PROCESS");
        printf("\nParent PID : %d", getpid());
        printf("\nParent's Parent PID : %d\n", getppid());
    }

    return 0;
}
```

### Shell Script Equivalent
```bash
#!/bin/bash
echo "Parent Process ID : $$"
(
    echo "Child Process ID : $$"
    echo "Parent Process ID : $PPID"
    exit 0
) &

wait
echo "Child Process Completed"
```

### Output 1
```text
CHILD PROCESS
Child PID : 4512
Parent PID : 4511

PARENT PROCESS
Parent PID : 4511
Parent's Parent PID : 2304
```

---

## Program 2: `wait()` System Call

### C Program
```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main()
{
    pid_t pid;
    pid = fork();

    if(pid == 0)
    {
        printf("Child Process Running\n");
        sleep(5);
        printf("Child Process Completed\n");
    }
    else
    {
        wait(NULL);
        printf("Parent Resumes Execution\n");
    }

    return 0;
}
```

### Shell Script Equivalent
```bash
#!/bin/bash
(
    echo "Child Process Running"
    sleep 5
    echo "Child Process Completed"
) &

wait
echo "Parent Resumes Execution"
```

### Output 2
```text
Child Process Running
Child Process Completed
Parent Resumes Execution
```

---

## Program 3: `close()` System Call

### C Program
```c
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main()
{
    int fd;
    fd = open("sample.txt", O_RDONLY | O_CREAT, 0644);

    if(fd < 0)
    {
        printf("File Opening Failed\n");
        return 1;
    }

    printf("File Opened Successfully (fd = %d)\n", fd);

    close(fd);
    printf("File Closed Successfully\n");

    return 0;
}
```

### Shell Script Equivalent
```bash
#!/bin/bash
touch sample.txt
exec 3< sample.txt
echo "File Opened Successfully"
exec 3<&-
echo "File Closed Successfully"
```

### Output 3
```text
File Opened Successfully (fd = 3)
File Closed Successfully
```

---

### Compilation and Execution

#### Compiling & Running C Programs:
```bash
gcc process.c -o process
./process
```

#### Executing Shell Scripts:
```bash
chmod +x process.sh
./process.sh
```

---

### Inference
The process management system calls `fork()`, `getpid()`, `wait()`, `exit()`, and `close()` were studied and implemented successfully. The creation of child processes, process synchronization, process termination, process identification, and file descriptor management were understood through both C programs and shell scripting equivalents.

### Result
Thus, the programs for Process Management using system calls `fork()`, `getpid()`, `wait()`, `exit()`, and `close()` were executed successfully using C programming and Shell scripting, and the outputs were verified.
