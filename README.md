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

vii) Inversion of array(using merge sort)
 
#include <bits/stdc++.h> 
using namespace std; 

int _mergeSort(int arr[], int temp[], int left, int right); 
int merge(int arr[], int temp[], int left, int mid, int right); 

/* This function sorts the input array and returns the 
number of inversions in the array */
int mergeSort(int arr[], int array_size) 
{ 
	int temp[array_size]; 
	return _mergeSort(arr, temp, 0, array_size - 1); 
} 

/* An auxiliary recursive function that sorts the input array and 
returns the number of inversions in the array. */
int _mergeSort(int arr[], int temp[], int left, int right) 
{ 
	int mid, inv_count = 0; 
	if (right > left) { 
		/* Divide the array into two parts and 
		call _mergeSortAndCountInv() 
		for each of the parts */
		mid = (right + left) / 2; 

		/* Inversion count will be sum of 
		inversions in left-part, right-part 
		and number of inversions in merging */
		inv_count += _mergeSort(arr, temp, left, mid); 
		inv_count += _mergeSort(arr, temp, mid + 1, right); 

		/*Merge the two parts*/
		inv_count += merge(arr, temp, left, mid + 1, right); 
	} 
	return inv_count; 
} 

/* This funt merges two sorted arrays 
and returns inversion count in the arrays.*/
int merge(int arr[], int temp[], int left, 
		int mid, int right) 
{ 
	int i, j, k; 
	int inv_count = 0; 

	i = left; /* i is index for left subarray*/
	j = mid; /* j is index for right subarray*/
	k = left; /* k is index for resultant merged subarray*/
	while ((i <= mid - 1) && (j <= right)) { 
		if (arr[i] <= arr[j]) { 
			temp[k++] = arr[i++]; 
		} 
		else { 
			temp[k++] = arr[j++]; 

			/* this is tricky -- see above 
			explanation/diagram for merge()*/
			inv_count = inv_count + (mid - i); 
		} 
	} 

	/* Copy the remaining elements of left subarray 
(if there are any) to temp*/
	while (i <= mid - 1) 
		temp[k++] = arr[i++]; 

	/* Copy the remaining elements of right subarray 
(if there are any) to temp*/
	while (j <= right) 
		temp[k++] = arr[j++]; 

	/*Copy back the merged elements to original array*/
	for (i = left; i <= right; i++) 
		arr[i] = temp[i]; 

	return inv_count; 
} 

int main() 
{ 
    int n,i;
    cin>>n;
	int arr[n]; 
	for(i=0;i<n;i++){
	    cin>>arr[i];
	}
	int ans = mergeSort(arr, n); 
	cout << " Number of inversions are " << ans; 
	return 0; 
}

viii) Stock buy and sell 

#include <bits/stdc++.h> 
using namespace std; 

// This function finds the buy sell 
// schedule for maximum profit 
void stockBuySell(int price[], int n) 
{ 
	// Prices must be given for at least two days 
	if (n == 1) 
		return; 

	// Traverse through given price array 
	int i = 0; 
	while (i < n - 1) { 

		// Find Local Minima 
		// Note that the limit is (n-2) as we are 
		// comparing present element to the next element 
		while ((i < n - 1) && (price[i + 1] <= price[i])) 
			i++; 

		// If we reached the end, break 
		// as no further solution possible 
		if (i == n - 1) 
			break; 

		// Store the index of minima 
		int buy = i++; 

		// Find Local Maxima 
		// Note that the limit is (n-1) as we are 
		// comparing to previous element 
		while ((i < n) && (price[i] >= price[i - 1])) 
			i++; 

		// Store the index of maxima 
		int sell = i - 1; 

		cout << "Buy on day: " << buy 
			<< "\t Sell on day: " << sell << endl; 
	} 
} 

// Driver code 
int main() 
{ 
	// Stock prices on consecutive days 
	int price[] = { 100, 180, 260, 310, 40, 535, 695 }; 
	int n = sizeof(price) / sizeof(price[0]); 

	// Fucntion call 
	stockBuySell(price, n); 

	return 0; 
}

ix) Rotation of matrix clockwise

#include <bits/stdc++.h> 
using namespace std; 

#define N 4 

// Function to rotate the matrix 90 degree clockwise 
void rotate90Clockwise(int a[N][N]) 
{ 

	// Traverse each cycle 
	for (int i = 0; i < N / 2; i++) { 
		for (int j = i; j < N - i - 1; j++) { 

			// Swap elements of each cycle 
			// in clockwise direction 
			int temp = a[i][j]; 
			a[i][j] = a[N - 1 - j][i]; 
			a[N - 1 - j][i] = a[N - 1 - i][N - 1 - j]; 
			a[N - 1 - i][N - 1 - j] = a[j][N - 1 - i]; 
			a[j][N - 1 - i] = temp; 
		} 
	} 
} 

// Function for print matrix 
void printMatrix(int arr[N][N]) 
{ 
	for (int i = 0; i < N; i++) { 
		for (int j = 0; j < N; j++) 
			cout << arr[i][j] << " "; 
		cout << '\n'; 
	} 
} 
 
int main() 
{ 
	int arr[N][N] = { { 1, 2, 3, 4 }, 
					{ 5, 6, 7, 8 }, 
					{ 9, 10, 11, 12 }, 
					{ 13, 14, 15, 16 } }; 
	rotate90Clockwise(arr); 
	printMatrix(arr); 
	return 0; 
} 


2) MATHS

i) Excel column number
 
#include <bits/stdc++.h> 

using namespace std; 

// Returns result when we pass title. 
int titleToNumber(string s) 
{ 
	// This process is similar to 
	// binary-to-decimal conversion 
	int result = 0; 
	for (const auto& c : s) 
	{ 
		result *= 26; 
		result += c - 'A' + 1; 
	} 

	return result; 
} 

int main() 
{
    string s;
    cin>>s;
	cout << titleToNumber(s) << endl; 
	return 0; 
} 

ii) x^n in O(logn)

#include<iostream> 
using namespace std; 
class gfg 
{ 
	
/* Function to calculate x raised to the power n */
public: 
int power(int x, unsigned int n) 
{ 
	int temp; 
	if( n == 0) 
		return 1; 
	temp = power(x, n/2); 
	if (n%2 == 0) 
		return temp*temp; 
	else
		return x*temp*temp; 
} 
};

int main() 
{ 
	gfg g; 
	int x; 
	unsigned int n; 
	cin>>x>>n;
	cout << g.power(x, n); 
	return 0; 
} 

iii) count number of trailing zeroes in factorial of a no.


#include <iostream> 
using namespace std; 

// Function to return trailing 
// 0s in factorial of n 
int findTrailingZeros(int n) 
{ 
	// Initialize result 
	int count = 0; 

	// Keep dividing n by powers of 
	// 5 and update count 
	for (int i = 5; n / i >= 1; i *= 5) 
		count += n / i; 

	return count; 
} 
 
int main() 
{ 
	int n;
	cin>>n;
	cout << "Count of trailing 0s in " << n 
		<< "! is " << findTrailingZeros(n); 
	return 0; 
} 

iv) gcd in O(logn)

#include <bits/stdc++.h> 
using namespace std; 

// Function to return 
// gcd of a and b 
int gcd(int a, int b) 
{ 
	if (a == 0) 
		return b; 
	return gcd(b % a, a); 
} 

int main() 
{ 
	int a , b;
	cin>>a>>b;
	cout << "GCD(" << a << ", "
		<< b << ") = " << gcd(a, b) 
						<< endl; 
	
	return 0; 
}

v) Grid unique path

#include <iostream> 
using namespace std; 

// Returns count of possible paths to reach cell at 
// row number m and column number n from the topmost 
// leftmost cell (cell at 1, 1) 
int numberOfPaths(int m, int n) 
{ 
	// Create a 2D table to store results of subproblems 
	int count[m][n]; 

	// Count of paths to reach any cell in first column is 1 
	for (int i = 0; i < m; i++) 
		count[i][0] = 1; 

	// Count of paths to reach any cell in first row is 1 
	for (int j = 0; j < n; j++) 
		count[0][j] = 1; 

	// Calculate count of paths for other cells in 
	// bottom-up manner using the recursive solution 
	for (int i = 1; i < m; i++) { 
		for (int j = 1; j < n; j++) 

			// By uncommenting the last part the code calculatest he total 
			// possible paths if the diagonal Movements are allowed 
			count[i][j] = count[i - 1][j] + count[i][j - 1]; //+ count[i-1][j-1]; 
	} 
	return count[m - 1][n - 1]; 
} 

int main() 
{ 
	cout << numberOfPaths(3, 3); 
	return 0; 
} 


3) Hashing

i) Two sum problem

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int,int> m;
        vector<int> v;
        for(int i=0;i<nums.size();i++)
        {
            if(m.find(target-nums[i])!=m.end())
            {
                v.push_back(m[target-nums[i]]);
                v.push_back(i);
                return v;
            }
            m[nums[i]]=i;
        }
        return v;
    }
};

ii) 4 sum problem

#include <iostream>
#include <unordered_map>
#include <vector>
using namespace std;

typedef pair<int, int> Pair;

// Function to check if Quadruplet exists in an array with given sum
bool quadTuple(int arr[], int n, int sum)
{
	// create an empty map
	// key -> sum of a pair of elements in the array
	// value -> vector storing index of every pair having that sum
	unordered_map<int, vector<Pair>> map;

	// consider each element except last element
	for (int i = 0; i < n - 1; i++)
	{
		// start from i'th element till last element
		for (int j = i + 1; j < n; j++)
		{
			// calculate remaining sum
			int val = sum - (arr[i] + arr[j]);

			// if remaining sum is found in the map,
			// we have found a Quadruplet
			if (map.find(val) != map.end())
			{
				// check every pair having sum equal to remaining sum
				for (auto pair : map.find(val)->second)
				{
					int x = pair.first;
					int y = pair.second;

					// if Quadruplet don't overlap, print it and return true
					if ((x != i && x != j) && (y != i && y != j))
					{
						cout << "Quadruplet Found ("
							 << arr[i] << ", " << arr[j] << ", " << arr[x]
							 << ", " << arr[y] << ")";
						return true;
					}
				}
			}

			// insert current pair into the map
			map[arr[i] + arr[j]].push_back({i, j});
		}
	}

	// return false if Quadruplet don't exist
	return false;
}

int main()
{
        int n,sum;
	cin>>n;
	int arr[n];
	for(int i=0;i<n;i++){
	cin>>arr[i];
	}
	cin>>sum;
	if (!quadTuple(arr, n, sum))
		cout << "Quadruplet Don't Exist";

	return 0;
}

iii) Longest consecutive sequence

#include <bits/stdc++.h> 
using namespace std; 

// Returns length of the longest 
// contiguous subsequence 
int findLongestConseqSubseq(int arr[], int n) 
{ 
	unordered_set<int> S; 
	int ans = 0; 

	// Hash all the array elements 
	for (int i = 0; i < n; i++) 
		S.insert(arr[i]); 

	// check each possible sequence from 
	// the start then update optimal length 
	for (int i = 0; i < n; i++) { 
		// if current element is the starting 
		// element of a sequence 
		if (S.find(arr[i] - 1) == S.end()) { 
			// Then check for next elements 
			// in the sequence 
			int j = arr[i]; 
			while (S.find(j) != S.end()) 
				j++; 

			// update optimal length if 
			// this length is more 
			ans = max(ans, j - arr[i]); 
		} 
	} 
	return ans; 
} 

int main() 
{ 
    int n,i;
    cin>>n;
	int arr[n]; 
	for(i=0;i<n;i++){
	    cin>>arr[i];
	}
	cout << "Length of the Longest contiguous subsequence is "
		<< findLongestConseqSubseq(arr, n); 
	return 0; 
}

iv)  Longest subarray with sum 0

#include <bits/stdc++.h> 
using namespace std; 

// Returns Length of the required subarray 
int maxLen(int arr[], int n) 
{ 
	// Map to store the previous sums 
	unordered_map<int, int> presum; 

	int sum = 0; // Initialize the sum of elements 
	int max_len = 0; // Initialize result 

	// Traverse through the given array 
	for (int i = 0; i < n; i++) { 
		// Add current element to sum 
		sum += arr[i]; 

		if (arr[i] == 0 && max_len == 0) 
			max_len = 1; 
		if (sum == 0) 
			max_len = i + 1; 

		// Look for this sum in Hash table 
		if (presum.find(sum) != presum.end()) { 
			// If this sum is seen before, then update max_len 
			max_len = max(max_len, i - presum[sum]); 
		} 
		else { 
			// Else insert this sum with index in hash table 
			presum[sum] = i; 
		} 
	} 

	return max_len; 
} 

int main() 
{
    int n,i;
    cin>>n;
	int arr[n];
	for(i=0;i<n;i++){
	    cin>>arr[i];
	}
	cout << "Length of the longest 0 sum subarray is "
		<< maxLen(arr, n); 

	return 0; 
} 

V) Longest subarray without repeating characters

public int lengthOfLongestSubstring(String s) {
if(s==null||s.length()==0){
return 0;
}
HashSet<Character> set = new HashSet<>();
int result = 1;
int i=0;
for(int j=0; j<s.length(); j++){
char c = s.charAt(j);
if(!set.contains(c)){
set.add(c);
result = Math.max(result, set.size());
}else{
while(i<j){
if(s.charAt(i)==c){
i++;
break;
}
set.remove(s.charAt(i));
i++;
}
}
}
return result;
}

3) Linked list

i) reverse a linked list

#include <iostream> 
using namespace std; 

/* Link list node */
struct Node { 
	int data; 
	struct Node* next; 
	Node(int data) 
	{ 
		this->data = data; 
		next = NULL; 
	} 
}; 

struct LinkedList { 
	Node* head; 
	LinkedList() 
	{ 
		head = NULL; 
	} 

	/* Function to reverse the linked list */
	void reverse() 
	{ 
		// Initialize current, previous and 
		// next pointers 
		Node* current = head; 
		Node *prev = NULL, *next = NULL; 

		while (current != NULL) { 
			// Store next 
			next = current->next; 

			// Reverse current node's pointer 
			current->next = prev; 

			// Move pointers one position ahead. 
			prev = current; 
			current = next; 
		} 
		head = prev; 
	} 

	/* Function to print linked list */
	void print() 
	{ 
		struct Node* temp = head; 
		while (temp != NULL) { 
			cout << temp->data << " "; 
			temp = temp->next; 
		} 
	} 

	void push(int data) 
	{ 
		Node* temp = new Node(data); 
		temp->next = head; 
		head = temp; 
	} 
}; 

/* Driver program to test above function*/
int main() 
{ 
	/* Start with the empty list */
	LinkedList ll;
	int n,N;
	cout<<"enter no. of node to be formed "<<endl;
	cin>>n;
	cout<<"enter the data to be inserted"<<endl;
	for(int i=0;i<n;i++){
	    cin>>N;
	    ll.push(N);
	}

	cout << "Given linked list\n"; 
	ll.print(); 

	ll.reverse(); 

	cout << "\nReversed Linked list \n"; 
	ll.print(); 
	return 0; 
} 








