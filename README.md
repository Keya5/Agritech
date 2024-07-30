# Agritech
#include <stdio.h>

#define MAX_CROPS 100

typedef struct {
    char name[50];
    float health; // Health percentage (0-100)
    float yield;  // Yield in tons per hectare
} Crop;

void inputCropData(Crop *crop) {
    printf("Enter crop name: ");
    scanf("%s", crop->name);
    printf("Enter crop health (0-100): ");
    scanf("%f", &crop->health);
    printf("Enter crop yield (tons per hectare): ");
    scanf("%f", &crop->yield);
}

void displayCropData(Crop crop) {
    printf("Crop Name: %s\n", crop.name);
    printf("Health: %.2f%%\n", crop.health);
    printf("Yield: %.2f tons/ha\n", crop.yield);
}

float calculateAverageYield(Crop crops[], int count) {
    float totalYield = 0.0;
    for (int i = 0; i < count; i++) {
        totalYield += crops[i].yield;
    }
    return (count > 0) ? (totalYield / count) : 0.0;
}

int main() {
    Crop crops[MAX_CROPS];
    int cropCount = 0;
    char choice;

    do {
        if (cropCount < MAX_CROPS) {
            inputCropData(&crops[cropCount]);
            cropCount++;
        } else {
            printf("Maximum crop limit reached.\n");
            break;
        }

        printf("Do you want to add another crop? (y/n): ");
        scanf(" %c", &choice);
    } while (choice == 'y' || choice == 'Y');

    printf("\n--- Crop Data ---\n");
    for (int i = 0; i < cropCount; i++) {
        displayCropData(crops[i]);
    }

    float averageYield = calculateAverageYield(crops, cropCount);
    printf("Average Yield: %.2f tons/ha\n", averageYield);

    return 0;
}
