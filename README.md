# Interview-practice-questions
collection of all type of interview questions 

1) Array-
i)Find the duplicate in an array of N integers.

#include <bits/stdc++.h>
using namespace std;

int main()
{
int N;
cin>>N;
int numRay[N];
for(int i=0;i<N;i++){
cin>>numRay[i];
}
for (int i = 0; i < N; i++)
{
numRay[numRay[i] % N] = numRay[numRay[i] % N] + N;
}
cout << "The repeating elements are : " << endl;
for (int i = 0; i < N; i++)
{
if (numRay[i] >= N*2)
{
cout << i << " " << endl;
}
}
return 0;
}



ii) Sort an array of 0's 1's 2's without using extra space or sorting algo.

#include <bits/stdc++.h>
using namespace std;

// Utility function to print the contents of an array
void printArr(int arr[], int n)
{
	for (int i = 0; i < n; i++)
		cout << arr[i] << " ";
}

// Function to sort the array of 0s, 1s and 2s
void sortArr(int arr[], int n)
{
	int i, cnt0 = 0, cnt1 = 0, cnt2 = 0;

	// Count the number of 0s, 1s and 2s in the array
	for (i = 0; i < n; i++) {
		switch (arr[i]) {
		case 0:
			cnt0++;
			break;
		case 1:
			cnt1++;
			break;
		case 2:
			cnt2++;
			break;
		}
	}

	// Update the array
	i = 0;

	// Store all the 0s in the beginning
	while (cnt0 > 0) {
		arr[i++] = 0;
		cnt0--;
	}

	// Then all the 1s
	while (cnt1 > 0) {
		arr[i++] = 1;
		cnt1--;
	}

	// Finally all the 2s
	while (cnt2 > 0) {
		arr[i++] = 2;
		cnt2--;
	}

	// Print the sorted array
	printArr(arr, n);
}

// Driver code
int main()
{
    int n,i;
    cin>>n;
	int arr[n];
	for(i=0;i<n;i++){
        cin>>arr[i];
	}
	sortArr(arr, n);

	return 0;
}



iii)Find Repeating and Missing element in an array.

#include <bits/stdc++.h>
using namespace std;

void printTwoElements(int arr[], int size)
{
	int i;
	cout << "The repeating element is/are ";

	for (i = 0; i < size; i++) {
		if (arr[abs(arr[i]) - 1] > 0)
			arr[abs(arr[i]) - 1] = -arr[abs(arr[i]) - 1];
		else
			cout << abs(arr[i]) << " ";
	}

	cout <<endl<< "missing element is/are ";
	for (i = 0; i < size; i++) {
		if (arr[i] > 0)
			cout << (i + 1)<<" ";
	}
}

/* Driver code */
int main()
{
    int n,i;
    cin>>n;
	int arr[n];
	for(i=0;i<n;i++){
        cin>>arr[i];
	}
	printTwoElements(arr, n);
}


iv) Kadane's algorithm

#include<iostream>
#include<climits>
using namespace std;

int maxSubArraySum(int a[], int size)
{
int max_so_far = 0, max_ending_here = 0;
for (int i = 0; i < size; i++)
{
	max_ending_here = max_ending_here + a[i];
	if (max_ending_here < 0)
		max_ending_here = 0;

	/* Do not compare for all elements. Compare only
		when max_ending_here > 0 */
	else if (max_so_far < max_ending_here)
		max_so_far = max_ending_here;
}
return max_so_far;
}

int main()
{
    int n;
    cin>>n;
	int a[n];
	for(int i=0;i<n;i++){
        cin>>a[i];
	}
	int max_sum = maxSubArraySum(a, n);
	cout << "Maximum contiguous sum is " << max_sum;
	return 0;
}

