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


v) Merge overlapping subintervals

#include<bits/stdc++.h> 
using namespace std; 

// An interval has start time and end time 
struct Interval 
{ 
	int start, end; 
}; 

// Compares two intervals according to their staring time. 
// This is needed for sorting the intervals using library 
// function std::sort(). See http://goo.gl/iGspV 
bool compareInterval(Interval i1, Interval i2) 
{ 
	return (i1.start < i2.start); 
} 

// The main function that takes a set of intervals, merges 
// overlapping intervals and prints the result 
void mergeIntervals(Interval arr[], int n) 
{ 
	// Test if the given set has at least one interval 
	if (n <= 0) 
		return; 

	// Create an empty stack of intervals 
	stack<Interval> s; 

	// sort the intervals in increasing order of start time 
	sort(arr, arr+n, compareInterval); 

	// push the first interval to stack 
	s.push(arr[0]); 

	// Start from the next interval and merge if necessary 
	for (int i = 1 ; i < n; i++) 
	{ 
		// get interval from stack top 
		Interval top = s.top(); 

		// if current interval is not overlapping with stack top, 
		// push it to the stack 
		if (top.end < arr[i].start) 
			s.push(arr[i]); 

		// Otherwise update the ending time of top if ending of current 
		// interval is more 
		else if (top.end < arr[i].end) 
		{ 
			top.end = arr[i].end; 
			s.pop(); 
			s.push(top); 
		} 
	} 

	// Print contents of stack 
	cout << "\n The Merged Intervals are: "; 
	while (!s.empty()) 
	{ 
		Interval t = s.top(); 
		cout << "[" << t.start << "," << t.end << "] "; 
		s.pop(); 
	} 
	return; 
} 

// Driver program 
int main() 
{ 
	Interval arr[] = { {6,8}, {1,9}, {2,4}, {4,7} }; 
	int n = sizeof(arr)/sizeof(arr[0]); 
	mergeIntervals(arr, n); 
	return 0; 
} 


vi) Pascals triangle


// A O(n^2) time and O(1) extra space 
#include <bits/stdc++.h> 

using namespace std; 
void printPascal(int n) 
{ 
	
for (int line = 1; line <= n; line++) 
{ 
	int C = 1; // used to represent C(line, i) 
	for (int i = 1; i <= line; i++) 
	{ 
		
		// The first value in a line is always 1 
		cout<< C<<" "; 
		C = C * (line - i) / i; 
	} 
	cout<<"\n"; 
} 
} 

// Driver code 
int main() 
{ 
	int n = 5; 
	printPascal(n); 
	return 0; 
} 
