//Binary Search Array
#include<stdio.h>
int main(){
    int arr[]={1,15,26,29,31,35,39,87,104,114};
    int value,low,high,mid;
    low=0;
    value=104;
    high=((sizeof(arr)/sizeof(arr[0]))-1);
    mid=(low+high)/2;
    while(low<=high){
        if(arr[mid]==value){
            printf("%d",mid);
        }
        if(value>arr[mid]){
            low=mid;
        }
        else{
            high=mid;
        }
        mid=(low+high)/2;

    }
    

}