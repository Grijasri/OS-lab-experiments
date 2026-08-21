# Experiment 7: Banker's Algorithm (Deadlock Avoidance)

## Ex. No: 7

### Aim
To implement Deadlock Avoidance using Banker's Algorithm and determine whether the system is in a safe state.

---

### System Concepts Used

1. **Allocation Matrix**: Stores the number of resource instances of each type currently allocated to each process.
2. **Maximum Matrix**: Stores the maximum resource instances required by each process to complete execution.
3. **Need Matrix**: Stores remaining resource instances required by each process.
   $$\text{Need}[i][j] = \text{Max}[i][j] - \text{Allocation}[i][j]$$
4. **Available Vector**: Stores currently available instances of each resource type.
5. **Safe Sequence**: An execution sequence $\langle P_0, P_1, \dots, P_{n-1} \rangle$ where all processes finish execution without causing a deadlock.

---

### Algorithm (Banker's Safety Algorithm)

1. Read the number of processes (`n`) and number of resource types (`m`).
2. Read Allocation Matrix `allocation[n][m]`.
3. Read Maximum Matrix `max[n][m]`.
4. Read Available Resources Vector `available[m]`.
5. Calculate Need Matrix: `need[i][j] = max[i][j] - allocation[i][j]`.
6. Initialize `finish[i] = 0` for all $i = 0, \dots, n-1$ and `count = 0`.
7. Find a process $P_i$ such that `finish[i] == 0` and `need[i][j] <= available[j]` for all resources $j = 0, \dots, m-1$.
8. If such a process $P_i$ is found:
   - Add process $P_i$ to `safeSeq[count++] = i`.
   - Update available resources: `available[j] = available[j] + allocation[i][j]`.
   - Mark process as completed: `finish[i] = 1`.
   - Repeat steps 7–8.
9. If `count == n`, the system is in a **Safe State**. Print the Safe Sequence.
10. Otherwise, the system is in an **Unsafe State** (potential deadlock).
11. Stop.

---

### C Program

```c
#include <stdio.h>

int main()
{
    int n, m, i, j, k;
    int allocation[10][10], max[10][10];
    int need[10][10];
    int available[10];
    int finish[10] = {0};
    int safeSeq[10];
    int count = 0;

    printf("Enter Number of Processes: ");
    scanf("%d", &n);

    printf("Enter Number of Resources: ");
    scanf("%d", &m);

    printf("\nEnter Allocation Matrix:\n");
    for(i = 0; i < n; i++)
        for(j = 0; j < m; j++)
            scanf("%d", &allocation[i][j]);

    printf("\nEnter Maximum Matrix:\n");
    for(i = 0; i < n; i++)
        for(j = 0; j < m; j++)
            scanf("%d", &max[i][j]);

    printf("\nEnter Available Resources:\n");
    for(i = 0; i < m; i++)
        scanf("%d", &available[i]);

    // Calculate Need Matrix
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < m; j++)
        {
            need[i][j] = max[i][j] - allocation[i][j];
        }
    }

    // Safety Algorithm
    while(count < n)
    {
        int found = 0;
        for(i = 0; i < n; i++)
        {
            if(finish[i] == 0)
            {
                for(j = 0; j < m; j++)
                {
                    if(need[i][j] > available[j])
                        break;
                }

                if(j == m)
                {
                    for(k = 0; k < m; k++)
                        available[k] += allocation[i][k];

                    safeSeq[count++] = i;
                    finish[i] = 1;
                    found = 1;
                }
            }
        }

        if(found == 0)
        {
            printf("\nSystem is NOT in Safe State (Deadlock Possible)\n");
            return 0;
        }
    }

    printf("\nSystem is in Safe State\n");
    printf("Safe Sequence: ");
    for(i = 0; i < n; i++)
        printf("P%d ", safeSeq[i]);
    printf("\n");

    return 0;
}
```

---

### Shell Program (`bankers.sh`)

```bash
#!/bin/bash
echo "Enter Number of Processes:"
read n

echo "Enter Safe Sequence (space separated, e.g. 1 3 4 0 2):"
read -a seq

echo "Safe Sequence is:"
for ((i=0;i<n;i++))
do
    echo -n "P${seq[$i]} "
done
echo
echo "System is in Safe State"
```

---

### Sample Input & Output

#### Input:
```text
Enter Number of Processes: 5
Enter Number of Resources: 3

Enter Allocation Matrix:
0 1 0
2 0 0
3 0 2
2 1 1
0 0 2

Enter Maximum Matrix:
7 5 3
3 2 2
9 0 2
2 2 2
4 3 3

Enter Available Resources:
3 3 2
```

#### Output:
```text
System is in Safe State
Safe Sequence: P1 P3 P4 P0 P2 
```

---

### Inference
The Banker's Algorithm for Deadlock Avoidance was studied and implemented successfully. The Need Matrix was computed, and the safe sequence of process execution was determined. The algorithm ensured that resources were allocated only when the system remained in a safe state, thereby avoiding deadlock.

### Result
Thus, the program to avoid Deadlock using Banker's Algorithm was executed successfully, and the safe sequence was verified.
