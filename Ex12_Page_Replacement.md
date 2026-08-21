# Experiment 12: Page Replacement Algorithms

## 1. FIFO Page Replacement

### C Program
```c
#include <stdio.h>

int main()
{
    int pages[50], frames[10];
    int n, f, i, j, k = 0;
    int fault = 0, found;

    printf("Enter Number of Pages: ");
    scanf("%d", &n);

    printf("Enter Reference String:\n");
    for(i = 0; i < n; i++)
        scanf("%d", &pages[i]);

    printf("Enter Number of Frames: ");
    scanf("%d", &f);

    for(i = 0; i < f; i++)
        frames[i] = -1;

    for(i = 0; i < n; i++)
    {
        found = 0;
        for(j = 0; j < f; j++)
        {
            if(frames[j] == pages[i])
            {
                found = 1;
                break;
            }
        }

        if(found == 0)
        {
            frames[k] = pages[i];
            k = (k + 1) % f;
            fault++;
        }
    }

    printf("Total Page Faults = %d\n", fault);

    return 0;
}
```

### Shell Script (`fifo.sh`)
```bash
#!/bin/bash
echo "FIFO Page Replacement Demonstration"
pages=(7 0 1 2 0 3 0 4 2 3 0 3 2)
frames=3

echo "Reference String: ${pages[*]}"
echo "Frames: $frames"
```

---

## 2. LRU Page Replacement

### C Program
```c
#include <stdio.h>

int main()
{
    int pages[50], frames[10], time[10];
    int n, f, i, j;
    int fault = 0, count = 0;
    int found, pos, min;

    printf("Enter Number of Pages: ");
    scanf("%d", &n);

    printf("Enter Reference String:\n");
    for(i = 0; i < n; i++)
        scanf("%d", &pages[i]);

    printf("Enter Number of Frames: ");
    scanf("%d", &f);

    for(i = 0; i < f; i++)
    {
        frames[i] = -1;
        time[i] = 0;
    }

    for(i = 0; i < n; i++)
    {
        found = 0;
        for(j = 0; j < f; j++)
        {
            if(frames[j] == pages[i])
            {
                count++;
                time[j] = count;
                found = 1;
                break;
            }
        }

        if(found == 0)
        {
            pos = -1;
            for(j = 0; j < f; j++)
            {
                if(frames[j] == -1)
                {
                    pos = j;
                    break;
                }
            }

            if(pos == -1)
            {
                min = time[0];
                pos = 0;
                for(j = 1; j < f; j++)
                {
                    if(time[j] < min)
                    {
                        min = time[j];
                        pos = j;
                    }
                }
            }

            frames[pos] = pages[i];
            count++;
            time[pos] = count;
            fault++;
        }
    }

    printf("Total Page Faults = %d\n", fault);

    return 0;
}
```

---

## 3. Optimal Page Replacement

### C Program
```c
#include <stdio.h>

int main()
{
    int pages[50], frames[10];
    int n, f;
    int i, j, k, pos;
    int fault = 0;
    int found;

    printf("Enter Number of Pages: ");
    scanf("%d", &n);

    printf("Enter Reference String:\n");
    for(i = 0; i < n; i++)
        scanf("%d", &pages[i]);

    printf("Enter Number of Frames: ");
    scanf("%d", &f);

    for(i = 0; i < f; i++)
        frames[i] = -1;

    for(i = 0; i < n; i++)
    {
        found = 0;
        for(j = 0; j < f; j++)
        {
            if(frames[j] == pages[i])
            {
                found = 1;
                break;
            }
        }

        if(found == 0)
        {
            pos = -1;
            for(j = 0; j < f; j++)
            {
                if(frames[j] == -1)
                {
                    pos = j;
                    break;
                }
            }

            if(pos == -1)
            {
                int farthest = -1;
                for(j = 0; j < f; j++)
                {
                    int future = 999;
                    for(k = i + 1; k < n; k++)
                    {
                        if(frames[j] == pages[k])
                        {
                            future = k;
                            break;
                        }
                    }

                    if(future > farthest)
                    {
                        farthest = future;
                        pos = j;
                    }
                }
            }

            frames[pos] = pages[i];
            fault++;
        }
    }

    printf("Total Page Faults = %d\n", fault);

    return 0;
}
```

---

## Output

Reference String: `7 0 1 2 0 3 0 4 2 3 0 3 2`, Number of Frames = `3`

```text
FIFO Page Replacement:
Total Page Faults = 10

LRU Page Replacement:
Total Page Faults = 9

Optimal Page Replacement:
Total Page Faults = 7
```
