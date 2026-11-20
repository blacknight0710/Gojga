
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
