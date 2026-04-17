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
