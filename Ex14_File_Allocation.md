# Experiment 14: File Allocation Strategies

## Ex. No: 14

### Aim
To implement various File Allocation Strategies such as Sequential Allocation, Indexed Allocation, and Linked Allocation and study the allocation of files in secondary storage.

---

## Algorithms

### A. SEQUENTIAL ALLOCATION
1. Read file starting block number (`start`) and file length (`length`).
2. Allocate consecutive contiguous memory blocks from `start` to `start + length - 1`.
3. Display all allocated blocks.
4. Stop.

### B. INDEXED ALLOCATION
1. Read index block number (`indexBlock`).
2. Read the total number of blocks needed (`n`).
3. Read block numbers allocated to the file and store them in the index block.
4. Display the index block and all points/allocated block numbers.
5. Stop.

### C. LINKED ALLOCATION
1. Read total number of blocks (`n`).
2. Read block numbers where file parts are allocated.
3. Link each block to the next allocated block (`block[i] -> block[i+1]`).
4. Set last block pointer to `NULL`.
5. Display the linked list representation of allocated blocks.
6. Stop.

---

## Program A: SEQUENTIAL FILE ALLOCATION

### C Program
```c
#include <stdio.h>

int main()
{
    int start, length, i;

    printf("Enter Starting Block: ");
    scanf("%d", &start);

    printf("Enter File Length (Number of Blocks): ");
    scanf("%d", &length);

    printf("\nAllocated Blocks:\n");
    for(i = 0; i < length; i++)
    {
        printf("%d ", start + i);
    }
    printf("\n");

    return 0;
}
```

### Shell Script (Sequential Allocation)
```bash
#!/bin/bash
echo "Enter Starting Block:"
read start
echo "Enter File Length:"
read length

echo -n "Allocated Blocks: "
for ((i=0;i<length;i++))
do
    echo -n "$((start+i)) "
done
echo
```

---

## Program B: INDEXED FILE ALLOCATION

### C Program
```c
#include <stdio.h>

int main()
{
    int n, indexBlock, blocks[20], i;

    printf("Enter Index Block: ");
    scanf("%d", &indexBlock);

    printf("Enter Number of Blocks: ");
    scanf("%d", &n);

    printf("Enter Block Numbers:\n");
    for(i = 0; i < n; i++)
    {
        scanf("%d", &blocks[i]);
    }

    printf("\nIndex Block : %d\n", indexBlock);
    printf("Allocated Blocks : ");
    for(i = 0; i < n; i++)
    {
        printf("%d ", blocks[i]);
    }
    printf("\n");

    return 0;
}
```

### Shell Script (Indexed Allocation)
```bash
#!/bin/bash
echo "Enter Index Block:"
read index
echo "Enter Number of Blocks:"
read n

echo "Enter Block Numbers:"
for ((i=0;i<n;i++))
do
    read block[$i]
done

echo "Index Block : $index"
echo -n "Allocated Blocks : "
for ((i=0;i<n;i++))
do
    echo -n "${block[$i]} "
done
echo
```

---

## Program C: LINKED FILE ALLOCATION

### C Program
```c
#include <stdio.h>

int main()
{
    int n, blocks[20], i;

    printf("Enter Number of Blocks: ");
    scanf("%d", &n);

    printf("Enter Block Numbers:\n");
    for(i = 0; i < n; i++)
    {
        scanf("%d", &blocks[i]);
    }

    printf("\nLinked Allocation:\n");
    for(i = 0; i < n - 1; i++)
    {
        printf("%d --> ", blocks[i]);
    }
    printf("%d --> NULL\n", blocks[n - 1]);

    return 0;
}
```

### Shell Script (Linked Allocation)
```bash
#!/bin/bash
echo "Enter Number of Blocks:"
read n

echo "Enter Block Numbers:"
for ((i=0;i<n;i++))
do
    read block[$i]
done

echo "Linked Allocation:"
for ((i=0;i<n-1;i++))
do
    echo -n "${block[$i]} --> "
done
echo "${block[$((n-1))]} --> NULL"
```

---

### Sample Inputs & Outputs

#### Sequential File Allocation
```text
Enter Starting Block: 10
Enter File Length (Number of Blocks): 5

Allocated Blocks:
10 11 12 13 14 
```

#### Indexed File Allocation
```text
Enter Index Block: 9
Enter Number of Blocks: 4
Enter Block Numbers:
11 15 22 28

Index Block : 9
Allocated Blocks : 11 15 22 28 
```

#### Linked File Allocation
```text
Enter Number of Blocks: 4
Enter Block Numbers:
14 29 35 42

Linked Allocation:
14 --> 29 --> 35 --> 42 --> NULL
```

---

### Inference
The various File Allocation Strategies namely Sequential Allocation, Indexed Allocation, and Linked Allocation were studied and implemented successfully. The allocation and organization of file blocks in secondary storage were analyzed, and the characteristics of each allocation strategy were observed and verified.

### Result
Thus, the programs to implement Sequential Allocation, Indexed Allocation, and Linked Allocation strategies were executed successfully using C programming and Shell scripting, and the outputs were verified.
