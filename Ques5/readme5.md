## **Command Line Interface Graded Lab Assignment 2, submitted by Pritha Aggarwal**

Linux Commands testing assignment  
Personal Ubuntu Used-

### **Question5**  
Create a shell script sync.sh to compare two directories dirA and dirB.Your script should:
• List files present only in dirA
• List files present only in dirB
• For files with the same name in both directories, check whether their contents matchDo NOT copy or modify files.Use diff, cmp, or checksum techniques.

**Command**:
```bash
#!/bin/bash

# Check if two arguments are provided
if [ "$#" -ne 2 ]; then
    echo "Usage: $0 <directory1> <directory2>"
    exit 1
fi

DIR_A=$1
DIR_B=$2

# Validate both are directories
if [[ ! -d "$DIR_A" || ! -d "$DIR_B" ]]; then
    echo "Error: Both arguments must be valid directories."
    exit 1
fi

echo "--- Comparing $DIR_A and $DIR_B ---"

# 1. Files present only in dirA
echo -e "\n[ Files only in $DIR_A ]"
comm -23 <(ls "$DIR_A" | sort) <(ls "$DIR_B" | sort)

# 2. Files present only in dirB
echo -e "\n[ Files only in $DIR_B ]"
comm -13 <(ls "$DIR_A" | sort) <(ls "$DIR_B" | sort)

# 3. Comparing content for files with the same name
echo -e "\n[ Content Comparison for matching filenames ]"
echo "------------------------------------------------"

# Find files present in both
COMMON_FILES=$(comm -12 <(ls "$DIR_A" | sort) <(ls "$DIR_B" | sort))

for FILE in $COMMON_FILES; do
    # Only compare if they are both actual files (not sub-directories)
    if [[ -f "$DIR_A/$FILE" && -f "$DIR_B/$FILE" ]]; then
        if cmp -s "$DIR_A/$FILE" "$DIR_B/$FILE"; then
            echo "MATCH: $FILE"
        else
            echo "DIFFER: $FILE (Contents are different)"
        fi
    fi
done
```
**Output**:  
![img1](images5/img1.png)   

Explanation: **comm command:** This is for comparing lists.

**-23:** Suppresses lines unique to the second file and lines common to both. Result: Only things in dirA.

**-13:** Suppresses lines unique to the first file and lines common to both. Result: Only things in dirB.

**-12:** Shows only the lines found in both.

**<(ls ... | sort):** This is called Process Substitution. It takes the output of the ls command and feeds it into comm as if it were a file. comm requires sorted input to work correctly.

**cmp -s:** The -s stands for silent. It doesn't print anything to the screen; it just sets an "exit code." If the exit code is 0, the files are identical; if it's 1, they are different.

