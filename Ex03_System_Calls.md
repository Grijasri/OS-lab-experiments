# Experiment 3: System Calls - Fork, Exit, Getpid, Wait, Close

## Program 1: Process Creation (`fork`, `getpid`, `wait`, `exit`)

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

### Shell Script
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

### Output
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

### Shell Script
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

### Output
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

### Shell Script
```bash
#!/bin/bash
touch sample.txt
exec 3< sample.txt
echo "File Opened Successfully"
exec 3<&-
echo "File Closed Successfully"
```

### Output
```text
File Opened Successfully (fd = 3)
File Closed Successfully
```
