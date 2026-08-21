# Experiment 9: Threading (POSIX Threads)

## Ex. No: 9

### Aim
To create and execute multiple threads using POSIX Threads (Pthreads) and demonstrate concurrent execution.

---

### Functions Used

1. **`pthread_create(&thread_id, attr, start_routine, arg)`**: Creates a new concurrent thread executing `start_routine`.
2. **`pthread_join(thread_id, retval)`**: Waits for a specific thread to terminate.
3. **`pthread_exit(retval)`**: Terminates the calling thread.
4. **`sleep(seconds)`**: Suspends execution of the current thread for specified duration.

---

### Algorithm

#### Thread Creation and Execution
1. Include required header files (`<pthread.h>`, `<stdio.h>`, `<stdlib.h>`, `<unistd.h>`).
2. Define a thread routine function `thread_function(void *arg)` to be executed by each thread.
3. In `main()`, declare thread identifiers `pthread_t t1, t2;`.
4. Create threads using `pthread_create(&t1, NULL, thread_function, NULL)` and `pthread_create(&t2, NULL, thread_function, NULL)`.
5. Execute thread routines concurrently.
6. Main thread waits for thread completions using `pthread_join(t1, NULL)` and `pthread_join(t2, NULL)`.
7. Display completion message and terminate program.
8. Stop.

---

### C Program

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>

void *thread_function(void *arg)
{
    int i;
    int thread_num = *(int*)arg;

    for(i = 1; i <= 5; i++)
    {
        printf("Thread %d Executing : Step %d\n", thread_num, i);
        sleep(1);
    }

    pthread_exit(NULL);
}

int main()
{
    pthread_t t1, t2;
    int id1 = 1, id2 = 2;

    // Create threads
    pthread_create(&t1, NULL, thread_function, &id1);
    pthread_create(&t2, NULL, thread_function, &id2);

    // Join threads (wait for completion)
    pthread_join(t1, NULL);
    pthread_join(t2, NULL);

    printf("All Threads Completed\n");

    return 0;
}
```

---

### Shell Program (`thread.sh`)

```bash
#!/bin/bash
# Shell scripting simulates concurrent execution using background processes (&)

task1()
{
    for i in 1 2 3 4 5
    do
        echo "Thread 1 : Step $i"
        sleep 1
    done
}

task2()
{
    for i in 1 2 3 4 5
    do
        echo "Thread 2 : Step $i"
        sleep 1
    done
}

# Run tasks concurrently in background
task1 &
task2 &

# Wait for both background tasks to finish
wait

echo "All Threads Completed"
```

---

### Compilation & Execution

#### Compiling C Program with Pthreads library:
```bash
gcc thread.c -o thread -pthread
./thread
```

#### Executing Shell Script:
```bash
chmod +x thread.sh
./thread.sh
```

---

### Sample Output

```text
Thread 1 Executing : Step 1
Thread 2 Executing : Step 1
Thread 1 Executing : Step 2
Thread 2 Executing : Step 2
Thread 1 Executing : Step 3
Thread 2 Executing : Step 3
Thread 1 Executing : Step 4
Thread 2 Executing : Step 4
Thread 1 Executing : Step 5
Thread 2 Executing : Step 5
All Threads Completed
```

---

### Inference
The concept of multithreading was studied and implemented successfully using POSIX Threads. Multiple threads were created and executed concurrently, and synchronization was achieved using `pthread_join()`. The behavior of concurrent execution was observed and verified.

### Result
Thus, the program to implement Threading using POSIX Threads (Pthreads) was executed successfully, and the output was verified.
