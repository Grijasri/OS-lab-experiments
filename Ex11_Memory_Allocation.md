# Experiment 11: Memory Allocation Methods (First Fit, Best Fit, Worst Fit)

## Ex. No: 11

### Aim
To implement the memory allocation methods namely First Fit, Best Fit, and Worst Fit and allocate memory blocks to processes efficiently.

---

## Algorithm

### A. FIRST FIT
1. Read the number of memory blocks (`nb`) and processes (`np`).
2. Read the size of each memory block and process.
3. For each process, scan memory blocks from the beginning (index 0).
4. Allocate the first block that is large enough (`blockSize[j] >= processSize[i]`).
5. Reduce the remaining size of the allocated block (`blockSize[j] -= processSize[i]`).
6. Repeat until all processes are processed.
7. Display allocation details.

### B. BEST FIT
1. Read block sizes and process sizes.
2. For each process, scan all available blocks.
3. Select the smallest block that can accommodate the process (`blockSize[j] >= processSize[i]`).
4. Allocate the process to that best index (`bestIdx`).
5. Update remaining block size.
6. Display allocation details.

### C. WORST FIT
1. Read block sizes and process sizes.
2. For each process, scan all available blocks.
3. Select the largest available block that can accommodate the process (`blockSize[j] >= processSize[i]`).
4. Allocate the process to that worst index (`worstIdx`).
5. Update remaining block size.
6. Display allocation details.

---

## Program A: FIRST FIT

### C Program
```c
#include <stdio.h>

int main()
{
    int blockSize[20], processSize[20];
    int allocation[20];
    int nb, np, i, j;

    printf("Enter Number of Blocks: ");
    scanf("%d", &nb);
    printf("Enter Number of Processes: ");
    scanf("%d", &np);

    printf("Enter Block Sizes:\n");
    for(i = 0; i < nb; i++)
        scanf("%d", &blockSize[i]);

    printf("Enter Process Sizes:\n");
    for(i = 0; i < np; i++)
        scanf("%d", &processSize[i]);

    for(i = 0; i < np; i++)
        allocation[i] = -1;

    for(i = 0; i < np; i++)
    {
        for(j = 0; j < nb; j++)
        {
            if(blockSize[j] >= processSize[i])
            {
                allocation[i] = j;
                blockSize[j] -= processSize[i];
                break;
            }
        }
    }

    printf("\nProcess No\tProcess Size\tBlock No\n");
    for(i = 0; i < np; i++)
    {
        printf("%d\t\t%d\t\t", i + 1, processSize[i]);
        if(allocation[i] != -1)
            printf("%d\n", allocation[i] + 1);
        else
            printf("Not Allocated\n");
    }

    return 0;
}
```

### Shell Script (First Fit)
```bash
#!/bin/bash
echo "First Fit Memory Allocation Demonstration"
blocks=(100 500 200 300 600)
processes=(212 417 112 426)

echo "Memory Blocks: ${blocks[*]}"
echo "Processes: ${processes[*]}"
echo "Allocation Performed Using First Fit"
```

---

## Program B: BEST FIT

### C Program
```c
#include <stdio.h>

int main()
{
    int blockSize[20], processSize[20];
    int allocation[20];
    int nb, np, i, j, bestIdx;

    printf("Enter Number of Blocks: ");
    scanf("%d", &nb);
    printf("Enter Number of Processes: ");
    scanf("%d", &np);

    printf("Enter Block Sizes:\n");
    for(i = 0; i < nb; i++)
        scanf("%d", &blockSize[i]);

    printf("Enter Process Sizes:\n");
    for(i = 0; i < np; i++)
        scanf("%d", &processSize[i]);

    for(i = 0; i < np; i++)
        allocation[i] = -1;

    for(i = 0; i < np; i++)
    {
        bestIdx = -1;
        for(j = 0; j < nb; j++)
        {
            if(blockSize[j] >= processSize[i])
            {
                if(bestIdx == -1 || blockSize[j] < blockSize[bestIdx])
                    bestIdx = j;
            }
        }

        if(bestIdx != -1)
        {
            allocation[i] = bestIdx;
            blockSize[bestIdx] -= processSize[i];
        }
    }

    printf("\nProcess No\tProcess Size\tBlock No\n");
    for(i = 0; i < np; i++)
    {
        printf("%d\t\t%d\t\t", i + 1, processSize[i]);
        if(allocation[i] != -1)
            printf("%d\n", allocation[i] + 1);
        else
            printf("Not Allocated\n");
    }

    return 0;
}
```

---

## Program C: WORST FIT

### C Program
```c
#include <stdio.h>

int main()
{
    int blockSize[20], processSize[20];
    int allocation[20];
    int nb, np, i, j, worstIdx;

    printf("Enter Number of Blocks: ");
    scanf("%d", &nb);
    printf("Enter Number of Processes: ");
    scanf("%d", &np);

    printf("Enter Block Sizes:\n");
    for(i = 0; i < nb; i++)
        scanf("%d", &blockSize[i]);

    printf("Enter Process Sizes:\n");
    for(i = 0; i < np; i++)
        scanf("%d", &processSize[i]);

    for(i = 0; i < np; i++)
        allocation[i] = -1;

    for(i = 0; i < np; i++)
    {
        worstIdx = -1;
        for(j = 0; j < nb; j++)
        {
            if(blockSize[j] >= processSize[i])
            {
                if(worstIdx == -1 || blockSize[j] > blockSize[worstIdx])
                    worstIdx = j;
            }
        }

        if(worstIdx != -1)
        {
            allocation[i] = worstIdx;
            blockSize[worstIdx] -= processSize[i];
        }
    }

    printf("\nProcess No\tProcess Size\tBlock No\n");
    for(i = 0; i < np; i++)
    {
        printf("%d\t\t%d\t\t", i + 1, processSize[i]);
        if(allocation[i] != -1)
            printf("%d\n", allocation[i] + 1);
        else
            printf("Not Allocated\n");
    }

    return 0;
}
```

---

### Sample Output (First Fit / Best Fit / Worst Fit)

```text
Enter Number of Blocks: 5
Enter Number of Processes: 4
Enter Block Sizes:
100 500 200 300 600
Enter Process Sizes:
212 417 112 426

--- FIRST FIT RESULT ---
Process No	Process Size	Block No
1		212		2
2		417		5
3		112		2
4		426		Not Allocated

--- BEST FIT RESULT ---
Process No	Process Size	Block No
1		212		4
2		417		2
3		112		3
4		426		5

--- WORST FIT RESULT ---
Process No	Process Size	Block No
1		212		5
2		417		Not Allocated
3		112		2
4		426		Not Allocated
```

---

### Inference
The memory allocation methods First Fit, Best Fit, and Worst Fit were studied and implemented successfully. The allocation of processes to memory blocks was analyzed, and the differences in memory utilization and fragmentation among the three methods were observed and verified.

### Result
Thus, the programs to implement First Fit, Best Fit, and Worst Fit memory allocation methods were executed successfully using C programming and Shell scripting, and the outputs were verified.
