//All Sorting
#include<stdio.h>
int arr[100];
int size=0;
void createarr(int arr[]);
void swap(int *a,int *b);
void bubblesort(int arr[]);
void display(int arr[]);
void selectionsort(int arr[]);
void insertionsort(int arr[]);

int main(){
    printf("Create Array\n");
    createarr(arr);
    printf("Array after bubble sort\n");
    bubblesort(arr);
    display(arr);
    printf("Array after selection sort\n");
    selectionsort(arr);
    display(arr);
    printf("Array after insertion sort\n");
    insertionsort(arr);
    display(arr);
}
void createarr(int arr[]){
    int value;
    printf("Enter -1 to end\n");
    printf("Enter a number\n");
    scanf("%d",&value);
    while (value!=-1)
    {
        arr[size]=value;
        size++;

        printf("Enter a number\n");
        scanf("%d",&value);
    }
    for(int i=0;i<size;i++)
        printf("%d ",arr[i]);
    printf("\n");
    
}
//FUNCTION FOR SORTING
void swap(int *a,int *b){
    int temp;
    temp=*a;
    *a=*b;
    *b=temp;
}
//BUBBLE SORT
void bubblesort(int arr[]){ 
    int i,j;
    for(i=0;i<size-1;i++){
        for(j=0;j<size-i-1;j++){
            if(arr[j]>arr[j+1]){
                swap(&arr[j],&arr[j+1]);
            }
        }
    }
}
//SELECTION SORT
void selectionsort(int arr[]){
    int i,j,min_idx;
    for(i=0;i<size;i++){
        min_idx=i;
        for(j=i+1;j<size;j++){
            if(arr[j]<arr[min_idx]){
                min_idx=j;
            }
        }
        swap(&arr[i],&arr[min_idx]);
    }
}
//INSERTION SORT
void insertionsort(int arr[]){
    int i,j;
    for(i=1;i<size;i++){
        for(j=i;j>0;j--){
            if(arr[j]<arr[j-1]){
                swap(&arr[j],&arr[j-1]);
            }
        }
    }
}
void display(int arr[]){
    int i;
    for(int i=0;i<size;i++)
        printf("%d ",arr[i]);
    printf("\n");
}

