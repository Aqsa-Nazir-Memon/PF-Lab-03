## SECTION A — RECURSION
### Q1 Tower Countdown — Staircase Power Bill
```c
#include <stdio.h>

long long totalPower(int floors) {
    if (floors == 1)
        return 100;

    return totalPower(floors - 1) + (100LL * (1LL << (floors - 1)));
}

int main() {
    int floors;

    printf("Enter number of floors: ");
    scanf("%d", &floors);

    if (floors <= 0) {
        printf("Invalid number of floors.\n");
        return 0;
    }
    printf("Total power consumption: %lld kWh\n", totalPower(floors));

    return 0;
}
```
### Q2 Password Strength Checker — Recursive Character Count
```c
 #include <stdio.h>

void countUpperAndDigits(char *str, int *upper, int *digits) {
   
    if (*str == '\0')
        return;
    if (*str >= 'A' && *str <= 'Z')
        (*upper)++;

    if (*str >= '0' && *str <= '9')
        (*digits)++;
    countUpperAndDigits(str + 1, upper, digits);
}
int main() {
    char password[100];
    int upper = 0, digits = 0;

    printf("Enter password: ");
    scanf("%99s", password);
    countUpperAndDigits(password, &upper, &digits);

    printf("Uppercase letters: %d\n", upper);
    printf("Digits: %d\n", digits);

    return 0;
}
```
### Q3 Maze Escape — Recursive Path Finder
```c
#include <stdio.h>

int countWays(int n) {
    if (n == 0 || n == 1)
        return 1;

    return countWays(n - 1) + countWays(n - 2);
}
void printPaths(int n, int path[], int index) {
    if (n == 0) {
        for (int i = 0; i < index; i++) {
            printf("%d", path[i]);
            if (i < index - 1)
                printf("+");
        }
        printf("\n");
        return;
    }
    if (n < 0)
        return;

    path[index] = 1;
    printPaths(n - 1, path, index + 1);

    path[index] = 2;
    printPaths(n - 2, path, index + 1);
}
int main() {
    int n;
    int path[20];

    printf("Enter N (1 to 15): ");
    scanf("%d", &n);

    if (n < 1 || n > 15) {
        printf("Invalid input.\n");
        return 0;
    }
    printf("Total ways: %d\n", countWays(n));
    printf("Paths:\n");
    printPaths(n, path, 0);

    return 0;
}
```
## SECTION B — STRUCTURES
### Q4 Hospital Patient Registry
```c
#include <stdio.h>
#include <string.h>

struct Patient {
    char name[50];
    int age;
    char bloodType[5];
    int patientID;
    char diagnosis[100];
};
void displayAll(struct Patient p[], int n) {
    printf("\n--- Patient Records ---\n");
    printf("ID\tName\tAge\tBlood\tDiagnosis\n");

    for (int i = 0; i < n; i++) {
        printf("%d\t%s\t%d\t%s\t%s\n",
               p[i].patientID,
               p[i].name,
               p[i].age,
               p[i].bloodType,
               p[i].diagnosis);
    }
}

void searchByID(struct Patient p[], int n, int id) {
    for (int i = 0; i < n; i++) {
        if (p[i].patientID == id) {
            printf("\nPatient Found:\n");
            printf("ID: %d\nName: %s\nAge: %d\nBlood Type: %s\nDiagnosis: %s\n",
                   p[i].patientID,
                   p[i].name,
                   p[i].age,
                   p[i].bloodType,
                   p[i].diagnosis);
            return;
        }
    }
    printf("Patient not found.\n");
}

int main() {
    struct Patient p[5];  
    int id;

    for (int i = 0; i < 5; i++) {
        printf("\nEnter details for Patient %d\n", i + 1);

        printf("Name: ");
        scanf(" %[^\n]", p[i].name);

        printf("Age: ");
        scanf("%d", &p[i].age);

        printf("Blood Type: ");
        scanf(" %s", p[i].bloodType);

        printf("Patient ID: ");
        scanf("%d", &p[i].patientID);

        printf("Diagnosis: ");
        scanf(" %[^\n]", p[i].diagnosis);
    }

    displayAll(p, 5);
    printf("\nEnter Patient ID to search: ");
    scanf("%d", &id);

    searchByID(p, 5, id);

    return 0;
}
```
### Q5 University Course Catalog — Nested Structures
```c
#include <stdio.h>
#include <string.h>

struct Department {
    char deptCode[10];
    char deptName[50];
};

struct Course {
    char courseCode[10];
    char courseName[60];
    int creditHours;
    struct Department dept; 
};
void displayAll(struct Course c[], int n) {
    printf("\n--- Course Catalog ---\n");

    for (int i = 0; i < n; i++) {
        printf("\nCourse Code: %s\n", c[i].courseCode);
        printf("Course Name: %s\n", c[i].courseName);
        printf("Credit Hours: %d\n", c[i].creditHours);
        printf("Department Code: %s\n", c[i].dept.deptCode);
        printf("Department Name: %s\n", c[i].dept.deptName);
    }
}

void searchByDept(struct Course c[], int n, char code[]) {
    int found = 0;

    printf("\n--- Courses in Department %s ---\n", code);

    for (int i = 0; i < n; i++) {
        if (strcmp(c[i].dept.deptCode, code) == 0) {
            printf("\nCourse Code: %s\n", c[i].courseCode);
            printf("Course Name: %s\n", c[i].courseName);
            printf("Credit Hours: %d\n", c[i].creditHours);
            printf("Department: %s\n", c[i].dept.deptName);
            found = 1;
        }
    }

    if (!found) {
        printf("No courses found for this department.\n");
    }
}

int main() {
    struct Course c[3];
    char searchCode[10];

    for (int i = 0; i < 3; i++) {
        printf("\nEnter details for Course %d\n", i + 1);

        printf("Course Code: ");
        scanf(" %s", c[i].courseCode);

        printf("Course Name: ");
        scanf(" %[^\n]", c[i].courseName);

        printf("Credit Hours: ");
        scanf("%d", &c[i].creditHours);

        printf("Department Code: ");
        scanf(" %s", c[i].dept.deptCode);

        printf("Department Name: ");
        scanf(" %[^\n]", c[i].dept.deptName);
    }
    displayAll(c, 3);

    printf("\nEnter Department Code to search: ");
    scanf(" %s", searchCode);

    searchByDept(c, 3, searchCode);

    return 0;
}
```
### Q6 E-Commerce Order Tracker
```c
#include <stdio.h>
#include <string.h>

struct Order {
    int orderID;
    char customerName[50];
    char productName[50];
    int quantity;
    float unitPrice;
    char status[20];
};

float computeTotal(struct Order o) {
    return o.quantity * o.unitPrice;
}

void filterByStatus(struct Order orders[], int n, char *status) {
    printf("\n--- Orders with status: %s ---\n", status);

    for (int i = 0; i < n; i++) {
        if (strcmp(orders[i].status, status) == 0) {
            printf("\nOrder ID: %d\n", orders[i].orderID);
            printf("Customer: %s\n", orders[i].customerName);
            printf("Product: %s\n", orders[i].productName);
            printf("Quantity: %d\n", orders[i].quantity);
            printf("Unit Price: %.2f\n", orders[i].unitPrice);
            printf("Total Bill: %.2f\n", computeTotal(orders[i]));
            printf("Status: %s\n", orders[i].status);
        }
    }
}

int main() {
    struct Order orders[4];
    char statusSearch[20];

    for (int i = 0; i < 4; i++) {
        printf("\nEnter details for Order %d\n", i + 1);

        printf("Order ID: ");
        scanf("%d", &orders[i].orderID);

        printf("Customer Name: ");
        scanf(" %[^\n]", orders[i].customerName);

        printf("Product Name: ");
        scanf(" %[^\n]", orders[i].productName);

        printf("Quantity: ");
        scanf("%d", &orders[i].quantity);

        printf("Unit Price: ");
        scanf("%f", &orders[i].unitPrice);

        printf("Status (Pending/Shipped/Delivered): ");
        scanf(" %s", orders[i].status);
    }

    printf("\n--- Order Bills ---\n");
    for (int i = 0; i < 4; i++) {
        printf("\nOrder ID: %d\n", orders[i].orderID);
        printf("Total Bill: %.2f\n", computeTotal(orders[i]));
    }

    printf("\nEnter status to filter: ");
    scanf(" %s", statusSearch);

    filterByStatus(orders, 4, statusSearch);

    return 0;
}
```
