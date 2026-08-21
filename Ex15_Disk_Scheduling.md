# Experiment 15: Disk Scheduling Algorithms

## 1. FCFS Disk Scheduling

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

### Shell Script (`fcfs_disk.sh`)
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

## 2. SSTF Disk Scheduling

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

## 3. SCAN Disk Scheduling

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

    int pos = 0;
    for(i = 0; i < n; i++)
    {
        if(req[i] >= head)
        {
            pos = i;
            break;
        }
    }

    for(i = pos; i < n; i++)
    {
        seek += abs(req[i] - head);
        head = req[i];
    }

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

## 4. C-SCAN Disk Scheduling

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

    int pos = 0;
    for(i = 0; i < n; i++)
    {
        if(req[i] >= head)
        {
            pos = i;
            break;
        }
    }

    for(i = pos; i < n; i++)
    {
        seek += abs(req[i] - head);
        head = req[i];
    }

    head = 0;
    seek += (disk_size - 1);

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

## Output

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
