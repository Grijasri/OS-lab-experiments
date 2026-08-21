# Experiment 13: File Organization Techniques

## 1. Sequential File Organization

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

    fp = fopen("student.dat", "w");
    if(fp == NULL) return 1;

    printf("Enter Register Number: ");
    scanf("%d", &s.regno);
    printf("Enter Name: ");
    scanf("%s", s.name);

    fprintf(fp, "%d %s\n", s.regno, s.name);
    fclose(fp);

    fp = fopen("student.dat", "r");
    fscanf(fp, "%d %s", &s.regno, s.name);

    printf("\nRecord Details\n");
    printf("Register Number : %d\n", s.regno);
    printf("Name            : %s\n", s.name);
    fclose(fp);

    return 0;
}
```

### Shell Script
```bash
#!/bin/bash
echo "Enter Register Number:"
read regno
echo "Enter Name:"
read name

echo "$regno $name" > student.txt

echo "Contents of File:"
cat student.txt
```

---

## 2. Direct (Random) File Organization

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

    fp = fopen("random.dat", "wb+");
    if(fp == NULL) return 1;

    printf("Enter Register Number: ");
    scanf("%d", &s.regno);
    printf("Enter Name: ");
    scanf("%s", s.name);

    fwrite(&s, sizeof(s), 1, fp);
    rewind(fp);
    fread(&s, sizeof(s), 1, fp);

    printf("\nRecord Found\n");
    printf("Reg No : %d\n", s.regno);
    printf("Name   : %s\n", s.name);

    fclose(fp);
    return 0;
}
```

### Shell Script
```bash
#!/bin/bash
echo "Enter Record:"
read rec

echo "$rec" > random.txt

echo "Random Access Record:"
sed -n '1p' random.txt
```

---

## 3. Indexed File Organization

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

### Shell Script
```bash
#!/bin/bash
echo "101 Arun" > index.txt
echo "102 Kumar" >> index.txt
echo "103 Ravi" >> index.txt

echo "Enter Register Number to Search:"
read key

grep "^$key" index.txt || echo "Record Not Found"
```

---

## Output

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
