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
#include <stdio.h>
int main() {
    char name[50];
    int grade, i;
    FILE *fptr;
    
    fptr = fopen("grades.txt", "w");
    
    if (fptr == NULL) {
        printf("Error opening file for writing\n");
        return 1;
    }

    for (i = 0; i < 3; i++) {
        printf("Enter Student name %d: ", i + 1);
        scanf("%s", name);

        printf("Enter grade %d: ", i + 1);
        scanf("%d", &grade);

        fprintf(fptr, "%s %d\n", name, grade);
    }
    fclose(fptr);
    fptr = fopen("grades.txt", "r");
    
    if (fptr == NULL) {
        printf("Error opening file for reading\n");
        return 1;
    }
    printf("\nStored Records:\n");
    while (fscanf(fptr, "%s %d", name, &grade) != EOF) {
        printf("Name: %s, Grade: %d\n", name, grade);
    }
    fclose(fptr);

    return 0;
}
```
### Task 7: Inventory Log Appender
```c
#include <stdio.h>

int main() {
    char product[50];
    int quantity;
    FILE *fptr;
    
    fptr = fopen("inventory.txt", "a");

    if (fptr == NULL) {
        printf("Error opening file for appending\n");
        return 1;
    }
    printf("Enter product name: ");
    scanf("%s", product);

    printf("Enter quantity: ");
    scanf("%d", &quantity);
    
    fprintf(fptr, "%s %d\n", product, quantity);
    fclose(fptr);

    fptr = fopen("inventory.txt", "r");

    if (fptr == NULL) {
        printf("Error opening file for reading\n");
        return 1;
    }
    printf("\nInventory Records:\n");
    while (fscanf(fptr, "%s %d", product, &quantity) != EOF) {
        printf("Product: %s, Quantity: %d\n", product, quantity);
    }
    fclose(fptr);

    return 0;
}
```
### Task 8: Survey Result Processor
```c
#include <stdio.h>
int main() {
    int score, i;
    int val;
    int sum = 0;
    float average;
    FILE *fptr;

    fptr = fopen("survey.txt", "w");

    if (fptr == NULL) {
        printf("Error opening file for writing\n");
        return 1;
    }
    printf("Enter 5 survey scores (1–10):\n");
    for (i = 0; i < 5; i++) {
        scanf("%d", &score);
        fprintf(fptr, "%d\n", score);
    }
    fclose(fptr);
    fptr = fopen("survey.txt", "r");

    if (fptr == NULL) {
        printf("Error opening file for reading\n");
        return 1;
    }
    while (fscanf(fptr, "%d", &val) != EOF) {
        sum += val;
    }
    fclose(fptr);
    average = sum / 5.0;

    printf("\nSum = %d\n", sum);
    printf("Average = %.2f\n", average);
    return 0;
}
```
### Task 9: Configuration File Reader
```c
#include <stdio.h>
int main() 
{
    FILE *fptr;
    fptr = fopen("config.txt", "r");

    if (fptr == NULL) {
        printf("Config file not found. Creating default config.txt...\n");

        fptr = fopen("config.txt", "w");

        if (fptr == NULL) {
            printf("Error creating config file\n");
            return 1;
        }
        fprintf(fptr, "max_users=50\n");
        fprintf(fptr, "timeout=30\n");
        fprintf(fptr, "retry_limit=5\n");

        fclose(fptr);

        printf("Default config.txt created successfully.\n");
    } 
    else {
        printf("Config file found. Reading settings...\n");

        char line[100];

        while (fgets(line, sizeof(line), fptr) != NULL) {
            printf("%s", line);
        }
        fclose(fptr);
    }
    return 0;
}
```
### Task 10: Student Report Card Generator
```c
#include <stdio.h>

int main() {
    char name[50];
    int s1, s2, s3;
    float avg;
    char status[10];
    FILE *fptr;
    char line[100];
    
    printf("Enter student name: ");
    scanf(" %[^\n]", name);

    printf("Enter 3 subject scores:\n");
    scanf("%d %d %d", &s1, &s2, &s3);

    avg = (s1 + s2 + s3) / 3.0;

    if (avg >= 50)
        sprintf(status, "PASS");
    else
        sprintf(status, "FAIL");

    fptr = fopen("report.txt", "w+");

    if (fptr == NULL) {
        printf("Error opening file\n");
        return 1;
    }

    fprintf(fptr, "----- Report Card -----\n");
    fprintf(fptr, "Name: %s\n", name);
    fprintf(fptr, "Subject 1: %d\n", s1);
    fprintf(fptr, "Subject 2: %d\n", s2);
    fprintf(fptr, "Subject 3: %d\n", s3);
    fprintf(fptr, "Average: %.2f\n", avg);
    fprintf(fptr, "Status: %s\n", status);

    rewind(fptr);

    printf("\nGenerated Report:\n");
    while (fgets(line, sizeof(line), fptr) != NULL) {
        printf("%s", line);
    }
    
    fclose(fptr);

    return 0;
}
```
