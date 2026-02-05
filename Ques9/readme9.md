## **Command Line Interface Graded Lab Assignment 2, submitted by Pritha Aggarwal**

Linux Commands testing assignment  
Personal Ubuntu Used-

### **Question9**  
Write a C program to demonstrate zombie process prevention.
• Create multiple child processes
• Ensure terminated child processes do not remain zombies
• Parent process should print the PID of each child it cleans upUse fork(), wait(), or waitpid(). 

**Command**:
```bash
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

#define NUM_CHILDREN 3

int main() {
    pid_t pids[NUM_CHILDREN];
    int i;

    printf("Parent process started (PID: %d)\n", getpid());
    printf("------------------------------------\n");

    // 1. Create multiple child processes
    for (i = 0; i < NUM_CHILDREN; i++) {
        pids[i] = fork();

        if (pids[i] < 0) {
            perror("Fork failed");
            exit(1);
        }

        if (pids[i] == 0) {
            // This block is executed by the CHILD
            printf("Child %d started (PID: %d)\n", i + 1, getpid());
            
            // Simulate some work
            sleep(2); 
            
            printf("Child %d (PID: %d) is exiting...\n", i + 1, getpid());
            exit(0); // Child terminates here
        }
    }

    // 2. Parent process logic: Zombie Prevention
    printf("\nParent is waiting to reap children...\n\n");

    for (i = 0; i < NUM_CHILDREN; i++) {
        int status;
        /* waitpid() blocks the parent until the specific child (pids[i]) exits.
           Once it exits, the OS removes the child from the process table.
        */
        pid_t cleaned_pid = waitpid(pids[i], &status, 0);

        if (cleaned_pid > 0) {
            if (WIFEXITED(status)) {
                printf("Parent cleaned up Child PID: %d (Exit Status: %d)\n", 
                        cleaned_pid, WEXITSTATUS(status));
            }
        }
    }

    printf("\nAll children reaped. Parent (PID: %d) exiting.\n", getpid());
    return 0;
}
```
**Output**:  
![img1](images9/img1.png)   

Explanation: When a child calls exit(), it sends a SIGCHLD signal to the parent.

If the parent ignores this or is too busy to handle it, the child becomes a zombie (labeled <defunct> in the ps command).

By calling waitpid(), the parent explicitly asks the kernel for the child's termination information. Once that information is handed over, the kernel officially deletes the child's entry from the process table.
