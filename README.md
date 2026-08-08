#include <stdio.h>
#include <string.h>

#define MAX_ICECREAMS 100

struct IceCream {
    int id;
    char brand[40];
    char name[50];
    char flavor[30];
    char type[30];
    char size[20];
    char topping[40];
    float price;
    int quantity;
    int sold;
};

struct IceCream icecreams[MAX_ICECREAMS];
int iceCreamCount = 0;


/* Add a new ice cream */
void addIceCream() {

    if (iceCreamCount >= MAX_ICECREAMS) {
        printf("\nIce cream storage is full!\n");
        return;
    }

    printf("\n========== ADD ICE CREAM ==========\n");

    printf("Enter Ice Cream ID: ");
    scanf("%d", &icecreams[iceCreamCount].id);

    printf("Enter Brand: ");
    scanf(" %[^\n]", icecreams[iceCreamCount].brand);

    printf("Enter Ice Cream Name: ");
    scanf(" %[^\n]", icecreams[iceCreamCount].name);

    printf("Enter Flavor: ");
    scanf(" %[^\n]", icecreams[iceCreamCount].flavor);

    printf("Enter Type: ");
    scanf(" %[^\n]", icecreams[iceCreamCount].type);

    printf("Enter Size: ");
    scanf(" %[^\n]", icecreams[iceCreamCount].size);

    printf("Enter Topping: ");
    scanf(" %[^\n]", icecreams[iceCreamCount].topping);

    printf("Enter Price: ");
    scanf("%f", &icecreams[iceCreamCount].price);

    printf("Enter Quantity: ");
    scanf("%d", &icecreams[iceCreamCount].quantity);

    icecreams[iceCreamCount].sold = 0;

    iceCreamCount++;

    printf("\nIce cream added successfully!\n");
}


/* Display one ice cream */
void displayIceCream(struct IceCream i) {

    printf("\n------------------------------------------\n");
    printf("Ice Cream ID : %d\n", i.id);
    printf("Brand        : %s\n", i.brand);
    printf("Name         : %s\n", i.name);
    printf("Flavor       : %s\n", i.flavor);
    printf("Type         : %s\n", i.type);
    printf("Size         : %s\n", i.size);
    printf("Topping      : %s\n", i.topping);
    printf("Price        : %.2f\n", i.price);
    printf("Stock        : %d\n", i.quantity);
    printf("Sold         : %d\n", i.sold);
}


/* Display all ice creams */
void displayIceCreams() {

    int i;

    if (iceCreamCount == 0) {
        printf("\nNo ice cream records available.\n");
        return;
    }

    printf("\n========== ALL ICE CREAMS ==========\n");

    for (i = 0; i < iceCreamCount; i++) {
        displayIceCream(icecreams[i]);
    }
}


/* Search ice cream by ID */
void searchIceCream() {

    int id;
    int i;
    int found = 0;

    printf("\nEnter Ice Cream ID: ");
    scanf("%d", &id);

    for (i = 0; i < iceCreamCount; i++) {

        if (icecreams[i].id == id) {

            printf("\n========== ICE CREAM FOUND ==========\n");
            displayIceCream(icecreams[i]);

            found = 1;
            break;
        }
    }

    if (!found) {
        printf("\nIce cream not found!\n");
    }
}


/* Search by brand */
void searchByBrand() {

    char brand[40];
    int i;
    int found = 0;

    printf("\nEnter Brand: ");
    scanf(" %[^\n]", brand);

    printf("\n========== BRAND SEARCH ==========\n");

    for (i = 0; i < iceCreamCount; i++) {

        if (strcmp(icecreams[i].brand, brand) == 0) {

            displayIceCream(icecreams[i]);
            found = 1;
        }
    }

    if (!found) {
        printf("\nNo ice creams found for this brand.\n");
    }
}


/* Search by flavor */
void searchByFlavor() {

    char flavor[30];
    int i;
    int found = 0;

    printf("\nEnter Flavor: ");
    scanf(" %[^\n]", flavor);

    printf("\n========== FLAVOR SEARCH ==========\n");

    for (i = 0; i < iceCreamCount; i++) {

        if (strcmp(icecreams[i].flavor, flavor) == 0) {

            displayIceCream(icecreams[i]);
            found = 1;
        }
    }

    if (!found) {
        printf("\nNo ice creams found with this flavor.\n");
    }
}


/* Search by type */
void searchByType() {

    char type[30];
    int i;
    int found = 0;

    printf("\nEnter Ice Cream Type: ");
    scanf(" %[^\n]", type);

    printf("\n========== TYPE SEARCH ==========\n");

    for (i = 0; i < iceCreamCount; i++) {

        if (strcmp(icecreams[i].type, type) == 0) {

            displayIceCream(icecreams[i]);
            found = 1;
        }
    }

    if (!found) {
        printf("\nNo ice creams found of this type.\n");
    }
}


/* Search by size */
void searchBySize() {

    char size[20];
    int i;
    int found = 0;

    printf("\nEnter Size: ");
    scanf(" %[^\n]", size);

    printf("\n========== SIZE SEARCH ==========\n");

    for (i = 0; i < iceCreamCount; i++) {

        if (strcmp(icecreams[i].size, size) == 0) {

            displayIceCream(icecreams[i]);
            found = 1;
        }
    }

    if (!found) {
        printf("\nNo ice creams found with this size.\n");
    }
}


/* Search by price range */
void priceRange() {

    float minPrice, maxPrice;
    int i;
    int found = 0;

    printf("\nEnter Minimum Price: ");
    scanf("%f", &minPrice);

    printf("Enter Maximum Price: ");
    scanf("%f", &maxPrice);

    printf("\n========== PRICE RANGE ==========\n");

    for (i = 0; i < iceCreamCount; i++) {

        if (icecreams[i].price >= minPrice &&
            icecreams[i].price <= maxPrice) {

            displayIceCream(icecreams[i]);
            found = 1;
        }
    }

    if (!found) {
        printf("\nNo ice creams found in this price range.\n");
    }
}


/* Find cheapest ice cream */
void cheapestIceCream() {

    int i;
    int cheap;

    if (iceCreamCount == 0) {
        printf("\nNo ice cream records available.\n");
        return;
    }

    cheap = 0;

    for (i = 1; i < iceCreamCount; i++) {

        if (icecreams[i].price < icecreams[cheap].price) {
            cheap = i;
        }
    }

    printf("\n========== CHEAPEST ICE CREAM ==========\n");
    displayIceCream(icecreams[cheap]);
}


/* Find most expensive ice cream */
void expensiveIceCream() {

    int i;
    int expensive;

    if (iceCreamCount == 0) {
        printf("\nNo ice cream records available.\n");
        return;
    }

    expensive = 0;

    for (i = 1; i < iceCreamCount; i++) {

        if (icecreams[i].price > icecreams[expensive].price) {
            expensive = i;
        }
    }

    printf("\n========== MOST EXPENSIVE ICE CREAM ==========\n");
    displayIceCream(icecreams[expensive]);
}


/* Sell ice cream */
void sellIceCream() {

    int id;
    int amount;
    int i;
    int found = 0;

    printf("\nEnter Ice Cream ID: ");
    scanf("%d", &id);

    for (i = 0; i < iceCreamCount; i++) {

        if (icecreams[i].id == id) {

            found = 1;

            printf("Enter Quantity to Sell: ");
            scanf("%d", &amount);

            if (amount <= 0) {
                printf("\nInvalid quantity!\n");
            }
            else if (amount > icecreams[i].quantity) {
                printf("\nInsufficient stock!\n");
            }
            else {

                icecreams[i].quantity -= amount;
                icecreams[i].sold += amount;

                printf("\nSale completed successfully!\n");
                printf("Total Amount: %.2f\n",
                       amount * icecreams[i].price);
            }

            break;
        }
    }

    if (!found) {
        printf("\nIce cream not found!\n");
    }
}


/* Display low-stock ice creams */
void lowStock() {

    int i;
    int found = 0;

    printf("\n========== LOW STOCK ICE CREAMS ==========\n");

    for (i = 0; i < iceCreamCount; i++) {

        if (icecreams[i].quantity <= 5) {

            printf("\nID       : %d", icecreams[i].id);
            printf("\nBrand    : %s", icecreams[i].brand);
            printf("\nName     : %s", icecreams[i].name);
            printf("\nQuantity : %d\n", icecreams[i].quantity);

            found = 1;
        }
    }

    if (!found) {
        printf("\nNo low-stock ice creams found.\n");
    }
}


/* Calculate inventory value */
void inventoryValue() {

    int i;
    float total = 0;

    if (iceCreamCount == 0) {
        printf("\nNo ice cream records available.\n");
        return;
    }

    for (i = 0; i < iceCreamCount; i++) {
        total += icecreams[i].price *
                 icecreams[i].quantity;
    }

    printf("\n========== INVENTORY VALUE ==========\n");
    printf("Total Inventory Value: %.2f\n", total);
}


/* Sales report */
void salesReport() {

    int i;
    int totalSold = 0;
    float totalRevenue = 0;

    printf("\n========== SALES REPORT ==========\n");

    for (i = 0; i < iceCreamCount; i++) {

        totalSold += icecreams[i].sold;

        totalRevenue += icecreams[i].sold *
                        icecreams[i].price;

        printf("\nIce Cream : %s", icecreams[i].name);
        printf("\nBrand     : %s", icecreams[i].brand);
        printf("\nSold      : %d\n", icecreams[i].sold);
    }

    printf("\nTotal Ice Creams Sold : %d\n", totalSold);
    printf("Total Revenue         : %.2f\n", totalRevenue);
}


/* Main function */
int main() {

    int choice;

    printf("================================================\n");
    printf("         ICE CREAM SHOP MANAGEMENT SYSTEM\n");
    printf("================================================\n");

    do {

        printf("\n================ MAIN MENU ================\n");
        printf("1.  Add Ice Cream\n");
        printf("2.  Display All Ice Creams\n");
        printf("3.  Search Ice Cream by ID\n");
        printf("4.  Search by Brand\n");
        printf("5.  Search by Flavor\n");
        printf("6.  Search by Type\n");
        printf("7.  Search by Size\n");
        printf("8.  Search by Price Range\n");
        printf("9.  Find Cheapest Ice Cream\n");
        printf("10. Find Most Expensive Ice Cream\n");
        printf("11. Sell Ice Cream\n");
        printf("12. Display Low Stock\n");
        printf("13. Calculate Inventory Value\n");
        printf("14. Sales Report\n");
        printf("15. Exit\n");
        printf("===========================================\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {

            case 1:
                addIceCream();
                break;

            case 2:
                displayIceCreams();
                break;

            case 3:
                searchIceCream();
                break;

            case 4:
                searchByBrand();
                break;

            case 5:
                searchByFlavor();
                break;

            case 6:
                searchByType();
                break;

            case 7:
                searchBySize();
                break;

            case 8:
                priceRange();
                break;

            case 9:
                cheapestIceCream();
                break;

            case 10:
                expensiveIceCream();
                break;

            case 11:
                sellIceCream();
                break;

            case 12:
                lowStock();
                break;

            case 13:
                inventoryValue();
                break;

            case 14:
                salesReport();
                break;

            case 15:
                printf("\nThank you for using Ice Cream Shop Management System!\n");
                break;

            default:
                printf("\nInvalid choice! Please try again.\n");
        }

    } while (choice != 15);

    return 0;
}
