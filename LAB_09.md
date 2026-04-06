## SECTION A — FUNCTIONS
### Q1 Hospital Emergency Room — Patient Triage Score
```c
#include <stdio.h>
float triageScore(int severity, int age, int vitals)
{
    return (severity * 0.5) + (age * 0.3) + (vitals * 0.2);
}
int main()
{
    int severity, age, vitals;
    float score;

    printf("Enter severity, age risk, vitals: ");
    scanf("%d %d %d", &severity, &age, &vitals);

    score = triageScore(severity, age, vitals);
    printf("Triage Score : %.2f\n", score);

    if(score > 7.0)
        printf("Immediate attention required\n");
    else if(score >= 4.0)
        printf("Moderate priority\n");
    else
        printf("Can wait\n");

    return 0;
}
```
### Q2 Online Retail Store — Discount and Invoice Generator
```c
#include <stdio.h>
float applyDiscount(float price, int tier)
{
    float discount = 0;
    if(tier == 1)        
        discount = price * 0.05;
    else if(tier == 2)   
        discount = price * 0.10;
    else if(tier == 3)   
        discount = price * 0.20;
    else if(tier == 4)   
        discount = price * 0.30;
    return price - discount;
}

void printInvoice(float original, float discounted)
{
    float discountAmount = original - discounted;
    float delivery = 0;
    if(discounted < 2000)
        delivery = 150;

    float finalTotal = discounted + delivery;

    printf("\n----- INVOICE -----\n");
    printf("Original Price: Rs. %.2f\n", original);
    printf("Discount: Rs. %.2f\n", discountAmount);
    printf("Price after Discount: Rs. %.2f\n", discounted);

    if(delivery > 0)
        printf("Delivery Charges: Rs. %.2f\n", delivery);
    else
        printf("Delivery Charges: FREE\n");
    printf("Final Total: Rs. %.2f\n", finalTotal);
}

int main()
{
    float price, discountedPrice;
    int tier;
    printf("Enter original price: ");
    scanf("%f", &price);

    printf("Enter membership tier (1-Bronze, 2-Silver, 3-Gold, 4-Platinum): ");
    scanf("%d", &tier);

    discountedPrice = applyDiscount(price, tier);
    printInvoice(price, discountedPrice);

    return 0;
}
```
### Q3 Cricket Analytics App — Batting Performance Evaluator
```c
#include <stdio.h>

int totalRuns(int arr[], int n)
{
    int sum = 0;
    for(int i=0; i<n; i++)
        sum += arr[i];
    return sum;
}
int highestScore(int arr[], int n)
{
    int max = arr[0];
    for(int i=1; i<n; i++)
        if(arr[i] > max)
            max = arr[i];
    return max;
}
int aboveAverage(int arr[], int n, float avg)
{
    int count = 0;
    for(int i=0; i<n; i++)
        if(arr[i] > avg)
            count++;
    return count;
}
int main()
{
    int arr[10];
    int total, max, count;
    float avg;

    printf("Enter 10 match scores:\n");
    for(int i=0; i<10; i++)
        scanf("%d", &arr[i]);

    total = totalRuns(arr, 10);
    avg = (float)total / 10;
    max = highestScore(arr, 10);
    count = aboveAverage(arr, 10, avg);

    printf("\nTotal Runs: %d\n", total);
    printf("Average: %.2f\n", avg);
    printf("Highest Score: %d\n", max);
    printf("Matches above average: %d\n", count);

    return 0;
}
```
### Q4 Smart ATM — Secure PIN Validation System
```c
#include <stdio.h>
int validatePIN(int storedPIN, int enteredPIN)
{
     if(storedPIN == enteredPIN)
        return 1;
    else
        return 0;
}
int main()
{
    int storedPIN = 4729;
    int entered;
    for(int i=1; i<=3; i++)
    {
        printf("Enter PIN: ");
        scanf("%d", &entered);
        if(validatePIN(storedPIN, entered))
        {
            printf("Access granted. Welcome!\n");
            break;
        }
        else
        {
            printf("Incorrect PIN. Attempts left: %d\n", 3 - i);
        }
        if(i == 3)
            printf("Card blocked. Contact your bank.\n");
    }

    return 0;
}
```
### Q5 Power Plant Monitor — Unit Conversion Pipeline
```c
#include <stdio.h>

float toMegajoules(float kwh) { return kwh * 3.6; }
float toBTU(float kwh) { return kwh * 3412.14; }
float toCalories(float kwh) { return kwh * 859845; }
int main()
{
    float kwh;
    printf("Enter energy in kWh: ");
    scanf("%f", &kwh);
    printf("Megajoules (MJ): %.2f\n", toMegajoules(kwh));
    printf("BTU: %.2f\n", toBTU(kwh));

    printf("Calories (kcal): %.2f\n", toCalories(kwh));
    printf("\n(Using function call chaining)\n");
    printf("MJ directly: %.2f\n", toMegajoules(kwh));
    return 0;
}
```
### Q6 Restaurant Billing — Multi-Table Revenue Summary
```c
#include <stdio.h>
float totalRevenue(float bills[], int n)
{
    float sum = 0;
    for(int i=0; i<n; i++)
        sum += bills[i];
    return sum;
}
int bestTable(float bills[], int n)
{
    int maxIdx = 0;
    for(int i=1; i<n; i++)
        if(bills[i] > bills[maxIdx])
            maxIdx = i;
    return maxIdx;
}
int isProfitable(float total)
{
    return total > 10000;
}
int main()
{
    float bills[5];
    float total;
    int best;

    printf("Enter 5 table bills: ");
    for(int i=0; i<5; i++)
        scanf("%f", &bills[i]);

    total = totalRevenue(bills, 5);
    best = bestTable(bills, 5);

    printf("\nTotal Revenue: %.2f\n", total);
    printf("Best Table: %d\n", best + 1);

    if(isProfitable(total))
        printf("Profitable night\n");
    else
        printf("Not profitable\n");

    return 0;
}
```
## SECTION B — POINTERS

### Q7 Exam Results System — In-Place Grade Scaling
```c
#include <stdio.h>
int main()
{
    int arr[6] = {40, 55, 60, 30, 50, 45};
    int *p = arr;
    int highest = *p;

    printf("Original:\n");
    for(int i=0; i<6; i++)
        printf("%d ", *(p+i));

    for(int i=1; i<6; i++)
        if(*(p+i) > highest)
            highest = *(p+i);

    for(int i=0; i<6; i++)
        *(p+i) = (int)(((float)*(p+i)/highest)*100);
    printf("\nScaled:\n");
    for(int i=0; i<6; i++)
        printf("%d ", *(p+i));
    return 0;
}
```
### Q8 IoT Sensor Hub — Multi-Type Data Logger
```c
#include <stdio.h>
    
    int main()
    {
        void *sensor;
        int vibrations = 847;
        sensor = &vibrations;
        printf("Vibration: %d Address: %p\n", *(int*)sensor, (void*)sensor);
    
        float temp = 73.6;
        sensor = &temp;
        printf("Temperature: %.2f Address: %p\n", *(float*)sensor, (void*)sensor);
    
        char status = 'W';
        sensor = &status;
        printf("Status: %c Address: %p\n", *(char*)sensor, (void*)sensor);
    
        if(*(char*)sensor == 'N')
            printf("Normal\n");
        else if(*(char*)sensor == 'W')
            printf("Warning\n");
        else
            printf("Critical Alert!\n");
    
        return 0;
    }
```
### Q9 School Attendance System — Weekly 2D Record Traversal
```c
#include <stdio.h>
int main()
{
    int attendance[4][5] = {
        {1,1,0,1,1},
        {0,1,0,1,0},
        {1,1,1,1,1},
        {0,0,1,0,1}
    };
    int (*p)[5] = attendance;
    for(int i=0; i<4; i++)
    {
        int total = 0;
        printf("Student %d: ", i+1);
        for(int j=0; j<5; j++)
        {
            printf("%d ", (*(p+i))[j]);
            total += (*(p+i))[j];
        }
        printf("Total = %d", total);

        if(total < 3)
            printf(" (At risk)");

        printf("\n");
    }
    return 0;
}
```
### Q10 Game Engine — Runtime Combat Action Dispatcher
```c
#include <stdio.h>
int basicAttack(int dmg, int hp)
{
    return hp - dmg;
}

int powerStrike(int dmg, int hp)
{
    return hp - (int)(dmg * 2.5);
}
int heal(int dmg, int hp)
{
    return hp + 20;
}
int poisonAttack(int dmg, int hp)
{
    return hp - (dmg / 2);
}
int main()
{
    int hp = 100, dmg = 25, choice;
    int (*action)(int, int);  

    for(int turn = 1; turn <= 3; turn++)
    {
        printf("\nTurn %d — Current HP: %d\n", turn, hp);

        printf("1. Basic Attack\n");
        printf("2. Power Strike\n");
        printf("3. Heal\n");
        printf("4. Poison Attack\n");

        do {
            printf("Enter choice (1-4): ");
            scanf("%d", &choice);
        } while(choice < 1 || choice > 4);  
        switch(choice)
        {
            case 1: action = basicAttack; break;
            case 2: action = powerStrike; break;
            case 3: action = heal; break;
            case 4: action = poisonAttack; break;
        }
        
        hp = action(dmg, hp);
        if(hp < 0) hp = 0;
        if(hp > 100) hp = 100;
        
        if(choice == 1)
            printf("Basic Attack used!\n");
        else if(choice == 2)
            printf("Power Strike used!\n");
        else if(choice == 3)
            printf("Heal used!\n");
        else
            printf("Poison Attack used!\n");
        printf("HP after action: %d\n", hp);
    }
    printf("\nCombat ended. Final HP: %d\n", hp);
    return 0;
}
```
