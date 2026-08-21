# Experiment 13: File Organization Techniques

## Ex. No: 13

### Aim
To implement various File Organization Techniques such as Sequential File Organization, Direct (Random) File Organization, and Indexed File Organization.

---

## Algorithms

### A. SEQUENTIAL FILE ORGANIZATION
1. Create a file.
2. Enter records sequentially one by one.
3. Store records continuously in sequential order.
4. Read and display records sequentially from beginning to end.
5. Stop.

### B. DIRECT (RANDOM) FILE ORGANIZATION
1. Create a file.
2. Store records at specific byte offset positions (`fseek`, `fwrite`).
3. Use record key/number as direct target address.
4. Access and retrieve records directly using file position seeking (`fseek`, `fread`).
5. Display required record.
6. Stop.

### C. INDEXED FILE ORGANIZATION
1. Create data records.
2. Create an index containing key values and corresponding record locations.
3. Search index table for requested key.
4. Retrieve corresponding record directly using pointer index location.
5. Display record details.
6. Stop.

---

## Program A: SEQUENTIAL FILE ORGANIZATION

### C Program
```c
#include <stdio.h>

struct student
{
    int regno;
    char name[20];
};

int main()
{
    FILE *fp;
    struct student s;

    // Writing record sequentially
    fp = fopen("student.dat", "w");
    if(fp == NULL) return 1;

    printf("Enter Register Number: ");
    scanf("%d", &s.regno);
    printf("Enter Name: ");
    scanf("%s", s.name);

    fprintf(fp, "%d %s\n", s.regno, s.name);
    fclose(fp);

    // Reading record sequentially
    fp = fopen("student.dat", "r");
    fscanf(fp, "%d %s", &s.regno, s.name);

    printf("\nRecord Details\n");
    printf("Register Number : %d\n", s.regno);
    printf("Name            : %s\n", s.name);
    fclose(fp);

    return 0;
}
```

### Shell Script (Sequential)
```bash
#!/bin/bash
echo "Enter Register Number:"
read regno
echo "Enter Name:"
read name

echo "$regno $name" > student.txt

echo "Contents of File (Sequential Reading):"
cat student.txt
```

---

## Program B: DIRECT (RANDOM) FILE ORGANIZATION

### C Program
```c
#include <stdio.h>

struct student
{
    int regno;
    char name[20];
};

int main()
{
    FILE *fp;
    struct student s;

    // Open file for random read/write in binary mode
    fp = fopen("random.dat", "wb+");
    if(fp == NULL) return 1;

    printf("Enter Register Number: ");
    scanf("%d", &s.regno);
    printf("Enter Name: ");
    scanf("%s", s.name);

    // Write binary record
    fwrite(&s, sizeof(s), 1, fp);

    // Seek directly to beginning (or specific record position)
    rewind(fp);

    // Read binary record directly
    fread(&s, sizeof(s), 1, fp);

    printf("\nRecord Found (Random Access)\n");
    printf("Reg No : %d\n", s.regno);
    printf("Name   : %s\n", s.name);

    fclose(fp);
    return 0;
}
```

### Shell Script (Direct / Random Access)
```bash
#!/bin/bash
echo "Enter Record:"
read rec

echo "$rec" > random.txt

echo "Random Access Record (Line 1):"
sed -n '1p' random.txt
```

---

## Program C: INDEXED FILE ORGANIZATION

### C Program
```c
#include <stdio.h>

struct student
{
    int regno;
    char name[20];
};

int main()
{
    struct student s[3];
    int key, i, found = 0;

    printf("Enter 3 Student Records:\n");
    for(i = 0; i < 3; i++)
    {
        printf("Record %d (RegNo Name): ", i + 1);
        scanf("%d %s", &s[i].regno, s[i].name);
    }

    printf("\nEnter Register Number to Search: ");
    scanf("%d", &key);

    // Search via index key matching
    for(i = 0; i < 3; i++)
    {
        if(s[i].regno == key)
        {
            printf("\nRecord Found via Index\n");
            printf("Reg No : %d\n", s[i].regno);
            printf("Name   : %s\n", s[i].name);
            found = 1;
            break;
        }
    }

    if(!found)
    {
        printf("\nRecord Not Found\n");
    }

    return 0;
}
```

### Shell Script (Indexed Search)
```bash
#!/bin/bash
# Create index file with Key Record mapping
echo "101 Arun" > index.txt
echo "102 Kumar" >> index.txt
echo "103 Ravi" >> index.txt

echo "Enter Register Number to Search:"
read key

echo "SearchResult:"
grep "^$key" index.txt || echo "Record Not Found"
```

---

### Sample Output

```text
Enter 3 Student Records:
Record 1 (RegNo Name): 101 Arun
Record 2 (RegNo Name): 102 Kumar
Record 3 (RegNo Name): 103 Ravi

Enter Register Number to Search: 102

Record Found via Index
Reg No : 102
Name   : Kumar
```

---

### Inference
The various File Organization Techniques namely Sequential, Direct (Random), and Indexed File Organization were studied and implemented successfully. The methods of storing, retrieving, and searching records were analyzed, and the efficiency of each technique was observed and verified.

### Result
Thus, the programs to implement Sequential File Organization, Direct File Organization, and Indexed File Organization were executed successfully using C programming and Shell scripting, and the outputs were verified.
