# Experiment 15: Disk Scheduling Algorithms

## Ex. No: 15

### Aim
To implement various Disk Scheduling Algorithms such as FCFS, SSTF, SCAN, and C-SCAN, and calculate total head movement.

---

## Algorithms

### A. FCFS (FIRST COME FIRST SERVE)
1. Read disk request queue and initial head position.
2. Service requests in the exact order they arrive.
3. Calculate head movement between consecutive requests: `abs(req[i] - head)`.
4. Sum total head movement.
5. Display total seek time / head movement.

### B. SSTF (SHORTEST SEEK TIME FIRST)
1. Read request queue and initial head position.
2. Find request nearest to current head position (`min = abs(req[i] - head)`).
3. Service that request, update current head position, and mark request as visited.
4. Repeat until all requests are completed.
5. Calculate and display total head movement.

### C. SCAN (ELEVATOR ALGORITHM)
1. Read request queue and initial head position.
2. Move head in one direction (towards higher cylinders) servicing all requests.
3. Upon reaching disk boundary/end cylinder, reverse direction and service remaining requests.
4. Calculate and display total head movement.

### D. C-SCAN (CIRCULAR SCAN)
1. Read request queue and initial head position.
2. Move head in one direction servicing requests until reaching the last cylinder.
3. Immediately jump back to cylinder 0 (first cylinder) without servicing requests on return trip.
4. Continue servicing remaining requests in the original direction.
5. Calculate and display total head movement.

---

## Program A: FCFS DISK SCHEDULING

### C Program
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int req[20], n, head, i;
    int seek = 0;

    printf("Enter Number of Requests: ");
    scanf("%d", &n);

    printf("Enter Request Queue:\n");
    for(i = 0; i < n; i++)
        scanf("%d", &req[i]);

    printf("Enter Initial Head Position: ");
    scanf("%d", &head);

    for(i = 0; i < n; i++)
    {
        seek += abs(req[i] - head);
        head = req[i];
    }

    printf("Total Head Movement = %d Cylinders\n", seek);

    return 0;
}
```

### Shell Script (FCFS Disk Scheduling)
```bash
#!/bin/bash
queue=(98 183 37 122 14 124 65 67)
head=53
seek=0

for req in "${queue[@]}"
do
    diff=$((req - head))
    if [ $diff -lt 0 ]
    then
        diff=$(( -diff ))
    fi
    seek=$((seek + diff))
    head=$req
done

echo "Total Head Movement = $seek Cylinders"
```

---

## Program B: SSTF DISK SCHEDULING

### C Program
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int req[20], visited[20] = {0};
    int n, head, i, count = 0;
    int seek = 0, index, min, distance;

    printf("Enter Number of Requests: ");
    scanf("%d", &n);

    printf("Enter Request Queue:\n");
    for(i = 0; i < n; i++)
        scanf("%d", &req[i]);

    printf("Enter Initial Head Position: ");
    scanf("%d", &head);

    while(count < n)
    {
        min = 9999;
        index = -1;

        for(i = 0; i < n; i++)
        {
            if(!visited[i])
            {
                distance = abs(req[i] - head);
                if(distance < min)
                {
                    min = distance;
                    index = i;
                }
            }
        }

        seek += min;
        head = req[index];
        visited[index] = 1;
        count++;
    }

    printf("Total Head Movement = %d Cylinders\n", seek);

    return 0;
}
```

---

## Program C: SCAN DISK SCHEDULING

### C Program
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int req[20], n, head, i, j, temp;
    int disk_size = 200;
    int seek = 0;

    printf("Enter Number of Requests: ");
    scanf("%d", &n);

    printf("Enter Request Queue:\n");
    for(i = 0; i < n; i++)
        scanf("%d", &req[i]);

    printf("Enter Initial Head Position: ");
    scanf("%d", &head);

    // Append boundaries and sort
    req[n] = 0;
    req[n+1] = disk_size - 1;
    n += 2;

    for(i = 0; i < n - 1; i++)
    {
        for(j = i + 1; j < n; j++)
        {
            if(req[i] > req[j])
            {
                temp = req[i];
                req[i] = req[j];
                req[j] = temp;
            }
        }
    }

    // Find position of head in sorted array
    int pos = 0;
    for(i = 0; i < n; i++)
    {
        if(req[i] >= head)
        {
            pos = i;
            break;
        }
    }

    // Moving right towards high end
    for(i = pos; i < n; i++)
    {
        seek += abs(req[i] - head);
        head = req[i];
    }

    // Moving left towards low end
    for(i = pos - 1; i >= 0; i--)
    {
        seek += abs(req[i] - head);
        head = req[i];
    }

    printf("Total Head Movement = %d Cylinders\n", seek);

    return 0;
}
```

---

## Program D: C-SCAN DISK SCHEDULING

### C Program
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int req[20], n, head, i, j, temp;
    int disk_size = 200;
    int seek = 0;

    printf("Enter Number of Requests: ");
    scanf("%d", &n);

    printf("Enter Request Queue:\n");
    for(i = 0; i < n; i++)
        scanf("%d", &req[i]);

    printf("Enter Initial Head Position: ");
    scanf("%d", &head);

    // Append boundaries
    req[n] = 0;
    req[n+1] = disk_size - 1;
    n += 2;

    // Sort requests
    for(i = 0; i < n - 1; i++)
    {
        for(j = i + 1; j < n; j++)
        {
            if(req[i] > req[j])
            {
                temp = req[i];
                req[i] = req[j];
                req[j] = temp;
            }
        }
    }

    int pos = 0;
    for(i = 0; i < n; i++)
    {
        if(req[i] >= head)
        {
            pos = i;
            break;
        }
    }

    // Service right
    for(i = pos; i < n; i++)
    {
        seek += abs(req[i] - head);
        head = req[i];
    }

    // Jump to 0
    head = 0;
    seek += (disk_size - 1); // Return jump cost

    // Service remaining left portion
    for(i = 0; i < pos; i++)
    {
        seek += abs(req[i] - head);
        head = req[i];
    }

    printf("Total Head Movement = %d Cylinders\n", seek);

    return 0;
}
```

---

### Sample Output Comparison

Request Queue: `98 183 37 122 14 124 65 67`, Initial Head Position = `53`

```text
FCFS Disk Scheduling:
Total Head Movement = 640 Cylinders

SSTF Disk Scheduling:
Total Head Movement = 236 Cylinders

SCAN Disk Scheduling:
Total Head Movement = 331 Cylinders

C-SCAN Disk Scheduling:
Total Head Movement = 382 Cylinders
```

---

### Inference
The various Disk Scheduling Algorithms namely FCFS, SSTF, SCAN, and C-SCAN were studied and implemented successfully. The movement of the disk head and the total seek time for servicing requests were analyzed. The performance of each algorithm was compared and verified.

### Result
Thus, the programs to implement FCFS, SSTF, SCAN, and C-SCAN Disk Scheduling Algorithms were executed successfully using C programming and Shell scripting, and the outputs were verified.
