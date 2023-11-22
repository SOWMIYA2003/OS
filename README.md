# OS
![image](https://github.com/SOWMIYA2003/OS/assets/93427443/9e60e02f-27d1-469f-9c58-0577288d2a14)
```
#include <stdio.h>

typedef struct Process 
{
  int pid, bt, wt, tat;
} Process;

void shortestJobFirst(Process processes[], int n) 
{
  for (int i = 0; i < n; i++) 
  {
    processes[i].wt = 0;
    for (int j = 0; j < i; j++) 
    {
      processes[i].wt += processes[j].bt;
    }
    processes[i].tat = processes[i].bt + processes[i].wt;
  }

  int totalWt = 0, totalTat = 0;
  for (int i = 0; i < n; i++) 
  {
    totalWt += processes[i].wt;
    totalTat += processes[i].tat;
  }

  float avgWt = (float) totalWt / n;
  float avgTat = (float) totalTat / n;

  printf("Process ID | Burst Time | Waiting Time | Turnaround Time\n");
  for (int i = 0; i < n; i++) 
  {
    printf("%d           | %d            | %d              | %d\n", processes[i].pid, processes[i].bt, processes[i].wt, processes[i].tat);
  }

  printf("\nAverage waiting time: %.2f\n", avgWt);
  printf("Average turnaround time: %.2f\n", avgTat);
}

int main() 
{
  Process processes[] = {{0, 2}, {1, 4}, {2, 3}, {3, 6}};
  int n = sizeof(processes) / sizeof(processes[0]);

  shortestJobFirst(processes, n);

  return 0;
}

```
![image](https://github.com/SOWMIYA2003/OS/assets/93427443/0d7d63d4-fa32-4e4f-81c6-d86d1002d640)

# ---------------------------------------------------

