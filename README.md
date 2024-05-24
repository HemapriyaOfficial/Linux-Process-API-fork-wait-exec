# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:
```
## C Program to print process ID and parent Process ID using Linux API system calls

#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main(void)
{	      
	       pid_t process_id;
	    
	       pid_t p_process_id;
	      
         process_id = getpid();
	      
	       p_process_id = getppid();
	     


	      printf("The process id: %d\n",process_id);
	      printf("The process id of parent function: %d\n",p_process_id);
	      return 0; }

```












##OUTPUT






![318212892-abd6bc5c-80c2-4a06-a9cc-216fcf14d114](https://github.com/HemapriyaOfficial/Linux-Process-API-fork-wait-exec/assets/147114275/dd9c6e28-9672-4149-9849-d1661051d687)








## C Program to create new process using Linux API system calls fork() and exit()
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main() {
    int pid;
    pid = fork();
    if (pid == -1) {
        perror("fork");
        exit(EXIT_FAILURE);
    }
    else if (pid == 0) {
        printf("I am child, my pid is %d\n", getpid());
        printf("My parent pid is: %d\n", getppid());
        exit(EXIT_SUCCESS);
    }
    else {
        printf("I am parent, my pid is %d\n", getpid());
        sleep(100);
        exit(EXIT_SUCCESS);
    }
    return 0;
}

```









##OUTPUT




![318212938-d69d4941-a7a1-40c3-a644-6ca827ece3b8](https://github.com/HemapriyaOfficial/Linux-Process-API-fork-wait-exec/assets/147114275/4dbace31-5ab2-4331-8026-fd314fd7310a)




## C Program to execute Linux system commands using Linux API system calls exec() family
```
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
int main() {
    pid_t pid = fork();
    if (pid < 0) {
        perror("Fork failed");
        exit(EXIT_FAILURE);
    } else if (pid == 0) {
        printf("This is the child process. Executing 'ls' command.\n");
        execl("/bin/ls", "ls", "-l", NULL); 
        perror("execl failed");
        exit(EXIT_FAILURE);
    } else {
        int status;
        waitpid(pid, &status, 0); // Wait for the child to finish
        if (WIFEXITED(status)) {
            printf("Child process exited with status %d.\n", WEXITSTATUS(status));
        } else {
            printf("Child process did not exit normally.\n");
        }
        printf("Parent process is done.\n");
    }
    return 0;
}
```

























##OUTPUT






![318212955-51df1c38-a5a1-4710-b99f-132d63606fbd](https://github.com/HemapriyaOfficial/Linux-Process-API-fork-wait-exec/assets/147114275/163c3c19-3fd8-478a-9549-0c4fde0ad27c)












# RESULT:
The programs are executed successfully.
