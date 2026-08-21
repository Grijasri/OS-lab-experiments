# Experiment 4: CPU Scheduling Algorithms

## Ex. No: 4

### Aim
To write and execute C and Shell programs for implementing various CPU Scheduling Algorithms:
1. First Come First Serve (FCFS)
2. Shortest Job First (SJF - Non-Preemptive)
3. Priority Scheduling
4. Round Robin Scheduling

and to calculate Waiting Time (WT), Turnaround Time (TAT), Average Waiting Time, and Average Turnaround Time.

---

## 1. First Come First Serve (FCFS)

### Algorithm
1. Read the number of processes (`n`).
2. Read burst time (`bt`) for each process.
3. Set waiting time of first process as `wt[0] = 0`.
4. Calculate waiting time for remaining processes: `wt[i] = wt[i-1] + bt[i-1]`.
5. Calculate turnaround time for each process: `tat[i] = wt[i] + bt[i]`.
6. Calculate average waiting time and average turnaround time.
7. Display results.

### C Program
```c
#include<stdio.h>

int main()
{
    int n, i;
    int bt[20], wt[20], tat[20];
    float avg_wt = 0, avg_tat = 0;

    printf("Enter Number of Processes: ");
    scanf("%d", &n);

    for(i = 0; i < n; i++)
    {
        printf("Enter Burst Time for P%d: ", i + 1);
        scanf("%d", &bt[i]);
    }

    wt[0] = 0;

    for(i = 1; i < n; i++)
        wt[i] = wt[i-1] + bt[i-1];

    for(i = 0; i < n; i++)
    {
        tat[i] = wt[i] + bt[i];
        avg_wt += wt[i];
        avg_tat += tat[i];
    }

    printf("\nProcess\tBT\tWT\tTAT\n");
    for(i = 0; i < n; i++)
        printf("P%d\t%d\t%d\t%d\n", i + 1, bt[i], wt[i], tat[i]);

    printf("\nAverage Waiting Time = %.2f", avg_wt / n);
    printf("\nAverage Turnaround Time = %.2f\n", avg_tat / n);

    return 0;
}
```

### Shell Program (`fcfs.sh`)
```bash
#!/bin/bash
echo "Enter Number of Processes"
read n

for ((i=0;i<n;i++))
do
    echo "Enter Burst Time for P$((i+1))"
    read bt[$i]
done

wt[0]=0

for ((i=1;i<n;i++))
do
    wt[$i]=$((wt[i-1]+bt[i-1]))
done

echo
echo -e "Process\tBT\tWT\tTAT"

total_wt=0
total_tat=0

for ((i=0;i<n;i++))
do
    tat[$i]=$((wt[i]+bt[i]))
    total_wt=$((total_wt+wt[i]))
    total_tat=$((total_tat+tat[i]))
    echo -e "P$((i+1))\t${bt[i]}\t${wt[i]}\t${tat[i]}"
done

avg_wt=$(awk "BEGIN {printf \"%.2f\", $total_wt/$n}")
avg_tat=$(awk "BEGIN {printf \"%.2f\", $total_tat/$n}")

echo
echo "Average Waiting Time = $avg_wt"
echo "Average Turnaround Time = $avg_tat"
```

### Sample Output (FCFS)
```text
Enter Number of Processes: 3
Enter Burst Time for P1: 24
Enter Burst Time for P2: 3
Enter Burst Time for P3: 3

Process	BT	WT	TAT
P1	24	0	24
P2	3	24	27
P3	3	27	30

Average Waiting Time = 17.00
Average Turnaround Time = 27.00
```

---

## 2. Shortest Job First (SJF - Non-Preemptive)

### Algorithm
1. Read the number of processes and burst times.
2. Sort processes in ascending order according to burst time.
3. Calculate waiting time: `wt[0] = 0`, `wt[i] = wt[i-1] + bt[i-1]`.
4. Calculate turnaround time: `tat[i] = wt[i] + bt[i]`.
5. Calculate averages and display results.

### C Program
```c
#include<stdio.h>

int main()
{
    int n, i, j, temp;
    int bt[20], wt[20], tat[20], p[20];
    float avg_wt = 0, avg_tat = 0;

    printf("Enter Number of Processes: ");
    scanf("%d", &n);

    for(i = 0; i < n; i++)
    {
        printf("Enter Burst Time for P%d: ", i + 1);
        scanf("%d", &bt[i]);
        p[i] = i + 1;
    }

    // Sorting burst times in ascending order
    for(i = 0; i < n - 1; i++)
    {
        for(j = i + 1; j < n; j++)
        {
            if(bt[i] > bt[j])
            {
                temp = bt[i];
                bt[i] = bt[j];
                bt[j] = temp;

                temp = p[i];
                p[i] = p[j];
                p[j] = temp;
            }
        }
    }

    wt[0] = 0;
    for(i = 1; i < n; i++)
        wt[i] = wt[i-1] + bt[i-1];

    printf("\nProcess\tBT\tWT\tTAT\n");
    for(i = 0; i < n; i++)
    {
        tat[i] = wt[i] + bt[i];
        avg_wt += wt[i];
        avg_tat += tat[i];
        printf("P%d\t%d\t%d\t%d\n", p[i], bt[i], wt[i], tat[i]);
    }

    printf("\nAverage Waiting Time = %.2f", avg_wt / n);
    printf("\nAverage Turnaround Time = %.2f\n", avg_tat / n);

    return 0;
}
```

### Shell Program (`sjf.sh`)
```bash
#!/bin/bash
echo "Enter Number of Processes"
read n

for ((i=0;i<n;i++))
do
    echo "Enter Burst Time for P$((i+1))"
    read bt[$i]
    p[$i]=$((i+1))
done

# Sorting burst times (Ascending Order)
for ((i=0;i<n-1;i++))
do
    for ((j=i+1;j<n;j++))
    do
        if [ ${bt[i]} -gt ${bt[j]} ]
        then
            temp=${bt[i]}
            bt[$i]=${bt[j]}
            bt[$j]=$temp

            temp=${p[i]}
            p[$i]=${p[j]}
            p[$j]=$temp
        fi
    done
done

wt[0]=0
for ((i=1;i<n;i++))
do
    wt[$i]=$((wt[i-1]+bt[i-1]))
done

echo
echo -e "Process\tBT\tWT\tTAT"
total_wt=0
total_tat=0

for ((i=0;i<n;i++))
do
    tat[$i]=$((wt[i]+bt[i]))
    total_wt=$((total_wt+wt[i]))
    total_tat=$((total_tat+tat[i]))
    echo -e "P${p[i]}\t${bt[i]}\t${wt[i]}\t${tat[i]}"
done

avg_wt=$(awk "BEGIN {printf \"%.2f\", $total_wt/$n}")
avg_tat=$(awk "BEGIN {printf \"%.2f\", $total_tat/$n}")

echo
echo "Average Waiting Time = $avg_wt"
echo "Average Turnaround Time = $avg_tat"
```

### Sample Output (SJF)
```text
Enter Number of Processes: 4
Enter Burst Time for P1: 6
Enter Burst Time for P2: 8
Enter Burst Time for P3: 7
Enter Burst Time for P4: 3

Process	BT	WT	TAT
P4	3	0	3
P1	6	3	9
P3	7	9	16
P2	8	16	24

Average Waiting Time = 7.00
Average Turnaround Time = 13.00
```

---

## 3. Priority Scheduling

### Algorithm
1. Read process burst times and priorities (Lower number = Higher Priority).
2. Sort processes according to priority.
3. Calculate waiting time and turnaround time.
4. Display results.

### C Program
```c
#include<stdio.h>

int main()
{
    int n, i, j, temp;
    int bt[20], pr[20], wt[20], tat[20], p[20];
    float avg_wt = 0, avg_tat = 0;

    printf("Enter Number of Processes: ");
    scanf("%d", &n);

    for(i = 0; i < n; i++)
    {
        printf("\nEnter Burst Time for P%d: ", i + 1);
        scanf("%d", &bt[i]);
        printf("Enter Priority for P%d: ", i + 1);
        scanf("%d", &pr[i]);
        p[i] = i + 1;
    }

    // Sort according to priority
    for(i = 0; i < n - 1; i++)
    {
        for(j = i + 1; j < n; j++)
        {
            if(pr[i] > pr[j])
            {
                temp = pr[i]; pr[i] = pr[j]; pr[j] = temp;
                temp = bt[i]; bt[i] = bt[j]; bt[j] = temp;
                temp = p[i];  p[i] = p[j];   p[j] = temp;
            }
        }
    }

    wt[0] = 0;
    for(i = 1; i < n; i++)
        wt[i] = wt[i-1] + bt[i-1];

    printf("\nProcess\tPriority\tBT\tWT\tTAT\n");
    for(i = 0; i < n; i++)
    {
        tat[i] = wt[i] + bt[i];
        avg_wt += wt[i];
        avg_tat += tat[i];
        printf("P%d\t%d\t\t%d\t%d\t%d\n", p[i], pr[i], bt[i], wt[i], tat[i]);
    }

    printf("\nAverage Waiting Time = %.2f", avg_wt / n);
    printf("\nAverage Turnaround Time = %.2f\n", avg_tat / n);

    return 0;
}
```

### Shell Program (`priority.sh`)
```bash
#!/bin/bash
echo "Enter Number of Processes"
read n

for ((i=0;i<n;i++))
do
    echo "Enter Burst Time for P$((i+1))"
    read bt[$i]
    echo "Enter Priority for P$((i+1))"
    read pr[$i]
    p[$i]=$((i+1))
done

# Sort according to Priority
for ((i=0;i<n-1;i++))
do
    for ((j=i+1;j<n;j++))
    do
        if [ ${pr[i]} -gt ${pr[j]} ]
        then
            temp=${pr[i]}; pr[$i]=${pr[j]}; pr[$j]=$temp
            temp=${bt[i]}; bt[$i]=${bt[j]}; bt[$j]=$temp
            temp=${p[i]};  p[$i]=${p[j]};   p[$j]=$temp
        fi
    done
done

wt[0]=0
for ((i=1;i<n;i++))
do
    wt[$i]=$((wt[i-1]+bt[i-1]))
done

echo
echo -e "Process\tPriority\tBT\tWT\tTAT"
total_wt=0
total_tat=0

for ((i=0;i<n;i++))
do
    tat[$i]=$((wt[i]+bt[i]))
    total_wt=$((total_wt+wt[i]))
    total_tat=$((total_tat+tat[i]))
    echo -e "P${p[i]}\t${pr[i]}\t\t${bt[i]}\t${wt[i]}\t${tat[i]}"
done

avg_wt=$(awk "BEGIN {printf \"%.2f\", $total_wt/$n}")
avg_tat=$(awk "BEGIN {printf \"%.2f\", $total_tat/$n}")

echo
echo "Average Waiting Time = $avg_wt"
echo "Average Turnaround Time = $avg_tat"
```

### Sample Output (Priority)
```text
Enter Number of Processes: 3
Enter Burst Time for P1: 10
Enter Priority for P1: 3
Enter Burst Time for P2: 1
Enter Priority for P2: 1
Enter Burst Time for P3: 2
Enter Priority for P3: 2

Process	Priority	BT	WT	TAT
P2	1		1	0	1
P3	2		2	1	3
P1	3		10	3	13

Average Waiting Time = 1.33
Average Turnaround Time = 5.67
```

---

## 4. Round Robin Scheduling

### Algorithm
1. Read number of processes and burst times.
2. Read time quantum (`tq`).
3. Execute each process for the given quantum.
4. If burst time remains (`rem_bt > 0`), place process back in queue.
5. Continue until all processes finish.
6. Calculate waiting time (`wt = completion_time - bt`) and turnaround time (`tat = completion_time`).

### C Program
```c
#include<stdio.h>

int main()
{
    int n, tq, i;
    int bt[20], rem_bt[20], wt[20] = {0}, tat[20];
    int time = 0, done;
    float avg_wt = 0, avg_tat = 0;

    printf("Enter Number of Processes: ");
    scanf("%d", &n);

    for(i = 0; i < n; i++)
    {
        printf("Enter Burst Time for P%d: ", i + 1);
        scanf("%d", &bt[i]);
        rem_bt[i] = bt[i];
    }

    printf("Enter Time Quantum: ");
    scanf("%d", &tq);

    do
    {
        done = 1;
        for(i = 0; i < n; i++)
        {
            if(rem_bt[i] > 0)
            {
                done = 0;
                if(rem_bt[i] > tq)
                {
                    time += tq;
                    rem_bt[i] -= tq;
                }
                else
                {
                    time += rem_bt[i];
                    wt[i] = time - bt[i];
                    rem_bt[i] = 0;
                }
            }
        }
    } while(!done);

    printf("\nProcess\tBT\tWT\tTAT\n");
    for(i = 0; i < n; i++)
    {
        tat[i] = bt[i] + wt[i];
        avg_wt += wt[i];
        avg_tat += tat[i];
        printf("P%d\t%d\t%d\t%d\n", i + 1, bt[i], wt[i], tat[i]);
    }

    printf("\nAverage Waiting Time = %.2f", avg_wt / n);
    printf("\nAverage Turnaround Time = %.2f\n", avg_tat / n);

    return 0;
}
```

### Shell Program (`rr.sh`)
```bash
#!/bin/bash
echo "Enter Number of Processes"
read n

for ((i=0;i<n;i++))
do
    echo "Enter Burst Time for P$((i+1))"
    read bt[$i]
    rem_bt[$i]=${bt[$i]}
done

echo "Enter Time Quantum"
read tq

time=0

while true
do
    done=1
    for ((i=0;i<n;i++))
    do
        if [ ${rem_bt[i]} -gt 0 ]
        then
            done=0
            if [ ${rem_bt[i]} -gt $tq ]
            then
                time=$((time+tq))
                rem_bt[$i]=$((rem_bt[i]-tq))
            else
                time=$((time+rem_bt[i]))
                wt[$i]=$((time-bt[i]))
                rem_bt[$i]=0
            fi
        fi
    done
    [ $done -eq 1 ] && break
done

echo
echo -e "Process\tBT\tWT\tTAT"
total_wt=0
total_tat=0

for ((i=0;i<n;i++))
do
    tat[$i]=$((bt[i]+wt[i]))
    total_wt=$((total_wt+wt[i]))
    total_tat=$((total_tat+tat[i]))
    echo -e "P$((i+1))\t${bt[i]}\t${wt[i]}\t${tat[i]}"
done

avg_wt=$(awk "BEGIN {printf \"%.2f\", $total_wt/$n}")
avg_tat=$(awk "BEGIN {printf \"%.2f\", $total_tat/$n}")

echo
echo "Average Waiting Time = $avg_wt"
echo "Average Turnaround Time = $avg_tat"
```

### Sample Output (Round Robin)
```text
Enter Number of Processes: 3
Enter Burst Time for P1: 24
Enter Burst Time for P2: 3
Enter Burst Time for P3: 3
Enter Time Quantum: 4

Process	BT	WT	TAT
P1	24	6	30
P2	3	4	7
P3	3	7	10

Average Waiting Time = 5.67
Average Turnaround Time = 15.67
```

---

### Inference
The C and Shell programs for implementing CPU Scheduling Algorithms (FCFS, SJF, Priority Scheduling, and Round Robin Scheduling) were successfully developed, executed, and the Waiting Time and Turnaround Time were obtained.

### Result
Thus, CPU scheduling algorithms FCFS, SJF, Priority, and Round Robin were implemented and verified.
