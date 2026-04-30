## Question 1 — The Student Grade Book
### a) Why a static array is a poor choice;
A static array such as: int grades[100];
is allocated at compile time, meaning its size is fixed before the program runs. The memory for 100 integers is reserved regardless of actual need.
In this system, the number of students is not known until runtime after enrollment ends. Therefore, using a static array creates several problems:

#### 1. Lack of flexibility 
•	The size of the array cannot be changed during execution. 
•	The program must assume a fixed maximum (e.g., 100), which may not match actual enrollment. 
#### 2. Memory wastage
•	If fewer students enroll (e.g., 30 students), the remaining space in the array is unused but still allocated. 
#### 3. Risk of overflow
•	If more than 100 students enroll, the array cannot store additional grades. 
•	This leads to buffer overflow, causing undefined behavior or program crashes. 
### b)
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n;

    printf("Enter number of students: ");
    scanf("%d", &n);
    float *grades = malloc(n * sizeof(float));
   
    if (grades == NULL) {
        printf("Memory allocation failed!\n");
        return 1;
    }
    for (int i = 0; i < n; i++) {
        printf("Enter grade for student %d: ", i + 1);
        scanf("%f", &grades[i]);
    }
    printf("\nStudent Grades:\n");
    for (int i = 0; i < n; i++) {
        printf("Student %d: %.2f\n", i + 1, grades[i]);
    }
    free(grades);
    return 0;
```
### c) What happens if free() is forgotten?

If the professor does not use free() after allocating memory with malloc, the program will cause a memory leak.
A memory leak occurs when a program keeps using memory that it has requested from the system but never gives it back, even though that memory is no longer needed.

#### Effects over time:
•	The program continues to consume more and more memory unnecessarily. 
•	Available system memory gradually decreases. 
•	Overall system performance can start to slow down. 
•	If the program runs for a long time (such as server or continuously running applications), it may: 
•	Become significantly slower 
•	Use up all available memory 
•	Eventually crash due to insufficient memory
## Question 2 — The Expanding Contact List
### a) C Program using malloc for 3 contacts
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *contacts;
    int i;
    contacts = (int *)malloc(3 * sizeof(int));
    if (contacts == NULL) {
        printf("Memory allocation failed!\n");
        return 1;
    }
    printf("Enter 3 contact IDs:\n");
    for (i = 0; i < 3; i++) {
        scanf("%d", &contacts[i]);
    }
```
### b) Expanding memory using realloc
```c
    contacts = (int *)realloc(contacts, 5 * sizeof(int));
    if (contacts == NULL) {
        printf("Memory reallocation failed!\n");
        return 1;
    }
    printf("Enter 2 more contact IDs:\n");
    for (i = 3; i < 5; i++) {
        scanf("%d", &contacts[i]);
    }
    printf("\nUpdated Contact List:\n");
    for (i = 0; i < 5; i++) {
        printf("Contact %d: %d\n", i + 1, contacts[i]);
    }
    free(contacts);

    return 0;
}
```
### c) What would happen if realloc fails and returns NULL?
If realloc() fails, it returns NULL. This is dangerous because if we directly assign it back to the original pointer, we lose access to the previously allocated memory.
#### Null Check:
```c
int *temp = realloc(contacts, 5 * sizeof(int));
if (temp == NULL) {
    printf("Reallocation failed!\n");
    free(contacts);   // free old memory safely
    return 1;
}
contacts = temp;
```
A dangling pointer happens when a pointer refers to memory that is no longer valid or has been freed.
In this scenario:
•	If we overwrite contacts with NULL after a failed realloc, we may lose the original memory address. 
•	That original memory still exists but is no longer accessible → this creates a memory leak. 
•	If we free memory but still use the pointer afterward, it becomes a dangling pointer. 

#### How should the pointer be handled after free()?
After freeing memory, the pointer should be set to NULL:
```c
free(contacts);
contacts = NULL;
```

## Question 3 — Sensor Data Buffer

### a) Why calloc is more appropriate than malloc?
Calloc is more suitable for this sensor system because it initializes all allocated memory to zero, while malloc does not.
•	Malloc: allocates memory but does not initialize it (contains garbage values) 
•	Calloc:  allocates memory and sets all bytes to 0 

It is safer choice because in a weather station:
•	Sensor readings must start from a known safe value (0.0) 
•	If garbage values are used, they may be incorrectly treated as real sensor data 
•	This can lead to wrong readings and faulty decisions 

Therefore, calloc is safer because it prevents accidental use of uninitialized (garbage) values.

### b) Write a C program using calloc.
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n;
    printf("Enter number of sensors: ");
    scanf("%d", &n);
    float *buffer = (float *)calloc(n, sizeof(float));

    if (buffer == NULL) {
        printf("Memory allocation failed!\n");
        return 1;  
   }
    printf("\nInitial sensor buffer values:\n");
    for (int i = 0; i < n; i++) {
        printf("Sensor %d: %.2f\n", i + 1, buffer[i]);
    }
    printf("\nEnter temperature readings:\n");
    for (int i = 0; i < n; i++) {
        printf("Sensor %d: ", i + 1);
        scanf("%f", &buffer[i]); 
  }
    printf("\nUpdated sensor readings:\n");
    for (int i = 0; i < n; i++) {
        printf("Sensor %d: %.2f\n", i + 1, buffer[i]);  
    }
    free(buffer);
    return 0;
   }
```
### c) Comparison of malloc and calloc and its importance in sensor applications
#### 1. Memory state immediately after allocation
Assume we allocate memory for 5 float values:
#### Using malloc
```c
float *a = malloc(5 * sizeof(float));
```
Memory is not initialized, so values are unpredictable:
Eg: 
•	Index= a[0] , value after malloc = 12.45 (garbage)
•	Index= a[1] , value after malloc = -0.0032 (garbage)
•	Index= a[2] , value after malloc = 981.27 (garbage)

#### Using calloc
```c
float *b = calloc(5, sizeof(float));
```
Memory is automatically initialized to zero
Eg:
•	Index= b[0] , value after calloc = 0.00
•	Index= b[1] , value after calloc = 0.00
•	Index= b[2] , value after calloc = 0.00

#### 2. Why this is dangerous in a sensor application
In a sensor system (like temperature monitoring):
If malloc is used:
•	The buffer contains garbage values 
•	The system may incorrectly treat them as real sensor readings 
•	This can lead to: 
•	False temperature spikes or drops 
•	Wrong alerts (e.g., overheating alarm triggered incorrectly) 
•	Faulty control decisions in embedded systems

So, in conclusion; 
Malloc: faster but unsafe for uninitialized data (contains garbage values) 
Calloc: safer because it initializes memory to 0.0 
In sensor applications, calloc prevents false readings and system errors caused by random memory values








