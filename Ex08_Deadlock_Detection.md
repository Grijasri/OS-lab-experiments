# Experiment 8: Deadlock Detection Algorithm

## C Program

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

## Shell Program (`deadlock.sh`)

```bash
#!/bin/bash
echo "Enter number of processes:"
read n

echo "Enter deadlocked process numbers (if any):"
read processes

if [ -z "$processes" ]
then
    echo "No Deadlock Detected"
else
    echo "Deadlocked Processes:"
    echo "$processes"
fi
```

## Output

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
