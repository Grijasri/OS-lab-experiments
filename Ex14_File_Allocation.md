# Experiment 14: File Allocation Strategies

## 1. Sequential File Allocation

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

### Shell Script
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

## 2. Indexed File Allocation

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

### Shell Script
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

## 3. Linked File Allocation

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

### Shell Script
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

## Output

```text
--- Sequential File Allocation ---
Enter Starting Block: 10
Enter File Length (Number of Blocks): 5

Allocated Blocks:
10 11 12 13 14 

--- Indexed File Allocation ---
Enter Index Block: 9
Enter Number of Blocks: 4
Enter Block Numbers:
11 15 22 28

Index Block : 9
Allocated Blocks : 11 15 22 28 

--- Linked File Allocation ---
Enter Number of Blocks: 4
Enter Block Numbers:
14 29 35 42

Linked Allocation:
14 --> 29 --> 35 --> 42 --> NULL
```
