# stacks.c
#include <stdio.h>
#include <stdlib.h>

typedef struct node{
    char data;
    struct node* next;

}node;
typedef struct stack{
    node* top;
}stack;

void inistack(stack*s){
    s-> top = NULL;
}
int isempty(stack *s){
    return s-> top == NULL;


}

void push(stack*s ,char value){
    node*newnode = malloc(sizeof(node));
    newnode ->data = value;
    newnode ->next = s->top;
    s->top = newnode;
}
char pop(stack *s ){
    if(isempty(s)){
            printf("stack is empty");
        return '\0';
    }
    node* temp = s->top;
    char value = temp->data;
    s->top = temp->next;
    free(temp);
    return value;
}

char peek(stack* s){
    if(isempty(s)){
        printf("stack is empty");

        return '\0';}

return s->top->data;
}

int function(char phrase[]){
    stack s;
    int i = 0;
    while(phrase[i]!= '\0'){
        char m = phrase[i];
        if(m!= '+' && m!= '-' && m!= '*' && m!= '/'  ){
            push(&s,m- '0');
        }
        else{
            int a = pop(&s);
            int b = pop(&s);

            int result= 0;

        switch (m){
            case '+':
                result = a + b;
                break;
             case '*':
                result = a * b;
                break;
             case '/':
                result = a / b;
                break;
             case '-':
                result = a - b;
                break;
        }
        push(&s,result);
    }
    i++;

}return pop(&s);}

void display(stack* s){
    if(isempty(s)){
        printf("stack is empty");
        return;
    }node*temp = s->top;
    printf("stack's elements are = ");
    while(temp!= NULL){
        printf("%c",temp->data);
        temp = temp ->next;
    }printf("\n");
}
void menu(stack *s){
    int choice;
    char var;
    char phrase[100];

    do{
        printf("\nENTER 1 FOR PUSH\n");
        printf("ENTER 2 FOR POP\n");
        printf("ENTER 3 FOR DISPLAYING THE ELEMENTS \n");
        printf("ENTER 4 FOR EVALUATE A POSTIF EXERPESTION \n");
        printf("ENTER 5 FOR EXIT\n");
        printf("ENTER UR CHOICE = !");
        scanf("%d",&choice);

        switch(choice){
            case 1 :
                printf("enter a character to push: ");
                scanf(" %c",&var);
                push(s,var);
                break;
            case 2 :
                var = pop(s);
                printf("you popped the element = %C",var);
                break;
            case 3 :
                display(s);
                break;
            case 4 :
                 printf("enter the operation");
                scanf("%s",phrase);
                printf("%d",function(phrase));

                break;
            case 5 :
                printf("ur out..!");
                break;
        }
    }while (choice != 5);

}

int main()
{

    stack s;
    char phrase[100];

    menu(&s);
   // printf("Hello world!\n");
    return 0;
}