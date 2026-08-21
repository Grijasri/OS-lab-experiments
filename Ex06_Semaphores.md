# Experiment 6: Semaphore Implementation (Mutual Exclusion)

## Ex. No: 6

### Aim
To implement Mutual Exclusion using Semaphore and ensure that only one process can access the critical section at a time.

---

### System Calls / Functions Used

1. **`sem_init(&sem, pshared, value)`**: Initializes an unnamed semaphore. `pshared = 1` enables sharing between processes.
2. **`sem_wait(&sem)`**: Performs wait (P) operation; decrements semaphore. If value becomes 0, process blocks.
3. **`sem_post(&sem)`**: Performs signal (V) operation; increments semaphore, waking up waiting process.
4. **`sem_destroy(&sem)`**: Destroys an initialized semaphore.
5. **`mmap(...)`**: Allocates POSIX shared memory accessible across process boundary created by `fork()`.
6. **`fork()`**: Spawns a child process.
7. **`wait(NULL)`**: Parent waits for child process termination.

---

### Algorithm

#### Semaphore-Based Mutual Exclusion
1. Initialize a counting/binary semaphore with value `1` in shared memory.
2. Create two processes (Parent and Child) using `fork()`.
3. Before entering the critical section, perform `sem_wait(sem)` (P operation).
4. If semaphore value is `1`, it is decremented to `0`, and process enters the critical section.
5. Execute critical section code.
6. Perform `sem_post(sem)` (V operation) to release semaphore (increment to `1`).
7. Waiting process acquires semaphore and enters critical section.
8. Destroy semaphore using `sem_destroy(sem)`.
9. Stop.

---

### C Program

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <semaphore.h>
#include <sys/mman.h>
#include <sys/wait.h>

int main()
{
    sem_t *sem;

    // Allocate shared memory for semaphore accessible by child process
    sem = mmap(NULL, sizeof(sem_t),
               PROT_READ | PROT_WRITE,
               MAP_SHARED | MAP_ANONYMOUS,
               -1, 0);

    // Initialize semaphore: pshared = 1, initial value = 1
    sem_init(sem, 1, 1);

    if(fork() == 0)
    {
        // Child Process
        sem_wait(sem); // Wait (P operation)
        printf("Child Process Entering Critical Section\n");
        sleep(2);
        printf("Child Process Leaving Critical Section\n");
        sem_post(sem); // Signal (V operation)
        exit(0);
    }

    // Parent Process
    sem_wait(sem); // Wait (P operation)
    printf("Parent Process Entering Critical Section\n");
    sleep(2);
    printf("Parent Process Leaving Critical Section\n");
    sem_post(sem); // Signal (V operation)

    wait(NULL); // Wait for child to complete
    sem_destroy(sem);

    return 0;
}
```

---

### Shell Script Equivalent (Lock File Simulation)

```bash
#!/bin/bash
LOCKFILE="/tmp/mylock"

# Lock acquiring routine
while [ -f "$LOCKFILE" ]
do
    sleep 1
done

touch "$LOCKFILE"

echo "Entering Critical Section"
sleep 3
echo "Leaving Critical Section"

rm -f "$LOCKFILE"
```

---

### Sample Output

```text
Child Process Entering Critical Section
Child Process Leaving Critical Section
Parent Process Entering Critical Section
Parent Process Leaving Critical Section
```

```text
Entering Critical Section
Leaving Critical Section
```

---

### Inference
The concept of Mutual Exclusion using Semaphore was studied and implemented successfully. The semaphore ensured that only one process accessed the critical section at a time, thereby preventing race conditions and ensuring proper synchronization between processes.

### Result
Thus, the program to implement Mutual Exclusion using Semaphore was executed successfully using C programming and Shell scripting, and the output was verified.
