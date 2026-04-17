## Objective 1: String Library Functions
### Task 1: Student Name Validator
```c
#include <stdio.h>
#include <string.h>

int main() {
    char name[100];
    int i, valid = 1;
    printf("Enter student name: ");
    fgets(name, sizeof(name), stdin);
    name[strcspn(name, "\n")] = '\0';
    int length = strlen(name);

    if (length < 3 || length > 20) {
        valid = 0;
    }
    if (name[0] == ' ' || name[length - 1] == ' ') {
        valid = 0;
    }
    for (i = 0; i < length; i++) {
        if (name[i] >= '0' && name[i] <= '9') {
            valid = 0;
            break;
        }
    }
    if (valid) {
        printf("Valid Name\n");
    } else {
        printf("Invalid Name\n");
    }
    printf("Length: %d\n", length);

    return 0;
}
```
### Task 2: Password Strength Checker
```c
#include <stdio.h>
#include <string.h>

int main() {
    char storedPassword[] = "Aqsa123";   
    char input[100];
    int attempts = 0;

    while (attempts < 3) {
        printf("Enter password: ");
        scanf(" %[^\n]", input);  

        if (strlen(input) == 0) {
            printf("Password cannot be empty\n");
            continue;
        }
        int result = strcmp(input, storedPassword);

        if (result == 0) {
            printf("Access Granted\n");
            return 0;
        } else {
            attempts++;

            if (result < 0) {
                printf("Incorrect password (Input is alphabetically BEFORE stored password)\n");
            } else {
                printf("Incorrect password (Input is alphabetically AFTER stored password)\n");
            }
            
            if (attempts == 2) {
                if (strncmp(input, storedPassword, 3) == 0) {
                    printf("Hint: First 3 characters match\n");
                } else {
                    printf("Hint: First 3 characters do NOT match\n");
                }
            }
        }
    }

    printf("Account Locked after 3 failed attempts\n");
    return 0;
}
```
### Task 3: Email Formatter & Domain Extractor
```c
#include <stdio.h>
#include <string.h>

int main() {
    char email[100];
    char copy[100];
    char formatted[150] = "Email: ";
    char *atPtr;

    printf("Enter email: ");
    scanf(" %[^\n]", email);

    strcpy(copy, email);

    atPtr = strchr(copy, '@');

    if (atPtr == NULL) {
        printf("Invalid email: '@' not found\n");
        return 0;
    }

    char *domain = atPtr + 1;

    if (strstr(domain, ".") == NULL) {
        printf("Invalid email: domain must contain '.'\n");
        return 0;
    }
    strcat(formatted, copy);
    printf("%s\n", formatted);
    printf("Domain: %s\n", domain);

    return 0;
}
```
## Objective 2: 2D Character Arrays
### Task 4: Classroom Roll Call System
```c
#include <stdio.h>
#include <string.h>

int main() {
    char names[5][30];
    char search[30];
    int i, found = 0;

    printf("Enter names of 5 students:\n");
    for (i = 0; i < 5; i++) {
        printf("Student %d: ", i + 1);
        fgets(names[i], 30, stdin);

        names[i][strcspn(names[i], "\n")] = '\0';
    }

    printf("\nClass List:\n");
    for (i = 0; i < 5; i++) {
        printf("%d. %s\n", i, names[i]);
    }
    printf("\nEnter name to search: ");
    fgets(search, 30, stdin);

    search[strcspn(search, "\n")] = '\0';
    for (i = 0; i < 5; i++) {
        if (strcmp(names[i], search) == 0) {
            printf("Found at position %d\n", i);
            found = 1;
            break;
        }
    }
    if (!found) {
        printf("Student not found\n");
    }
    return 0;
}
```
### Task 5: Word Frequency Counter
```c
#include <stdio.h>
#include <string.h>

int main() {
    char words[6][20];
    int seen[6] = {0};
    int i, j, k, count;

    printf("Enter 6 words: ");
    for (i = 0; i < 6; i++) {
        scanf("%s", words[i]);
    }
    for (i = 0; i < 6; i++) {
        if (seen[i] == 1)
            continue;

        count = 1;
        for (j = i + 1; j < 6; j++) {
            if (strcmp(words[i], words[j]) == 0) {
                count++;
                seen[j] = 1; 
            }
        }
  
        printf("\nWord: %s\n", words[i]);
        printf("Frequency: %d\n", count);
        printf("Characters: ");
        for (k = 0; words[i][k] != '\0'; k++) {
            printf("%c ", words[i][k]);
        }
        printf("\n");
    }
    return 0;
}
```
## Objective 3: File Handling in C
### Task 6: Student Grade Logger
```c
