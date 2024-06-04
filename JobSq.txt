//job sequence
#include <stdio.h>
#include <stdlib.h>


struct Job
{
    int id;        
    int deadline; 
    int profit;   
};

int compare(const void *a, const void *b)
{
    return (((struct Job *)b)->profit - ((struct Job *)a)->profit);
}

void jobSequencing(struct Job arr[], int n)
{
    qsort(arr, n, sizeof(struct Job), compare);

    int maxDeadline = 0, i, j;
    for (i = 0; i < n; ++i)
    {
        if (arr[i].deadline > maxDeadline)
            maxDeadline = arr[i].deadline;
    }

    int *slots = (int *)malloc(maxDeadline * sizeof(int));
    for (i = 0; i < maxDeadline; ++i)
        slots[i] = -1;

    int totalProfit = 0;
    for (i = 0; i < n; ++i)
    {
        for (j = arr[i].deadline - 1; j >= 0; --j)
        {
            if (slots[j] == -1)
            {
                slots[j] = arr[i].id;
                totalProfit += arr[i].profit;
                break;
            }
        }
    }

    printf("Sequence of jobs: ");
    for (i = 0; i < maxDeadline; ++i)
    {
        if (slots[i] != -1)
            printf("%d ", slots[i]);
    }
    printf("\nTotal profit: %d\n", totalProfit);

    free(slots);
}

int main()
{
    int n, i;
    printf("Enter the number of jobs: ");
    scanf("%d", &n);

    struct Job *arr = (struct Job *)malloc(n * sizeof(struct Job));

    printf("Enter job details (ID Deadline Profit):\n");
    for (i = 0; i < n; ++i)
    {
        printf("Job %d: \n", i + 1);
        scanf("%d %d %d", &arr[i].id, &arr[i].deadline, &arr[i].profit);
    }

    printf("\nGiven jobs:\n");
    printf("ID\tDeadline\tProfit\n");
    for (i = 0; i < n; ++i)
        printf("%d\t%d\t\t%d\n", arr[i].id, arr[i].deadline, arr[i].profit);

    printf("\nJob sequence and maximum profit:\n");
    jobSequencing(arr, n);

    free(arr);

    return 0;
}
