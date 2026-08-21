# Experiment 9: Threading (POSIX Threads)

## C Program

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

    pthread_create(&t1, NULL, thread_function, &id1);
    pthread_create(&t2, NULL, thread_function, &id2);

    pthread_join(t1, NULL);
    pthread_join(t2, NULL);

    printf("All Threads Completed\n");

    return 0;
}
```

## Shell Program (`thread.sh`)

```bash
#!/bin/bash
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

task1 &
task2 &

wait

echo "All Threads Completed"
```

## Output

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
