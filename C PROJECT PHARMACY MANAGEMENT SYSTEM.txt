```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_MEDICINES 100

// Structure to represent a medicine
struct Medicine {
    int id;
    char name[100];
    float price;
    int quantity;
};

// Global array to store medicines
struct Medicine medicines[MAX_MEDICINES];
int numMedicines = 0;

// Function prototypes
void createMedicine();
void readMedicine();
void updateMedicine();
void deleteMedicine();
void displayMenu();

int main() {
    int choice;

    do {
        displayMenu();
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch(choice) {
            case 1:
                createMedicine();
                break;
            case 2:
                readMedicine();
                break;
            case 3:
                updateMedicine();
                break;
            case 4:
                deleteMedicine();
                break;
            case 0:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while(choice != 0);

    return 0;
}

void displayMenu() {
    printf("\nPharmacy Management System Menu\n");
    printf("1. Create Medicine\n");
    printf("2. Read Medicine\n");
    printf("3. Update Medicine\n");
    printf("4. Delete Medicine\n");
    printf("0. Exit\n");
}

void createMedicine() {
    struct Medicine m;

    printf("\nEnter Medicine ID: ");
    scanf("%d", &m.id);
    printf("Enter Medicine Name: ");
    scanf("%s", m.name);
    printf("Enter Medicine Price: ");
    scanf("%f", &m.price);
    printf("Enter Medicine Quantity: ");
    scanf("%d", &m.quantity);

    medicines[numMedicines++] = m;
    printf("Medicine created successfully.\n");
}

void readMedicine() {
    int id, i;
    printf("\nEnter Medicine ID to read: ");
    scanf("%d", &id);

    for(i = 0; i < numMedicines; i++) {
        if(medicines[i].id == id) {
            printf("Medicine ID: %d\n", medicines[i].id);
            printf("Medicine Name: %s\n", medicines[i].name);
            printf("Medicine Price: %.2f\n", medicines[i].price);
            printf("Medicine Quantity: %d\n", medicines[i].quantity);
            return;
        }
    }

    printf("Medicine with ID %d not found.\n", id);
}

void updateMedicine() {
    int id, i;
    printf("\nEnter Medicine ID to update: ");
    scanf("%d", &id);

    for(i = 0; i < numMedicines; i++) {
        if(medicines[i].id == id) {
            printf("Enter New Medicine Name: ");
            scanf("%s", medicines[i].name);
            printf("Enter New Medicine Price: ");
            scanf("%f", &medicines[i].price);
            printf("Enter New Medicine Quantity: ");
            scanf("%d", &medicines[i].quantity);
            printf("Medicine updated successfully.\n");
            return;
        }
    }

    printf("Medicine with ID %d not found.\n", id);
}

void deleteMedicine() {
    int id, i, found = 0;
    printf("\nEnter Medicine ID to delete: ");
    scanf("%d", &id);

    for(i = 0; i < numMedicines; i++) {
        if(medicines[i].id == id) {
            found = 1;
            for(int j = i; j < numMedicines - 1; j++) {
                medicines[j] = medicines[j + 1];
            }
            numMedicines--;
            printf("Medicine deleted successfully.\n");
            break;
        }
    }

    if(!found)
        printf("Medicine with ID %d not found.\n", id);
}
