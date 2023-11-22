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
![image](https://github.com/SOWMIYA2003/OS/assets/93427443/d587fde4-9964-4cfd-8192-569b31bce724)
```
#include <stdio.h>

int main() {
  int process[4], burstTime[4], waitingTime[4], turnaroundTime[4];
  int totalWaitingTime = 0, totalTurnaroundTime = 0;
  float avgWaitingTime, avgTurnaroundTime;

  // Process ID
  process[0] = 0;
  process[1] = 1;
  process[2] = 2;
  process[3] = 3;

  // Burst time
  burstTime[0] = 2;
  burstTime[1] = 4;
  burstTime[2] = 3;
  burstTime[3] = 6;

  // Waiting time calculation
  for (int i = 0; i < 4; i++) {
    if (i == 0) {
      waitingTime[i] = 0;
    } else {
      waitingTime[i] = waitingTime[i - 1] + burstTime[i - 1];
    }
  }

  // Turnaround time calculation
  for (int i = 0; i < 4; i++) {
    turnaroundTime[i] = burstTime[i] + waitingTime[i];
  }

  // Calculate total waiting time
  for (int i = 0; i < 4; i++) {
    totalWaitingTime += waitingTime[i];
  }

  // Calculate total turnaround time
  for (int i = 0; i < 4; i++) {
    totalTurnaroundTime += turnaroundTime[i];
  }

  // Calculate average waiting time
  avgWaitingTime = totalWaitingTime / 4;

  // Calculate average turnaround time
  avgTurnaroundTime = totalTurnaroundTime / 4;

  printf("Process\tBurst Time\tWaiting Time\tTurnaround Time\n");
  for (int i = 0; i < 4; i++) {
    printf("%d\t\t%d\t\t%d\t\t%d\n", process[i], burstTime[i], waitingTime[i], turnaroundTime[i]);
  }

  printf("\nAverage waiting time: %.2f ms\n", avgWaitingTime);
  printf("Average turnaround time: %.2f ms\n", avgTurnaroundTime);

  return 0;
}

```
![image](https://github.com/SOWMIYA2003/OS/assets/93427443/f977c5a3-7737-4993-8fa5-702e6588fc58)
# --------------------------------------------------------------------------------------------
![image](https://github.com/SOWMIYA2003/OS/assets/93427443/bcef44b4-aff6-41fa-bcc4-2738bba355e1)

```
#include <stdio.h>

void roundRobin(int process[], int arrivalTime[], int burstTime[], int n, int quantumTime) {
  int waitingTime[n], turnaroundTime[n], completionTime[n];
  int totalWaitingTime = 0, totalTurnaroundTime = 0;

  // Calculate waiting time for each process
  for (int i = 0; i < n; i++) {
    waitingTime[i] = 0;
    for (int j = 0; j < i; j++) {
      if (arrivalTime[j] <= arrivalTime[i]) {
        waitingTime[i] += burstTime[j];
      }
    }
  }

  // Calculate completion time for each process
  for (int i = 0; i < n; i++) {
    completionTime[i] = waitingTime[i] + burstTime[i];
  }

  // Calculate turnaround time for each process
  for (int i = 0; i < n; i++) {
    turnaroundTime[i] = completionTime[i] - arrivalTime[i];
    totalWaitingTime += waitingTime[i];
    totalTurnaroundTime += turnaroundTime[i];
  }

  // Display the results
  printf("Process\tArrival Time\tBurst Time\tWaiting Time\tTurnaround Time\n");
  for (int i = 0; i < n; i++) {
    printf("%5d\t%10d\t%10d\t%10d\t%10d\n", process[i], arrivalTime[i], burstTime[i], waitingTime[i], turnaroundTime[i]);
  }

  printf("\nAverage waiting time: %.2f ms\n", (float)totalWaitingTime / n);
  printf("Average turnaround time: %.2f ms\n", (float)totalTurnaroundTime / n);
}

int main() {
  int process[] = {0, 1, 2, 3};
  int arrivalTime[] = {0, 0, 1, 3};
  int burstTime[] = {2, 4, 3, 6};
  int n = sizeof(process) / sizeof(process[0]);
  int quantumTime = 2;

  roundRobin(process, arrivalTime, burstTime, n, quantumTime);

  return 0;
}

```
![image](https://github.com/SOWMIYA2003/OS/assets/93427443/bc815b83-164e-41f0-abf1-1f6515285abc)
# -----------------------------------------------------------------------------------------

![image](https://github.com/SOWMIYA2003/OS/assets/93427443/1844a39a-0b96-41e3-ae34-92a8ac82173b)
```
#include <stdio.h>

typedef struct process {
  int processId;
  int priority;
  int burstTime;
  int arrivalTime;
  int waitingTime;
  int turnaroundTime;
} Process;

void prioritizeProcesses(Process processes[], int n) {
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < n - 1; j++) {
      if (processes[j].priority > processes[j + 1].priority) {
        Process temp = processes[j];
        processes[j] = processes[j + 1];
        processes[j + 1] = temp;
      }
    }
  }
}

void calculateWaitingTime(Process processes[], int n) {
  processes[0].waitingTime = 0;

  for (int i = 1; i < n; i++) {
    int previousBurstTime = 0;
    for (int j = 0; j < i; j++) {
      previousBurstTime += processes[j].burstTime;
    }

    processes[i].waitingTime = previousBurstTime - processes[i].arrivalTime;
  }
}

void calculateTurnaroundTime(Process processes[], int n) {
  for (int i = 0; i < n; i++) {
    processes[i].turnaroundTime = processes[i].waitingTime + processes[i].burstTime;
  }
}

void printProcessDetails(Process processes[], int n) {
  printf("Process\tPriority\tArrival Time\tBurst Time\tWaiting Time\tTurnaround Time\n");
  for (int i = 0; i < n; i++) {
    printf("%5d\t%5d\t%10d\t%10d\t%10d\t%10d\n", processes[i].processId, processes[i].priority, processes[i].arrivalTime, processes[i].burstTime, processes[i].waitingTime, processes[i].turnaroundTime);
  }
}

void calculateAverageWaitingTimeAndTurnaroundTime(Process processes[], int n) {
  int totalWaitingTime = 0;
  int totalTurnaroundTime = 0;

  for (int i = 0; i < n; i++) {
    totalWaitingTime += processes[i].waitingTime;
    totalTurnaroundTime += processes[i].turnaroundTime;
  }

  float averageWaitingTime = (float) totalWaitingTime / n;
  float averageTurnaroundTime = (float) totalTurnaroundTime / n;

  printf("\nAverage waiting time: %.2f ms\n", averageWaitingTime);
  printf("Average turnaround time: %.2f ms\n", averageTurnaroundTime);
}

int main() {
  Process processes[] = {
    {0, 3, 9, 0},
    {1, 1, 4, 0},
    {2, 4, 5, 0},
    {3, 2, 2, 0}
  };

  int n = sizeof(processes) / sizeof(processes[0]);

  prioritizeProcesses(processes, n);
  calculateWaitingTime(processes, n);
  calculateTurnaroundTime(processes, n);

  printProcessDetails(processes, n);
  calculateAverageWaitingTimeAndTurnaroundTime(processes, n);

  return 0;
}

```
![image](https://github.com/SOWMIYA2003/OS/assets/93427443/e362853f-0cc1-4ee1-a722-423c5d57531e)
# -------------------------------------------------------------------
![image](https://github.com/SOWMIYA2003/OS/assets/93427443/aa7c0b33-12d6-4cfb-b2be-1082258533c8)
```
#include <stdio.h>

int main() {
  int process[3], burstTime[3], waitingTime[3], turnaroundTime[3];
  int totalWaitingTime = 0, totalTurnaroundTime = 0;
  int avgWaitingTime, avgTurnaroundTime;

  // Process ID
  process[0] = 0;
  process[1] = 1;
  process[2] = 2;

  // Burst time
  burstTime[0] = 9;
  burstTime[1] = 4;
  burstTime[2] = 9;

  // Waiting time calculation
  for (int i = 0; i < 3; i++) {
    if (i == 0) {
      waitingTime[i] = 0;
    } else {
      waitingTime[i] = waitingTime[i - 1] + burstTime[i - 1];
    }
  }

  // Turnaround time calculation
  for (int i = 0; i < 3; i++) {
    turnaroundTime[i] = burstTime[i] + waitingTime[i];
  }

  // Calculate total waiting time
  for (int i = 0; i < 3; i++) {
    totalWaitingTime += waitingTime[i];
  }

  // Calculate total turnaround time
  for (int i = 0; i < 3; i++) {
    totalTurnaroundTime += turnaroundTime[i];
  }

  // Calculate average waiting time
  avgWaitingTime = totalWaitingTime / 3;

  // Calculate average turnaround time
  avgTurnaroundTime = totalTurnaroundTime / 3;

  printf("Process\tBurst Time\tWaiting Time\tTurnaround Time\n");
  for (int i = 0; i < 3; i++) {
    printf("%d\t\t%d\t\t%d\t\t%d\n", process[i], burstTime[i], waitingTime[i], turnaroundTime[i]);
  }

  printf("\nAverage waiting time: %d ms\n", avgWaitingTime);
  printf("Average turnaround time: %d ms\n", avgTurnaroundTime);

  return 0;
}

```
![image](https://github.com/SOWMIYA2003/OS/assets/93427443/2727d841-e5a4-4f34-ba81-92819a519a9b)
# ------------------------------------------------------------------------------------
![image](https://github.com/SOWMIYA2003/OS/assets/93427443/2ae436e1-4e11-4617-afa7-35b325488fd4)
```
#include <stdio.h>

int main() {
  int process[3], burstTime[3], waitingTime[3], turnaroundTime[3];
  int totalWaitingTime = 0, totalTurnaroundTime = 0;
  int avgWaitingTime, avgTurnaroundTime;

  // Process ID
  process[0] = 0;
  process[1] = 1;
  process[2] = 2;

  // Burst time
  burstTime[0] = 9;
  burstTime[1] = 4;
  burstTime[2] = 9;

  // Waiting time calculation
  for (int i = 0; i < 3; i++) {
    if (i == 0) {
      waitingTime[i] = 0;
    }
    else {
      waitingTime[i] = waitingTime[i - 1] + burstTime[i - 1];
    }
  }

  // Turnaround time calculation
  for (int i = 0; i < 3; i++) {
    turnaroundTime[i] = burstTime[i] + waitingTime[i];
  }

  // Calculate total waiting time
  for (int i = 0; i < 3; i++) {
    totalWaitingTime += waitingTime[i];
  }

  // Calculate total turnaround time
  for (int i = 0; i < 3; i++) {
    totalTurnaroundTime += turnaroundTime[i];
  }

  // Calculate average waiting time
  avgWaitingTime = totalWaitingTime / 3;

  // Calculate average turnaround time
  avgTurnaroundTime = totalTurnaroundTime / 3;

  printf("Process\tBurst Time\tWaiting Time\tTurnaround Time\n");
  for (int i = 0; i < 3; i++) {
    printf("%d\t\t%d\t\t%d\t\t%d\n", process[i], burstTime[i], waitingTime[i], turnaroundTime[i]);
  }

  printf("\nAverage waiting time: %d ms\n", avgWaitingTime);
  printf("Average turnaround time: %d ms\n", avgTurnaroundTime);

  return 0;
}

```
![image](https://github.com/SOWMIYA2003/OS/assets/93427443/9574e002-3f53-4376-8ff6-012ef7753f4b)
# -----------------------------------------------------
![image](https://github.com/SOWMIYA2003/OS/assets/93427443/f92c0540-6a0a-4958-a245-0fa1c7f3ade1)
# -------------------------------------------------------------------------
![image](https://github.com/SOWMIYA2003/OS/assets/93427443/57222481-bcfa-4bac-9499-b8b68e410bc2)
# -----------------------------------------------------------------------------------

