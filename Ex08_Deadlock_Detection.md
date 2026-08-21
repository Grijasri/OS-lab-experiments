# Experiment 8: Deadlock Detection Algorithm

## Ex. No: 8

### Aim
To implement the Deadlock Detection Algorithm and determine whether the system is in a deadlock state.

---

### System Concepts Used

1. **Allocation Matrix**: Represents resource instances currently allocated to each process.
2. **Request Matrix**: Represents resource instances currently requested by each process.
3. **Available Vector**: Represents available instances of each resource type.
4. **Work Vector**: Temporary workspace vector initialized to `Available`.
5. **Finish Vector**: Boolean flag vector indicating whether a process can finish execution without deadlock.

---

### Algorithm (Deadlock Detection Algorithm)

1. Read the number of processes (`n`) and resource types (`m`).
2. Read Allocation Matrix `allocation[n][m]`.
3. Read Request Matrix `request[n][m]`.
4. Read Available Resource Vector `available[m]`.
5. Initialize `work[j] = available[j]` for all $j = 0, \dots, m-1$.
6. Initialize `finish[i] = 0` for all processes having allocated resources.
7. Search for a process $P_i$ such that:
   - `finish[i] == 0`
   - `request[i][j] <= work[j]` for all $j = 0, \dots, m-1$.
8. If such a process $P_i$ is found:
   - `work[j] = work[j] + allocation[i][j]` for all $j = 0, \dots, m-1$.
   - Mark `finish[i] = 1`.
   - Repeat step 7.
9. If all processes have `finish[i] == 1`, **No Deadlock Detected**.
10. Otherwise, any process with `finish[i] == 0` is **Deadlocked**.
11. Stop.

---

### C Program

```c
#include <stdio.h>

int main()
{
    int allocation[10][10], request[10][10];
    int available[10];
    int work[10];
    int finish[10];
    int n, m;
    int i, j, k;
    int found;

    printf("Enter Number of Processes: ");
    scanf("%d", &n);

    printf("Enter Number of Resource Types: ");
    scanf("%d", &m);

    printf("\nEnter Allocation Matrix:\n");
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < m; j++)
        {
            scanf("%d", &allocation[i][j]);
        }
    }

    printf("\nEnter Request Matrix:\n");
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < m; j++)
        {
            scanf("%d", &request[i][j]);
        }
    }

    printf("\nEnter Available Resources:\n");
    for(i = 0; i < m; i++)
    {
        scanf("%d", &available[i]);
        work[i] = available[i];
    }

    for(i = 0; i < n; i++)
    {
        finish[i] = 0;
    }

    do
    {
        found = 0;
        for(i = 0; i < n; i++)
        {
            if(finish[i] == 0)
            {
                for(j = 0; j < m; j++)
                {
                    if(request[i][j] > work[j])
                        break;
                }

                if(j == m)
                {
                    for(k = 0; k < m; k++)
                    {
                        work[k] += allocation[i][k];
                    }
                    finish[i] = 1;
                    found = 1;
                }
            }
        }
    } while(found);

    found = 0;
    for(i = 0; i < n; i++)
    {
        if(finish[i] == 0)
        {
            if(found == 0)
                printf("\nDeadlocked Processes:\n");
            printf("P%d ", i);
            found = 1;
        }
    }

    if(found == 0)
    {
        printf("\nNo Deadlock Detected\n");
    }
    else
    {
        printf("\n");
    }

    return 0;
}
```

---

### Shell Program (`deadlock.sh`)

```bash
#!/bin/bash
echo "Enter number of processes:"
read n

echo "Enter deadlocked process numbers (if any, e.g. 1 2):"
read processes

if [ -z "$processes" ]
then
    echo "No Deadlock Detected"
else
    echo "Deadlocked Processes:"
    echo "$processes"
fi
```

---

### Sample Output 1 (No Deadlock)

```text
Enter Number of Processes: 3
Enter Number of Resource Types: 3

Enter Allocation Matrix:
0 1 0
2 0 0
3 0 3

Enter Request Matrix:
0 0 0
2 0 2
0 0 0

Enter Available Resources:
0 0 0

No Deadlock Detected
```

---

### Sample Output 2 (Deadlock Present)

```text
Enter Number of Processes: 3
Enter Number of Resource Types: 3

Enter Allocation Matrix:
0 1 0
2 0 0
3 0 3

Enter Request Matrix:
0 1 0
0 0 1
1 0 0

Enter Available Resources:
0 0 0

Deadlocked Processes:
P0 P1 P2 
```

---

### Inference
The Deadlock Detection Algorithm was studied and implemented successfully. The allocation, request, and available resource information were analyzed to determine whether deadlock existed in the system. The algorithm correctly identified deadlocked processes when present.

### Result
Thus, the program to implement the Deadlock Detection Algorithm was executed successfully, and deadlocked processes (if any) were identified and verified.
