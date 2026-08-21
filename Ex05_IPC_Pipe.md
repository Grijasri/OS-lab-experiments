# Experiment 5: Inter Process Communication (IPC) using Pipe

## Ex. No: 5

### Aim
To study and implement Inter Process Communication (IPC) between processes using Pipe Mechanism in UNIX.

---

### System Calls Used

1. **`pipe(fd)`**: Creates a unidirectional data channel (pipe) for IPC. `fd[0]` is open for reading, `fd[1]` for writing.
2. **`fork()`**: Creates a child process.
3. **`write(fd, buf, count)`**: Writes data from buffer to pipe descriptor.
4. **`read(fd, buf, count)`**: Reads data from pipe descriptor into buffer.
5. **`close(fd)`**: Closes unused file descriptors.
6. **`wait(NULL)`**: Suspends parent process until child process completes.

---

### Algorithm

#### Using Pipe Communication
1. Create a pipe using `pipe(fd)` system call.
2. Create a child process using `fork()`.
3. **If process is Child (`pid == 0`):**
   - Close the read end (`close(fd[0])`).
   - Write a message string into the pipe write end (`write(fd[1], ...)`).
   - Close the write end (`close(fd[1])`).
   - Terminate child process (`exit(0)`).
4. **If process is Parent (`pid > 0`):**
   - Wait for child process to finish (`wait(NULL)`).
   - Close the write end (`close(fd[1])`).
   - Read message from the pipe read end (`read(fd[0], ...)`).
   - Display the received message.
   - Close the read end (`close(fd[0])`).
5. Stop.

---

### C Program

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/wait.h>

int main()
{
    int fd[2];
    pid_t pid;
    char message[] = "Hello from Child Process";
    char buffer[100];

    if(pipe(fd) == -1)
    {
        printf("Pipe Creation Failed\n");
        return 1;
    }

    pid = fork();

    if(pid < 0)
    {
        printf("Fork Failed\n");
        return 1;
    }
    else if(pid == 0)
    {
        // Child Process: Writes to pipe
        close(fd[0]); // Close unused read end
        write(fd[1], message, strlen(message) + 1);
        close(fd[1]); // Close write end after writing
        exit(0);
    }
    else
    {
        // Parent Process: Reads from pipe
        wait(NULL);   // Wait for child to write
        close(fd[1]); // Close unused write end
        read(fd[0], buffer, sizeof(buffer));
        printf("Message received from child: %s\n", buffer);
        close(fd[0]); // Close read end
    }

    return 0;
}
```

---

### Shell Script Equivalents

#### Option 1: Unix Pipeline
```bash
#!/bin/bash
echo "Hello from Child Process" | cat
```

#### Option 2: Process Substitution / Subshell Reading
```bash
#!/bin/bash
(
    echo "Message from Child Process"
) | while read msg
do
    echo "Parent Received: $msg"
done
```

---

### Sample Output

```text
Message received from child: Hello from Child Process
```

```text
Parent Received: Message from Child Process
```

---

### Working Principle
- A pipe creates a communication channel between related processes.
- One process writes data into the pipe.
- Another process reads data from the pipe.
- Pipes support one-way (unidirectional) communication.
- Inter Process Communication (IPC) allows processes to exchange information and synchronize their activities.

---

### Inference
The Inter Process Communication (IPC) mechanism using pipes was studied and implemented successfully. The exchange of data between parent and child processes through a communication channel was understood using both C programming and shell scripting.

### Result
Thus, the program to illustrate Inter Process Communication (IPC) using Pipe Mechanism in UNIX was executed successfully and the output was verified.
