# ca question 2
Write a multithreaded program that calculates various statistical values for a list of numbers. This program will be passed a series of numbers on the command line and will then create three separate worker threads. One thread will determine the average of the numbers, the second will determine the maximum value, and the third will determine the minimum value. For example, suppose your program is passed the integers
90 81 78 95 79 72 85
The program will report The average value is 82 The minimum value is 72 The maximum value is 95
The variables representing the average, minimum, and maximum values will be stored globally. The worker threads will set these values, and the parent thread will output the values once the workers have exited.




#include<stdio.h>
#include<pthread.h>
int arr[50],n,i;

void *th()
{
	int sum=0;
	float average;
	printf("enter your number :=");
	scanf("%d",&n);
	for(i=0;i<n;i++)
	{
		scanf("%d",&arr[i]);
	}
	for(i=0;i<n;i++)
		{
			sum=sum+arr[i];
		}
	average=sum/n;
	printf("The average value is:%f",average);
}
void *th1()
{


	int temp=arr[0];
	for(int i=1;i<n;i++)
		{
			if(temp>arr[i])
			{
			temp=arr[i];
			}
		}
	printf("\nThe Minimum  value is:=%d",temp);

}
void *th2()
{

	int temp=arr[0];
	for(int i=1;i<n;i++)
		{
			if(temp<arr[i])
			{
			temp=arr[i];
			}
		}
	printf("\nThe Maximum  value is:=%d",temp);
	}
int main()
{
int n,i;
pthread_t t1;
pthread_t t2;
pthread_t t3;
	n=pthread_create(&t1,NULL,&th,NULL);
	pthread_join(t1,NULL);
	//printf("\n done and my value is %d",n);
	n=pthread_create(&t2,NULL,&th1,NULL);
        pthread_join(t2,NULL);
	//printf("\n done and my value is %d",n);
	n=pthread_create(&t3,NULL,&th2,NULL);
        pthread_join(t3,NULL);
	//printf("\n done and my value is %d",n);

}
