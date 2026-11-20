333

#include <stdio.h>
#include <stdlib.h>
#include <math.h>

struct Node {
    int coeff, exp;
    struct Node *next;
};

struct Node* create(int n) {
    struct Node *head = NULL, *temp, *new;
    int i;

    for (i = 0; i < n; i++) {
        new = malloc(sizeof(struct Node));

        printf("Enter coefficient and exponent: ");
        scanf("%d%d", &new->coeff, &new->exp);

        new->next = NULL;

        if (head == NULL)
            head = new;
        else {
            temp = head;
            while (temp->next)
                temp = temp->next;

            temp->next = new;
        }
    }
    return head;
}

void display(struct Node *p) {
    while (p) {
        printf("%dx^%d", p->coeff, p->exp);

        if (p->next)
            printf(" + ");

        p = p->next;
    }
    printf("\n");
}

int evaluate(struct Node *p, int x) {
    int sum = 0;

    while (p) {
        sum += p->coeff * pow(x, p->exp);
        p = p->next;
    }
    return sum;
}

int main() {
    struct Node *poly;
    int n, x;

    printf("Enter number of terms: ");
    scanf("%d", &n);

    poly = create(n);

    printf("\nPolynomial: ");
    display(poly);

    printf("Enter value of x: ");
    scanf("%d", &x);

    printf("Value = %d\n", evaluate(poly, x));

    return 0;
}



22

#include <stdio.h>
#include <stdlib.h>

struct Employee {
    int id;
    char name[30], designation[30];
    float basic, allowance, deduction, gross, net;
};

typedef struct Employee *Emp;

void calculate(Emp e) {
    e->gross = e->basic + e->allowance;
    e->net = e->gross - e->deduction;
}

void display(Emp e) {
    printf("\nID: %d\nName: %s\nDesignation: %s",
           e->id, e->name, e->designation);

    printf("\nBasic: %.2f\nAllowance: %.2f\nDeduction: %.2f",
           e->basic, e->allowance, e->deduction);

    printf("\nGross: %.2f\nNet: %.2f\n",
           e->gross, e->net);
}

int main() {
    Emp e;
    int n, i, id, choice;

    printf("Enter number of employees: ");
    scanf("%d", &n);

    e = malloc(n * sizeof(struct Employee));

    for (i = 0; i < n; i++) {
        printf("\nEmployee %d\n", i + 1);

        printf("ID: ");
        scanf("%d", &e[i].id);

        printf("Name: ");
        scanf(" %[^\n]", e[i].name);

        printf("Designation: ");
        scanf(" %[^\n]", e[i].designation);

        printf("Basic Salary: ");
        scanf("%f", &e[i].basic);

        printf("Allowance: ");
        scanf("%f", &e[i].allowance);

        printf("Deduction: ");
        scanf("%f", &e[i].deduction);

        calculate(&e[i]);
    }

    do {
        printf("\n1.Display 2.Search 3.Update 4.Exit\n");
        printf("Choice: ");
        scanf("%d", &choice);

        if (choice == 1) {
            for (i = 0; i < n; i++)
                display(&e[i]);
        }
        else if (choice == 2) {
            printf("Enter ID: ");
            scanf("%d", &id);

            for (i = 0; i < n; i++)
                if (e[i].id == id)
                    display(&e[i]);
        }
        else if (choice == 3) {
            printf("Enter ID: ");
            scanf("%d", &id);

            for (i = 0; i < n; i++) {
                if (e[i].id == id) {
                    printf("New Basic Salary: ");
                    scanf("%f", &e[i].basic);

                    printf("New Allowance: ");
                    scanf("%f", &e[i].allowance);

                    printf("New Deduction: ");
                    scanf("%f", &e[i].deduction);

                    calculate(&e[i]);
                }
            }
        }
    } while (choice != 4);

    free(e);
    return 0;
}

