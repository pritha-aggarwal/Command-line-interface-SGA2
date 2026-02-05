## **Command Line Interface Graded Lab Assignment 2, submitted by Pritha Aggarwal**

Linux Commands testing assignment  
Personal Ubuntu Used-

### **Question1**  
Create a shell script named analyze.sh that accepts exactly ONE command-line argument.
• If the argument is a file: – Display the number of lines, words, and characters in the file.
• If the argument is a directory: – Display the total number of files present. – Display the number of .txt files in the directory.
• If the argument count is invalid or the path does not exist: – Display an appropriate error message.

**1** User Identity Verification.  

**Command**:
```bash
id  
```
**Output**:  
![img1](images1/q1img1.png)   

Explanation: **'id'** is the command used for user identity verification. This command returns **UID, GID and all groups** associated with user.

**2** Workspace Validation. Display the current working directory and list all files and directories in that location using long format listing command.  

**Command**:
```bash
pwd && ls -l  
```
**Output**:  
![img2](images1/q1img2.png)   

Explanation: **'pwd'** returns the present working directory i.e. the directly being used currently and **'ls -l'** gives the list of the files in it in the long format (permissions, group, owner, date, size, time and name of file).

**3** Environment Confirmation File. Create a file named user_info.txt and write the line:&quot;Linux user environment verified&quot.  

**Command**: 
```bash
echo "Linux user environment verified" > user_info.txt
```
**Output**:  
![img3](images1/q1img3.png) 

Explanation: **'echo'** writes the given text in the file and **'>'** creates or overwrites (if already existing) the file.

**4** File Integrity Check. Display the number of characters present in user_info.txt.  

**Command**: 
```bash
wc -m user_info.txt
```  
**Output**:  
![img4](images1/q1img4.png) 

Explanation: **'wc'** counts the words, lines  and characters. **-m** specifies that characters are to be counted and not lines or bytes. **user_info.txt** is the target file to be checked.

**5** Learning the Tools. Identify one useful option and briefly explain what it does.  

**Command**: 
```bash
mkdir -p project/2025/data 
``` 
**Output**:  
![img5](images1/q1img5.png) 

Explanation: **'man mkdir'** opens the manual for all the options of mkdir command. **-p** is one of the options, it allows us to create parent directories without having to specify. eg- **'mkdir -p project/2025/data'** , will create any intermediate folders if missing.

**6** Home Directory Inspection. List the contents of your home directory sorted alphabetically. 

**Command**: 
```bash
ls -l ~ 
```
**Output**:  
![img6](images1/q1img6.png) 

Explanation: **'ls'** command gives the list of all content. **'-l'** gives the list in long format. **'~'** specifies that list is to be given from the Home Directory. **'ls'** command by default gives the result in the alphabetic format.

**7** Log Investigation. Search for the word &quot;admin&quot; inside a file named log.txt and display only the matching lines.  

**Command**: 
```bash
grep "admin" log.txt
``` 
**Output**:  
![img7](images1/q1img7.png) 

Explanation: **'grep'** command is the standard linux command for searching text patterns in a file. **'"admin"'** is the word to be searched. **'log.txt'** is the file where a text pattern is to be searched.

**8** System Information Check. Display the Linux kernel version currently running.  

**Command**:   
```bash
uname -r
```
**Output**:  
![img8](images1/q1img8.png)  

Explanation: **'uname'** prints the system information. **'-r'** specifically returns the kernel version information.

**9** Network Connectivity Test. Verify network connectivity by sending ICMP packets to www.google.com.  

**Command**: 
```bash
ping -c 4 www.google.com
```
**Output**:
![img9](images1/q1img9.png)  

Explanation:  **'ping'** sends **ECHO_REQUEST** packets to network host. **'-c 4'** stops the command automatically after sending 4 requests or it will run infinitely. **'www.google.com'** is the address of server.

**10** System Health Awareness. Display the command used to check system uptime and briefly explain its output (uptime duration, number of users, load average). 
 
**Command**: 
```bash
uptime
```
**Output**:
![img10](images1/q1img10.png)  

Explanation:  
**Uptime Duration:** Shows exactly how long the system has been running since the last reboot (days, hours, and minutes).  
**Number of Users:** Displays the total count of users currently logged into the system.  
**Load Average:** Lists three numbers representing the average system load over the last 1, 5, and 15 minutes; values higher than the number of CPU cores indicate the system is over-capacity.

