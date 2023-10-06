# EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS

AIM:
To implement First-Come-First-Serve (FCFS) Scheduling

ALGORITHM:
Start the process Accept the number of processes in the ready queue For each process in the ready queue, do the following: Accept the process ID and burst time Calculate the waiting time for the current process Calculate the turnaround time for the current process Display the process ID, burst time, waiting time and turnaround time for the current process Calculate the average waiting time and average turnaround time Stop the process

PROGRAM:
```
#include<stdio.h>
int main()
{
	int bt[20],p[20],wt[20],tat[20],i,j,n,total=0,pos,temp; float
	avg_wt,avg_tat;
	printf("Enter number of process:");
	scanf("%d",&n);
	printf("\nEnter Burst Time:\n");
	for(i=0;i<n;i++)
	{
		printf("p % d:",i+1);
		scanf("%d",&bt[i]);
		p[i]=i+1; //contains process number
	}
	wt[0]=0; //waiting time for first process will be zero
	//calculate waiting time
	for(i=1;i<n;i++)
	{
		wt[i]=0;
		for(j=0;j<i;j++)
		wt[i]+=bt[j];
		total+=wt[i];
	}
	avg_wt=(float)total/n; //average waiting time
	total=0;
	printf("\nProcess\t Burst Time \tWaiting Time\tTurnaround Time");
	for(i=0;i<n;i++)
	{
		tat[i]=bt[i]+wt[i]; //calculate turnaround time
		total+=tat[i];
		printf("\np%d\t\t %d\t\t %d\t\t\t%d",p[i],bt[i],wt[i],tat[i]);
	}
	avg_tat=(float)total/n; //average turnaround time
	printf("\n\nAverage Waiting Time=%f",avg_wt);
	printf("\nAverage Turnaround Time=%f\n",avg_tat);
}
```
OUTPUT:

![Screenshot 2023-10-06 085602](https://github.com/swetha1510/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/120623583/06838deb-09be-43e2-9fdf-7b3c843caf16)

RESULT:
First-Come-First-Serve Scheduling is implemented successfully.

AIM: 
To implement Shortest Job First (SJF) Preemptive Scheduling

ALGORITHM:
Start the process Accept the number of processes in the ready queue For each process in the ready queue, do the following: Accept the process ID and burst time Calculate the waiting time for the current process Calculate the turnaround time for the current process Display the process ID, burst time, waiting time and turnaround time for the current process Calculate the average waiting time and average turnaround time Stop the process

PROGRAM:
```

#include <stdio.h>
  
int main() 
{
      int arrival_time[10], burst_time[10], temp[10];
      int i, smallest, count = 0, time, limit;
      double wait_time = 0, turnaround_time = 0, end;
      float average_waiting_time, average_turnaround_time;
      printf("\nEnter the Total Number of Processes:");
      scanf("%d", &limit); 
      printf("\nEnter Details of %d Processes", limit);
      for(i = 0; i < limit; i++)
      {
            printf("\nEnter Arrival Time:");
            scanf("%d", &arrival_time[i]);
            printf("\nEnter Burst Time:");
            scanf("%d", &burst_time[i]); 
            temp[i] = burst_time[i];
      }
      burst_time[9] = 9999;  
      for(time = 0; count != limit; time++)
      {
            smallest = 9;
            for(i = 0; i < limit; i++)
            {
                  if(arrival_time[i] <= time && burst_time[i] < burst_time[smallest] && burst_time[i] > 0)
                  {
                        smallest = i;
                  }
            }
            burst_time[smallest]--;
            if(burst_time[smallest] == 0)
            {
                  count++;
                  end = time + 1;
                  wait_time = wait_time + end - arrival_time[smallest] - temp[smallest];
                  turnaround_time = turnaround_time + end - arrival_time[smallest];
            }
      }
      average_waiting_time = wait_time / limit; 
      average_turnaround_time = turnaround_time / limit;
      printf("nnAverage Waiting Time:%lf\n", average_waiting_time);
      printf("Average Turnaround Time:%lf\n", average_turnaround_time);
      return 0;
}
```

OUTPUT:
![Screenshot 2023-10-06 090209](https://github.com/swetha1510/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/120623583/9b3fc702-a06b-4f9f-b9d4-4b5414e5d93d)

## RESULT:
Shortest Job First (SJF) preemptive scheduling is implemented successfully.


AIM:
To implement Shortest Job First (SJF) Non-Preemptive Scheduling

ALGORITHM:
Shortest Job First (SJF) Non-Preemptive Scheduling is a scheduling algorithm that aims to minimize the average waiting time of processes in a CPU scheduling environment. It selects the process with the shortest burst time to execute first. The algorithm operates in a non-preemptive manner, meaning that once a process starts executing, it continues until it completes its entire burst time. To implement SJF, you first determine the burst time for each process and then sort the processes in ascending order of their burst times. The process with the shortest burst time is scheduled to run next. This process continues until all processes have been executed. SJF non-preemptive scheduling is effective in minimizing waiting times for shorter tasks but can lead to longer waiting times for longer tasks if they arrive early in the queue.

PROGRAM:
```
#include <stdio.h>

int main() {
    int n;
    printf("Enter the number of processes: ");
    scanf("%d", &n);

    int process_id[10];
    int arrival_time[10];
    int burst_time[10];
    int completion_time[10];
    int waiting_time[10];
    int turnaround_time[10];

    // Input process information
    for (int i = 0; i < n; i++) {
        process_id[i] = i + 1;
        printf("Enter arrival time for process %d: ", process_id[i]);
        scanf("%d", &arrival_time[i]);
        printf("Enter burst time for process %d: ", process_id[i]);
        scanf("%d", &burst_time[i]);
    }

    // Perform SJF Non-Preemptive Scheduling
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arrival_time[j] > arrival_time[j + 1]) {
                // Swap arrival_time
                int temp = arrival_time[j];
                arrival_time[j] = arrival_time[j + 1];
                arrival_time[j + 1] = temp;

                // Swap burst_time
                temp = burst_time[j];
                burst_time[j] = burst_time[j + 1];
                burst_time[j + 1] = temp;

                // Swap process_id
                temp = process_id[j];
                process_id[j] = process_id[j + 1];
                process_id[j + 1] = temp;
            }
        }
    }

    int time = 0; // Current time

    for (int i = 0; i < n; i++) {
        // Find the process with the smallest burst time that has arrived
        int shortest_job = -1;
        int shortest_time = 10000; // A large initial value

        for (int j = 0; j < n; j++) {
            if (arrival_time[j] <= time && burst_time[j] < shortest_time && burst_time[j] != -1) {
                shortest_job = j;
                shortest_time = burst_time[j];
            }
        }

        if (shortest_job == -1) {
            // No process is available to run at this time
            time++;
        } else {
            // Execute the selected process
            completion_time[shortest_job] = time + burst_time[shortest_job];
            waiting_time[shortest_job] = completion_time[shortest_job] - arrival_time[shortest_job] - burst_time[shortest_job];
            turnaround_time[shortest_job] = waiting_time[shortest_job] + burst_time[shortest_job];
            time = completion_time[shortest_job];
            burst_time[shortest_job] = -1; // Mark the process as completed
        }
    }

    // Display the scheduling information
    printf("\n-----------------------------------\n");
    printf("Process\tAT\tBT\tCT\tWT\tTAT\n");
    printf("-----------------------------------\n");
    for (int i = 0; i < n; i++) {
        printf("P%d\t%d\t%d\t%d\t%d\t%d\n", process_id[i], arrival_time[i],
               burst_time[i], completion_time[i], waiting_time[i],
               turnaround_time[i]);
    }
    printf("-----------------------------------\n");

    return 0;
}

```
OUTPUT:
![Screenshot 2023-10-06 092448](https://github.com/swetha1510/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/120623583/2163daf0-b333-4408-843f-7ca6a8cd7c5c)

RESULT: 
Shortest Job First (SJF) Non-preemptive scheduling is implemented successfully.

AIM:
To implement Round Robin (RR) Scheduling

ALGORITHM:
Start the process Get the number of elements to be inserted Get the value for burst time for individual processes Get the value for time quantum Make the CPU scheduler go around the ready queue allocating CPU to each process for the time interval specified Make the CPU scheduler pick the first process and set time to interrupt after quantum. And after it's expiry dispatch the process If the process has burst time less than the time quantum then the process is released by the CPU If the process has burst time greater than time quantum then it is interrupted by the OS and the process is put to the tail of ready queue and the schedule selects next process from head of the queue Calculate the total and average waiting time and turnaround time Display the results

PROGRAM:
```
#include<stdio.h>
int main()
{
    int st[10],bt[10],wt[10],tat[10],n,tq; 
    int i,count=0,swt=0,stat=0,temp,sq=0;
    float awt,atat;
    printf("Enter the number of processes :");
    scanf("%d",&n);
    printf("\nEnter the burst time of each process: ");
    for(i=0;i<n;i++)
    {
        printf("\np%d",i+1);
        scanf("%d",&bt[i]);
        st[i]=bt[i];
        
    }
    printf("\nenter the time quantum");
    scanf("%d",&tq);
    while(1)
    {
        for(i=0,count=0;i<n;i++)
        {
            temp=tq;
            if(st[i]==0)
            {
                count++;
                continue;
                
            }
            if(st[i]>tq)
            st[i]=st[i]-tq;
            else
            if(st[i]>=0)
            {
                temp=st[i];
                st[i]=0;
                
            }
            sq=sq+temp;
            tat[i]=sq;
            
        }
        if(n==count)
        break;
        
    }
    for(i=0;i<n;i++)
    {
        wt[i]=tat[i]-bt[i];
        swt=swt+wt[i];
        stat=stat+tat[i];
        
    }
    awt=(float)swt/n;
    atat=(float)stat/n;
    printf("\nprocess no\t burst time\t waiting time\t turnaround time\n");
    for(i=0;i<n;i++)
    printf("\n%d\t\t %d\t\t %d\t\t %d\n",i+1,bt[i],wt[i],tat[i]); 
    printf("\nAverage waiting time=%f\nAverage turn around time=%f",awt,atat);
}
```
OUTPUT:

![Screenshot 2023-10-06 090939](https://github.com/swetha1510/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/120623583/9ce21682-e79d-4646-b76a-789f1e4f373c)

RESULT:  
Round Robin (RR) Scheduling is implemented successfully.


AIM: 
To implement Priority Preemptive Scheduling

ALGORITHM:
Start the process Get the number of processes to be inserted Get the corresponding priority of processes Sort the processes according to the priority and allocate the one with highest priority to execute first If two process have same priority then FCFS scheduling algorithm is used Calculate the total and average waiting time and turnaround time Display the values Stop the process
PROGRAM:
```
#include<stdio.h>
struct process
{
    int WT,AT,BT,TAT,PT;
};

struct process a[10];

int main()
{
    int n,temp[10],t,count=0,short_p;
    float total_WT=0,total_TAT=0,Avg_WT,Avg_TAT;
    printf("Enter the number of the process\n");
    scanf("%d",&n);
    printf("Enter the arrival time , burst time and priority of the process\n");
    printf("AT BT PT\n");
    for(int i=0;i<n;i++)
    {
        scanf("%d%d%d",&a[i].AT,&a[i].BT,&a[i].PT);
        
        // copying the burst time in
        // a temp array fot futher use
        temp[i]=a[i].BT;
    }
    
    // we initialize the burst time
    // of a process with maximum 
    a[9].PT=10000;
    
    for(t=0;count!=n;t++)
    {
        short_p=9;
        for(int i=0;i<n;i++)
        {
            if(a[short_p].PT>a[i].PT && a[i].AT<=t && a[i].BT>0)
            {
                short_p=i;
            }
        }
        
        a[short_p].BT=a[short_p].BT-1;
        
        // if any process is completed
        if(a[short_p].BT==0)
        {
            // one process is completed
            // so count increases by 1
            count++;
            a[short_p].WT=t+1-a[short_p].AT-temp[short_p];
            a[short_p].TAT=t+1-a[short_p].AT;
            
            // total calculation
            total_WT=total_WT+a[short_p].WT;
            total_TAT=total_TAT+a[short_p].TAT;
            
        }
    }
    
    Avg_WT=total_WT/n;
    Avg_TAT=total_TAT/n;
    
    // printing of the answer
    printf("ID WT TAT\n");
    for(int i=0;i<n;i++)
    {
        printf("%d %d\t%d\n",i+1,a[i].WT,a[i].TAT);
    }
    
    printf("Avg waiting time of the process  is %f\n",Avg_WT);
    printf("Avg turn around time of the process is %f\n",Avg_TAT);
    
    return 0;
}
```
OUTPUT: 

![Screenshot 2023-10-06 091440](https://github.com/swetha1510/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/120623583/6746d88d-1205-41b9-917c-2cf0e2e92637)

RESULT:
Priority Preemptive scheduling is implemented successfully.


AIM: 
To implement Priority Non-Preemptive Scheduling

ALGORITHM:
Start the process Get the number of processes to be inserted Get the corresponding priority of processes Sort the processes according to the priority and allocate the one with highest priority to execute first If two process have same priority then FCFS scheduling algorithm is used Calculate the total and average waiting time and turnaround time Display the values Stop the process

PROGRAM:
```
#include<stdio.h>
 
int main()
{
    int bt[20],p[20],wt[20],tat[20],pr[20],i,j,n,total=0,pos,temp,avg_wt,avg_tat;
    printf("Enter Total Number of Process:");
    scanf("%d",&n);
 
    printf("\nEnter Burst Time and Priority\n");
    for(i=0;i<n;i++)
    {
        printf("\nP[%d]\n",i+1);
        printf("Burst Time:");
        scanf("%d",&bt[i]);
        printf("Priority:");
        scanf("%d",&pr[i]);
        p[i]=i+1;           
    }
 
    //sorting burst time, priority and process number in ascending order using selection sort
    for(i=0;i<n;i++)
    {
        pos=i;
        for(j=i+1;j<n;j++)
        {
            if(pr[j]<pr[pos])
                pos=j;
        }
 
        temp=pr[i];
        pr[i]=pr[pos];
        pr[pos]=temp;
 
        temp=bt[i];
        bt[i]=bt[pos];
        bt[pos]=temp;
 
        temp=p[i];
        p[i]=p[pos];
        p[pos]=temp;
    }
 
    wt[0]=0;	//waiting time for first process is zero
 
    //calculate waiting time
    for(i=1;i<n;i++)
    {
        wt[i]=0;
        for(j=0;j<i;j++)
            wt[i]+=bt[j];
 
        total+=wt[i];
    }
 
    avg_wt=total/n;      //average waiting time
    total=0;
 
    printf("\nProcess\t    Burst Time    \tWaiting Time\tTurnaround Time");
    for(i=0;i<n;i++)
    {
        tat[i]=bt[i]+wt[i];     //calculate turnaround time
        total+=tat[i];
        printf("\nP[%d]\t\t  %d\t\t    %d\t\t\t%d",p[i],bt[i],wt[i],tat[i]);
    }
 
    avg_tat=total/n;     //average turnaround time
    printf("\n\nAverage Waiting Time=%d",avg_wt);
    printf("\nAverage Turnaround Time=%d\n",avg_tat);
 
	return 0;
}
```
OUTPUT: 
![Screenshot 2023-10-06 091640](https://github.com/swetha1510/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/120623583/7cb9fdb6-1009-47ac-bb93-836266cd3f38)

RESULT:
Priority Non-preemptive scheduling is implemented successfully.

