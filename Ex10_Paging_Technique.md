# Experiment 10: Paging Technique

## C Program

```c
#include <stdio.h>

int main()
{
    int pageTable[20];
    int pageSize;
    int numPages;
    int logicalAddress;
    int pageNumber;
    int offset;
    int frameNumber;
    int physicalAddress;
    int i;

    printf("Enter Page Size: ");
    scanf("%d", &pageSize);

    printf("Enter Number of Pages: ");
    scanf("%d", &numPages);

    printf("Enter Frame Numbers for Each Page:\n");
    for(i = 0; i < numPages; i++)
    {
        printf("Page %d -> Frame: ", i);
        scanf("%d", &pageTable[i]);
    }

    printf("Enter Logical Address: ");
    scanf("%d", &logicalAddress);

    pageNumber = logicalAddress / pageSize;
    offset = logicalAddress % pageSize;

    if(pageNumber >= numPages)
    {
        printf("Invalid Logical Address\n");
        return 0;
    }

    frameNumber = pageTable[pageNumber];
    physicalAddress = (frameNumber * pageSize) + offset;

    printf("\nPage Number      : %d", pageNumber);
    printf("\nOffset           : %d", offset);
    printf("\nFrame Number     : %d", frameNumber);
    printf("\nPhysical Address : %d\n", physicalAddress);

    return 0;
}
```

## Shell Program (`paging.sh`)

```bash
#!/bin/bash
echo "Enter Page Size:"
read pageSize

echo "Enter Number of Pages:"
read numPages

declare -a pageTable

for ((i=0;i<numPages;i++))
do
    echo "Enter Frame Number for Page $i:"
    read pageTable[$i]
done

echo "Enter Logical Address:"
read logicalAddress

pageNumber=$((logicalAddress / pageSize))
offset=$((logicalAddress % pageSize))

if [ $pageNumber -ge $numPages ]
then
    echo "Invalid Logical Address"
    exit
fi

frameNumber=${pageTable[$pageNumber]}
physicalAddress=$((frameNumber * pageSize + offset))

echo "Page Number      : $pageNumber"
echo "Offset           : $offset"
echo "Frame Number     : $frameNumber"
echo "Physical Address : $physicalAddress"
```

## Output

```text
Enter Page Size: 1000
Enter Number of Pages: 4
Enter Frame Numbers for Each Page:
Page 0 -> Frame: 5
Page 1 -> Frame: 6
Page 2 -> Frame: 1
Page 3 -> Frame: 2
Enter Logical Address: 2350

Page Number      : 2
Offset           : 350
Frame Number     : 1
Physical Address : 1350
```
