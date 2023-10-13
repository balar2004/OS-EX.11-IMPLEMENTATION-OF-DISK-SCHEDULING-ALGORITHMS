# OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS
## 1.DISK SCHEDULING-FIRST COME FIRST SERVE
## Aim:
To write a program for the first come first serve method of disc scheduling.
## Description:
Disk scheduling is schedule I/O requests arriving for the disk.
It is important because: -
Multiple I/O requests may arrive by different processes and only one I/O request can be served at a time
by the disk controller. Thus other I/O requests need to wait in the waiting queue and need to be
scheduled.
Two or more request may be far from each other so can result in greater disk head movement.
Hard drives are one of the slowest parts of the computer system and thus need to be accessed in an
efficient manner
FCFS is the simplest of all the Disk Scheduling Algorithms. In FCFS, the requests are addressed in the
order they arrive in the disk queue.
## Program:
```
#include <stdio.h>
#include <stdlib.h>
int main() {
    int RQ[100], i, n, TotalHeadMovement = 0, initial;
    printf("Enter the number of Requests\n");
    scanf("%d", &n);
    printf("Enter the Requests sequence\n");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &RQ[i]);
    }
    printf("Enter initial head position\n");
    scanf("%d", &initial);
    for (i = 0; i < n; i++)
    {
        TotalHeadMovement += abs(RQ[i] - initial);
        initial = RQ[i];
    }
    printf("Total head movement is %d\n", TotalHeadMovement);
    return 0;
}
```
## Output:
![disk](https://github.com/balar2004/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/118791778/aca0292e-0b45-4611-afec-466ab9a06529)
## Result:
Thus the implementation of the program for first come first serve disc scheduling has been
successfully executed.

## 2.DISK SCHEDULING-SHORTEST SEEK TIME FIRST
## Aim:
To write a program for the first come first serve method of disc scheduling.
## Description:
Shortest seek time first (SSTF) algorithm
Shortest seek time first (SSTF) algorithm selects the disk I/O request which requires the least disk arm
movement from its current position regardless of the direction. It reduces the total seek time as compared
to FCFS.
## Program:
```
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int RQ[100], i, n, TotalHeadMovement = 0, initial, count = 0;
    printf("Enter the number of Requests\n");
    scanf("%d", &n);
    printf("Enter the Requests sequence\n");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &RQ[i]);
    }
    printf("Enter initial head position\n");
    scanf("%d", &initial);
    while (count != n)
    {
        int min = 10000;
        int index;
        for (i = 0; i < n; i++) 
        {
            int d = abs(RQ[i] - initial);
            if (d < min)
            {
                min = d;
                index = i;
            }
        }
        TotalHeadMovement += min;
        initial = RQ[index];
        RQ[index] = 10000;
        count++;
    }
    printf("Total head movement is %d\n", TotalHeadMovement);
    return 0;
}
```
## Output:
![disk2](https://github.com/balar2004/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/118791778/574359f3-3b3a-4837-a906-697716eba448)
## Result:
Thus the implementation of the program for shortest seek time first disc scheduling has been
successfully executed.

## 3.DISK SCHEDULING-SCAN
## Aim:
To write a program for the first come first serve method of disc scheduling.
## Description:
SCAN
It is also called as Elevator Algorithm. In this algorithm, the disk arm moves into a particular direction
till the end, satisfying all the requests coming in its path, and then it turns backend moves in the reverse
direction satisfying requests coming in its path.
It works in the way an elevator works, elevator moves in a direction completely till the last floor of that
direction and then turns back.
## Program:
```
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int RQ[100], i, j, n, TotalHeadMovement = 0, initial, size, move;
    printf("Enter the number of Requests\n");
    scanf("%d", &n);
    printf("Enter the Requests sequence\n");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &RQ[i]);
    }
    printf("Enter initial head position\n");
    scanf("%d", &initial);
    printf("Enter total disk size\n");
    scanf("%d", &size);
    printf("Enter the head movement direction (1 for high, 0 for low)\n");
    scanf("%d", &move);
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n - i - 1; j++) 
        {
            if(RQ[j] > RQ[j + 1])
            {
                int temp = RQ[j];
                RQ[j] = RQ[j + 1];
                RQ[j + 1] = temp;
            }
        }
    }
    int index;
    for (i = 0; i < n; i++) 
    {
        if (initial < RQ[i])
        {
            index = i;
            break;
        }
    }
    if (move == 1)
    {
        for (i = index; i < n; i++)
        {
            TotalHeadMovement += abs(RQ[i] - initial);
            initial = RQ[i];
        }
        TotalHeadMovement += abs(size - RQ[i - 1] - 1);
        initial = size - 1;
        for (i = index - 1; i >= 0; i--)
        {
            TotalHeadMovement += abs(RQ[i] - initial);
            initial = RQ[i];
        }
    }
    else
    {
        for (i = index - 1; i >= 0; i--)
        {
            TotalHeadMovement += abs(RQ[i] - initial);
            initial = RQ[i];
        }
        TotalHeadMovement += abs(RQ[i + 1] - 0);
        initial = 0;
        for (i = index; i < n; i++)
        {
            TotalHeadMovement += abs(RQ[i] - initial);
            initial = RQ[i];
        }
    }
    printf("Total head movement is %d\n", TotalHeadMovement);
    return 0;
}
```
## Output:
![disk3](https://github.com/balar2004/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/118791778/c4bc80ec-b022-4e05-8e84-8bb7509e61de)
## Result:
Thus the implementation of the program for SCAN disc scheduling has been successfully executed.

## 4.DISK SCHEDULING-LOOK
## Aim:
To write a program for the first come first serve method of disc scheduling.
## Description
Look
It is similar to the SCAN disk scheduling algorithm except for the difference that the disk arm in spite of
going to the end of the disk goes only to the last request to be serviced in front of the head and then
reverses its direction from there only. Thus, it prevents the extra delay which occurred due to unnecessary
traversal to the end of the disk.
## Program:
```
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int RQ[100], i, j, n, TotalHeadMovement = 0, initial, size, move;
    printf("Enter the number of Requests\n");
    scanf("%d", &n);
    printf("Enter the Requests sequence\n");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &RQ[i]);
    }
    printf("Enter initial head position\n");
    scanf("%d", &initial);
    printf("Enter total disk size\n");
    scanf("%d", &size);
    printf("Enter the head movement direction (1 for high, 0 for low)\n");
    scanf("%d", &move);
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n - i - 1; j++) 
        {
            if (RQ[j] > RQ[j + 1]) 
            {
                int temp = RQ[j];
                RQ[j] = RQ[j + 1];
                RQ[j + 1] = temp;
            }
        }
    }
    int index;
    for (i = 0; i < n; i++)
    {
        if (initial < RQ[i]) 
        {
            index = i;
            break;
        }
    }
    if (move == 1) 
    {
        for (i = index; i < n; i++) 
        {
            TotalHeadMovement += abs(RQ[i] - initial);
            initial = RQ[i];
        }
        for (i = index - 1; i >= 0; i--) {
            TotalHeadMovement += abs(RQ[i] - initial);
            initial = RQ[i];
        }
    } 
    else
    {
        for (i = index - 1; i >= 0; i--)
        {
            TotalHeadMovement += abs(RQ[i] - initial);
            initial = RQ[i];
        }
        for (i = index; i < n; i++)
        {
            TotalHeadMovement += abs(RQ[i] - initial);
            initial = RQ[i];
        }
    }
    printf("Total head movement is %d\n", TotalHeadMovement);
    return 0;
}
```
# Output:
![disk4](https://github.com/balar2004/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/118791778/137317b1-2841-4ff1-9799-454ac18a4e57)
## Result:
Thus the implementation of the program for LOOK disc scheduling has been successfully executed.
