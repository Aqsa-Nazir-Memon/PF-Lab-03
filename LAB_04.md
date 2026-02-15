## Task 1: Sports Team Selection Eligibility

```c
#include <stdio.h>
int main()
{
    float attendence;
    printf("Enter practice attendence percentage:");
    scanf ("%f" , &attendence);
    if (attendence>= 75){
        printf("Selected for Tournament");
    }
    else{
        printf("Not Selected");
    }
    return 0;}
```

## Task 2: Internet Data Usage Category

```c
#include <stdio.h>

int main()
{
    float data;
    printf("Enter total data used in GB:");
    scanf("%f", &data);
    if (data <=50){
        printf("Basic User");
    }
    else if (data<=150){
        printf("Standard User");
    }
    else {
        printf("Heavy User");
    }

    return 0;
}
```

## Task 3: Bank Account Balance Status

```c
#include <stdio.h>

int main()
{
    int balance;
    printf("Enter account balance:");
    scanf("%d", &balance);
    if (balance > 0){
        printf("Positive balance");
    }
    else if (balance < 0){
        printf("Overdrawn");
    }
    else {
        printf("Zero balance");
    }

    return 0;
}
```
## Task 4: Wi-Fi Access Authentication System
```c
#include <stdio.h>
int main()
{
    int password;
    char username[5];
    printf("Enter username:");
    scanf("%s", &username);
     printf("Enter password:");
    scanf("%d", &password);
    if (username[0]=='u'&& username[1]=='s' && username[2]=='e'
    && username[3]=='r' && password == 7890 )
    {
        printf("Connected Successfully");
    }
    else
    {
        printf("Connection Failed");    
    }
    
    return 0;
}
```
## Task 5: Banking Service Menu System
```c
#include <stdio.h>

int main() {
    int choice;
    double balance = 1000.00;   
    double amount;

    printf("     ATM Menu     \n");
    printf("1. Balance Inquiry\n");
    printf("2. Withdraw Money\n");
    printf("3. Deposit Money\n");
    printf("4. Exit\n");
    printf("Enter your choice: ");

    if (scanf("%d", &choice) != 1) {
        printf("Invalid input! Please enter a number between 1 and 4.\n");
        return 1;
    }

    switch(choice) {

        case 1:
            printf("\nYour current balance is: $%.2lf\n", balance);
            break;

        case 2:
            printf("\nEnter amount to withdraw: ");
            
            if (scanf("%lf", &amount) != 1 || amount <= 0) {
                printf("Invalid amount! Please enter a positive number.\n");
            }
            else if (amount > balance) {
                printf("Insufficient balance! Transaction failed.\n");
            }
            else {
                balance -= amount;   
                printf("Withdrawal successful!\n");
                printf("Remaining balance: $%.2lf\n", balance);
            }
            break;

        case 3:
            printf("\nEnter amount to deposit: ");
            
            if (scanf("%lf", &amount) != 1 || amount <= 0) {
                printf("Invalid amount! Please enter a positive number.\n");
            }
            else {
                balance += amount;  
                printf("Deposit successful!\n");
                printf("Updated balance: $%.2lf\n", balance);
            }
            break;

        case 4:
            printf("\nThank you for using the ATM. Goodbye!\n");
            break;

        default:
            printf("\nInvalid choice! Please select between 1 and 4.\n");
    }

    return 0;
}
```
## Task 6: Scholarship Evaluation System
```c
#include <stdio.h>

int main() {
    float marks1, marks2, marks3, marks4, marks5;
    float total, percentage;

    printf("  Scholarship Evaluation System  \n");

    printf("Enter marks for Subject 1 (0-100): ");
    if (scanf("%f", &marks1) != 1 || marks1 < 0 || marks1 > 100) {
        printf("Invalid input! Marks must be between 0 and 100.\n");
        return 1;
    }

    printf("Enter marks for Subject 2 (0-100): ");
    if (scanf("%f", &marks2) != 1 || marks2 < 0 || marks2 > 100) {
        printf("Invalid input! Marks must be between 0 and 100.\n");
        return 1;
    }

    printf("Enter marks for Subject 3 (0-100): ");
    if (scanf("%f", &marks3) != 1 || marks3 < 0 || marks3 > 100) {
        printf("Invalid input! Marks must be between 0 and 100.\n");
        return 1;
    }

    printf("Enter marks for Subject 4 (0-100): ");
    if (scanf("%f", &marks4) != 1 || marks4 < 0 || marks4 > 100) {
        printf("Invalid input! Marks must be between 0 and 100.\n");
        return 1;
    }

    printf("Enter marks for Subject 5 (0-100): ");
    if (scanf("%f", &marks5) != 1 || marks5 < 0 || marks5 > 100) {
        printf("Invalid input! Marks must be between 0 and 100.\n");
        return 1;
    }

    total = marks1 + marks2 + marks3 + marks4 + marks5;
    percentage = (total / 500) * 100;

    printf("\nTotal Marks = %.2f\n", total);
    printf("Percentage = %.2f%%\n", percentage);

    if (percentage >= 85) {
        printf("Result: Full Scholarship\n");
    }
    else if (percentage >= 70) {
        printf("Result: Partial Scholarship\n");
    }
    else if (percentage >= 50) {
        printf("Result: Eligible for Consideration\n");
    }
    else {
        printf("Result: Not Eligible\n");
    }

    return 0;
}
```
## Task 7: Festival Sale Discount Calculator
```c
#include <stdio.h>

int main() {
    float totalAmount, discount = 0, finalAmount;

    printf("  Festival Sale Discount Calculator  \n");

    printf("Enter total purchase amount: ");
    if (scanf("%f", &totalAmount) != 1 || totalAmount < 0) {
        printf("Invalid input! Please enter a positive amount.\n");
        return 1;
    }

    if (totalAmount >= 5000) {
        discount = (totalAmount * 20) / 100;
        printf("You got 20%% discount!\n");
    }
    else if (totalAmount >= 3000) {
        discount = (totalAmount * 10) / 100;
        printf("You got 10%% discount!\n");
    }
    else {
        discount = 0;
        printf("No discount applied.\n");
    }

    finalAmount = totalAmount - discount;

    printf("Discount Amount: %.2f\n", discount);
    printf("Final Amount to Pay: %.2f\n", finalAmount);

    return 0;
}
```
## Task 8: Math Operations Console Using Switch
```c
#include <stdio.h>
#include <math.h> 

int main() {

    int choice;
    double num1, num2, result;

    printf("  Math Operations Console  \n");
    printf("1. Addition\n");
    printf("2. Subtraction\n");
    printf("3. Multiplication\n");
    printf("4. Division\n");
    printf("5. Square of a number\n");
    printf("6. Cube of a number\n");
    printf("7. Square Root of a number\n");
    printf("8. Power (x^y)\n");
    printf("9. Absolute Value\n");
    printf("10. Modulus (Remainder)\n");
    printf("Enter your choice: ");

    if (scanf("%d", &choice) != 1) {
        printf("Invalid input! Please enter a number between 1 and 10.\n");
        return 1;
    }

    switch(choice) {
        
        case 1:
        case 2:
        case 3:
        case 4:
        case 8:
        case 10:

            printf("Enter two numbers: ");
            if (scanf("%lf %lf", &num1, &num2) != 2) {
                printf("Invalid input! Please enter valid numbers.\n");
                return 1;
            }

            if (choice == 1) {
                result = num1 + num2;
                printf("Result = %.2lf\n", result);
            }
            else if (choice == 2) {
                result = num1 - num2;
                printf("Result = %.2lf\n", result);
            }
            else if (choice == 3) {
                result = num1 * num2;
                printf("Result = %.2lf\n", result);
            }
            else if (choice == 4) {
                if (num2 == 0) {
                    printf("Error! Division by zero is not allowed.\n");
                } else {
                    result = num1 / num2;
                    printf("Result = %.2lf\n", result);
                }
            }
            else if (choice == 8) {
                result = pow(num1, num2);
                printf("Result = %.2lf\n", result);
            }
            else if (choice == 10) {
                if ((int)num2 == 0) {
                    printf("Error! Modulus by zero is not allowed.\n");
                } else {
                    result = (int)num1 % (int)num2;
                    printf("Result = %.0lf\n", result);
                }
            }

            break;
            
        case 5:
        case 6:
        case 7:
        case 9:

            printf("Enter one number: ");
            if (scanf("%lf", &num1) != 1) {
                printf("Invalid input! Please enter a valid number.\n");
                return 1;
            }

            if (choice == 5) {
                result = num1 * num1;
                printf("Result = %.2lf\n", result);
            }
            else if (choice == 6) {
                result = num1 * num1 * num1;
                printf("Result = %.2lf\n", result);
            }
            else if (choice == 7) {
                if (num1 < 0) {
                    printf("Error! Square root of negative number is not allowed.\n");
                } else {
                    result = sqrt(num1);
                    printf("Result = %.2lf\n", result);
                }
            }
            else if (choice == 9) {
                result = fabs(num1);
                printf("Result = %.2lf\n", result);
            }

            break;

        default:
            printf("Invalid menu choice! Please select between 1 and 10.\n");
    }

    return 0;
}
```
