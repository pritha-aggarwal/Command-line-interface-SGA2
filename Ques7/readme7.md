## **Command Line Interface Graded Lab Assignment 2, submitted by Pritha Aggarwal**

Linux Commands testing assignment  
Personal Ubuntu Used-

### **Question7**  
Write a shell script patterns.sh that reads a text file and:
• Writes words containing ONLY vowels into vowels.txt
• Writes words containing ONLY consonants into consonants.txt
• Writes words containing both vowels and consonants but starting with a consonant into mixed.txt, Case should be ignored while checking patterns.  

**Command**:
```bash
#!/bin/bash

INPUT="words.txt"

# Check if input file exists
if [ ! -f "$INPUT" ]; then
    echo "Error: $INPUT not found."
    exit 1
fi

# Prepare the cleaned word list (one word per line, no punctuation)
# This makes it much easier to run regex on individual words
CLEAN_WORDS=$(tr -s '[:space:]' '\n' < "$INPUT" | tr -d '[:punct:]')

# 1. Words containing ONLY vowels
# Pattern: From start (^) to end ($), every character must be a, e, i, o, or u.
echo "$CLEAN_WORDS" | grep -iE "^[aeiou]+$" > vowels.txt

# 2. Words containing ONLY consonants
# Pattern: From start (^) to end ($), every character must be a consonant.
echo "$CLEAN_WORDS" | grep -iE "^[bcdfghjklmnpqrstvwxyz]+$" > consonants.txt

# 3. Mixed words starting with a consonant
# Pattern: Starts with a consonant, followed by any letters, 
# AND it must contain at least one vowel (filtered via a second grep).
echo "$CLEAN_WORDS" | grep -iE "^[bcdfghjklmnpqrstvwxyz][a-z]*$" | grep -iE "[aeiou]" > mixed.txt

echo "Processing complete."
echo "vowels.txt:     $(wc -l < vowels.txt) words"
echo "consonants.txt: $(wc -l < consonants.txt) words"
echo "mixed.txt:      $(wc -l < mixed.txt) words"
```
**Output**:  
![img1](images7/img1.png)   

Explanation: ^ and $: These are anchors. ^ means the start of the word, and $ means the end. Without these, grep would find "apple" in the vowel list because "a" is a vowel. With them, it forces the entire word to match.

**[aeiou]+:** The square brackets define a set of allowed characters. The + means "one or more."

The first grep ^[bcdfghjklmnpqrstvwxyz][a-z]*$ ensures the word starts with a consonant and contains only letters.

The second piped grep [aeiou] ensures the word must have at least one vowel. Since it already passed the "starts with consonant" check, this naturally results in a "mixed" word.
