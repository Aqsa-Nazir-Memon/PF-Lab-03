## 1. Gym Membership Discount Evaluation (Nested If-Else)

```c
#include <stdio.h>
int main(){
    int fitnessScore, age;
    printf("Enter FitnessScore:");
    scanf ("%d", &fitnessScore);
    printf("Enter Age:");
    scanf("%d", &age);
    if (fitnessScore>=85){
        if(age<25){
        printf("Discount: 40%%\n");
    }
    else{
        printf("Discount: 25%%\n");
    }
    } else{
        if(fitnessScore>= 70 && age<30){
            printf("Discount: 15%%\n");
        } else{
            printf("No Discount\n");
        }
    }
    return 0;
}
```
## 2. Mobile Data Billing System (Nested If-Else + Logical Operators)
```c
#include<stdio.h>
int main(){
    float data, rate, totalbill;
    int customertype;
    printf("Enter Data Usage in GB: ");
    scanf("%f", &data);
    printf("Enter customer type: 1 = Prepaid, 2 = Postpaid:  ");
    scanf("%d", &customertype);
    if (data<= 2){
        rate = 50;
    }
     else if (data>2 && data<=10){
        if (customertype==1){
            rate = 40;
        }
        else if (customertype==2){
            rate = 35;
        }
        else {
        printf("Invalid Input!");
        return 1;
        }
        } else{
        rate = 25;
    }
    totalbill = data * rate;
    printf ("Rate per GB: Rs. %.2f\n", rate);
    printf("Total BIll: Rs. %.2f\n" , totalbill);
    
    return 0;}
```
## 3. Airport Luggage Fee Calculator (Nested Switch-Case)
```c
#include <stdio.h>
int main(){
    int handbag, checkedbag;
    float weight, rate, totalfee;
    
    printf("Select Main Luggage Type:\n");
    printf("1. Handbag\n");
    printf("2. Checked Bag\n");
    printf("3. Sports Equipment\n");
    printf("Enter choice: ");
    scanf("%d", &handbag);
    
    printf("Enter weight in KG ");
    scanf("%f", &weight);
    
    switch (handbag){
        case 1:
        printf("Select Handbag Type:\n");
    printf("1. Small\n");
    printf("2. Large\n");
    printf("Enter choice: ");
    scanf("%d", &handbag);
    
        switch (handbag){
        case 1:
            rate = 100;
            break;
        case 2:
            rate = 200;
            break;
        default:
            printf("Invalid Type");
            return 0; }
        break;
        case 2:
        printf("Select CheckedBag Type:\n");
    printf("1. Domestic\n");
    printf("2. International\n");
    printf("Enter choice: ");
    scanf("%d", &checkedbag);
    
        switch (checkedbag){
        case 1:
            rate = 300;
            break;
        case 2:
            rate = 500;
            break;
        default:
            printf("Invalid Type");
            return 0;
        }
        break;
        case 3:
            rate = 1000;
            break;
      default:
        printf("Invalid Input");
        return 0;
    }
    totalfee = weight * rate;
    printf("Rate per kg: Rs. %.2f\n", rate);
      printf("Total Fee: Rs. %.2f\n", totalfee);
    return 0;
}
```
## 4. Online Bookstore Ordering System (Nested Switch-Case)
```c
#include <stdio.h>

int main() {
    int category, choice, quantity;
    int price = 0, total = 0;

    printf("  Online Bookstore  \n");
    printf("Select Book Category:\n");
    printf("1. Fiction\n");
    printf("2. Non-Fiction\n");
    printf("Enter your choice: ");
    scanf("%d", &category);

    switch(category) {

        case 1:
            printf("1. Novel (Rs. 600)\n");
            printf("2. Comic (Rs. 300)\n");
            printf("Enter your choice: ");
            scanf("%d", &choice);

            switch(choice) {
                case 1:
                    price = 600;
                    break;
                case 2:
                    price = 300;
                    break;
                default:
                    printf("Invalid Fiction choice!\n");
                    return 0;
            }
            break;

        case 2:
            printf("1. Biography (Rs. 800)\n");
            printf("2. Self-Help (Rs. 500)\n");
            printf("Enter your choice: ");
            scanf("%d", &choice);

            switch(choice) {
                case 1:
                    price = 800;
                    break;
                case 2:
                    price = 500;
                    break;
                default:
                    printf("Invalid Non-Fiction choice!\n");
                    return 0;
            }
            break;

        default:
            printf("Invalid Category choice!\n");
            return 0;
    }

    printf("Enter quantity: ");
    scanf("%d", &quantity);

    total = price * quantity;

    printf("Total Bill = Rs. %d\n", total);

    return 0; }
```
## 5. Staff Incentive Calculation (Nested Ternary Operator)
```c
#include <stdio.h>

int main() {
    float salary, incentive;
    int service;

    printf("Enter salary: ");
    scanf("%f", &salary);

    printf("Enter years of service: ");
    scanf("%d", &service);

    incentive = (service > 15) ? (0.35 * salary) :
                (service > 7)  ? (0.20 * salary) :
                                 (0.05 * salary);

    printf("Incentive Amount = %.2f\n", incentive);

    return 0; }
```
## 6. Quadrilateral Type Identifier (Nested If-Else + Relational Operators)
```c
#include <stdio.h>

int main() {
    float a, b, c, d;
    printf("Enter four sides: ");
    scanf("%f %f %f %f", &a, &b, &c, &d);

    if (a <= 0 || b <= 0 || c <= 0 || d <= 0) {
        printf("Not a valid quadrilateral\n");
    }
    else {
        if (a == b && b == c && c == d) {
            printf("Square\n");
        }
        else if (a == c && b == d) {
            printf("Rectangle\n");
        }
        else {
            printf("General Quadrilateral\n");
        }
    }	
    return 0; }
```
## 7. ATM Transaction Authentication System (Logical Operators + Nested If)
```c
#include <stdio.h>

int main() {
    int CardNo, CardPin;
    int validCard = 12345;     
    int validPin = 1111;       
    float balance = 10000.0;   
    float amount;

    printf("Enter Card Number: ");
    scanf("%d", &CardNo);

    if (CardNo == validCard) {      

        printf("Enter PIN: ");
        scanf("%d", &CardPin);

        if (CardPin == validPin) {  

            printf("Enter Amount: ");
            scanf("%f", &amount);

            if (amount > 0 && amount <= balance) {  
                balance -= amount;
                printf("Transaction Successful\n");
                printf("Remaining Balance: %.2f\n", balance);
            }
            else {
                printf("Insufficient Funds\n");
            }

        } else {
            printf("Invalid PIN\n");
        }

    } else {
        printf("Invalid Card\n");
    }

    return 0;
}
```
## 8. Advanced Health Calculator (Switch + Nested Conditions + Math Library)
```c
#include <stdio.h>
#include <math.h>

int main() {
    int choice;
    float weight, height, bmi, idealWeight, maxHR, age;
    char gender;

    printf("   Advanced Health Calculator  \n");
    printf("Select Operation:\n");
    printf("1. BMI Calculation\n");
    printf("2. BMR Calculation\n");
    printf("3. Ideal Weight (Devine Formula)\n");
    printf("4. Heart Rate Zone (Percentage of Max HR)\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    switch(choice) {

        case 1: 
            printf("Enter weight (kg): ");
            scanf("%f", &weight);
            printf("Enter height (m): ");
            scanf("%f", &height);

            if (weight <= 0 || height <= 0) {
                printf("Error: Weight and height must be positive.\n");
            } else {
                bmi = weight / pow(height, 2);   
                printf("BMI = %.2f\n", bmi);
            }
            break;

        case 2: 
            printf("Enter weight (kg): ");
            scanf("%f", &weight);
            printf("Enter height (cm): ");
            scanf("%f", &height);
            printf("Enter age (years): ");
            scanf("%f", &age);
            printf("Enter gender (M/F): ");
            scanf(" %c", &gender);

            if (weight <= 0 || height <= 0 || age <= 0) {
                printf("Error: Weight, height, and age must be positive.\n");
            } else {
                if (gender == 'M' || gender == 'm') {
                 
                    float bmr = 10*weight + 6.25*height - 5*age + 5;
                    printf("BMR = %.2f kcal/day\n", bmr);
                } else if (gender == 'F' || gender == 'f') {
                    
                    float bmr = 10*weight + 6.25*height - 5*age - 161;
                    printf("BMR = %.2f kcal/day\n", bmr);
                } else {
                    printf("Invalid gender input.\n");
                }
            }
            break;

        case 3: 
            printf("Enter height (cm): ");
            scanf("%f", &height);
            printf("Enter gender (M/F): ");
            scanf(" %c", &gender);

            if (height <= 0) {
                printf("Error: Height must be positive.\n");
            } else {
                if (gender == 'M' || gender == 'm') {
                    idealWeight = 50 + 0.9*(height - 152);  
                    printf("Ideal Weight = %.2f kg\n", idealWeight);
                } else if (gender == 'F' || gender == 'f') {
                    idealWeight = 45.5 + 0.9*(height - 152); 
                    printf("Ideal Weight = %.2f kg\n", idealWeight);
                } else {
                    printf("Invalid gender input.\n");
                }
            }
            break;

        case 4: 
            printf("Enter age (years): ");
            scanf("%f", &age);

            if (age <= 0) {
                printf("Error: Age must be positive.\n");
            } else {
                maxHR = 220 - age;
                printf("Heart Rate Zones:\n");
                printf("50%% of Max HR = %.0f bpm\n", 0.5 * maxHR);
                printf("60%% of Max HR = %.0f bpm\n", 0.6 * maxHR);
                printf("70%% of Max HR = %.0f bpm\n", 0.7 * maxHR);
                printf("80%% of Max HR = %.0f bpm\n", 0.8 * maxHR);
                printf("90%% of Max HR = %.0f bpm\n", 0.9 * maxHR);
            }
            break;

        default:
            printf("Invalid choice.\n");
    }

    return 0;
}
```
