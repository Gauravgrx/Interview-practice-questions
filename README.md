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


ii) Middle of a linked list

#include<bits/stdc++.h> 
using namespace std; 

// Struct 
struct Node 
{ 
	int data; 
	struct Node* next; 
}; 

/* Function to get the middle of the linked list*/
void printMiddle(struct Node *head) 
{ 
	struct Node *slow_ptr = head; 
	struct Node *fast_ptr = head; 

	if (head!=NULL) 
	{ 
		while (fast_ptr != NULL && fast_ptr->next != NULL) 
		{ 
			fast_ptr = fast_ptr->next->next; 
			slow_ptr = slow_ptr->next; 
		} 
		printf("The middle element is [%d]\n\n", slow_ptr->data); 
	} 
} 

// Function to add a new node 
void push(struct Node** head_ref, int new_data) 
{ 
	/* allocate node */
	struct Node* new_node = new Node; 

	/* put in the data */
	new_node->data = new_data; 

	/* link the old list off the new node */
	new_node->next = (*head_ref); 

	/* move the head to point to the new node */
	(*head_ref) = new_node; 
} 

// A utility function to print a given linked list 
void printList(struct Node *ptr) 
{ 
	while (ptr != NULL) 
	{ 
		printf("%d->", ptr->data); 
		ptr = ptr->next; 
	} 
	printf("NULL\n"); 
} 

// Driver Code 
int main() 
{ 
	// Start with the empty list 
	struct Node* head = NULL; 
	int n;
	
	// Iterate and add element 
	for (int i=5; i>0; i--) 
	{ 
	    cin>>n;
		push(&head, n); 
		printList(head); 
		printMiddle(head); 
	} 

	return 0; 
} 

iii) Merge two sorted linked list

 #include <iostream>
#include <new>
#define SIZE(arr) (sizeof(arr) / sizeof(arr[0]))
using namespace std;
struct node {
   int data;
   struct node *next;
};
node *createList(int *arr, int n){
   node *head, *p;
   p = head = new node;
   head->data = arr[0];
   head->next = NULL;
   for (int i = 1; i < n; ++i) {
      p->next = new node;
      p = p->next;
      p->data = arr[i];
      p->next = NULL;
   }
return head;
}
void displayList(node *head){
   while (head != NULL) {
      cout << head->data << " ";
      head = head->next;
   }
   cout << endl;
}
node *mergeSortedLists(node *head1, node *head2){
   node *result = NULL;
   if (head1 == NULL) {
      return head2;
   }
   if (head2 == NULL) {
      return head1;
   }
   if (head1->data < head2->data) {
      result = head1;
      result->next = mergeSortedLists(head1->next, head2);
   } else {
      result = head2;
      result->next = mergeSortedLists(head1, head2->next);
   }
   return result;
}
int main(){
    int n,m,i;
    cout<<"enter size of arrays"<<endl;
    cin>>n>>m; 
    int arr1[n];
    int arr2[m];
    cout<<"enter array elements in sorted order"<<endl;
    for(i=0;i<n;i++){
        cin>>arr1[i];
    }
    for(i=0;i<m;i++){
        cin>>arr2[i];
    }
   node *head1, *head2, *result = NULL;
   head1 = createList(arr1, n);
   head2 = createList(arr2, m);
   cout << "First sorted list: " << endl;
   displayList(head1);
   cout << "Second sorted list: " << endl;
   displayList(head2);
   result = mergeSortedLists(head1, head2);
   cout << "Final sorted list: " << endl;
   displayList(result);
   return 0;
}
	
iv) delete nth node from the end of linked list

#include<bits/stdc++.h> 
using namespace std; 

class LinkedList 
{ 
	public: 
	
	// Linked list Node 
	class Node 
	{ 
		public: 
		int data; 
		Node* next; 
		Node(int d) 
		{ 
			data = d; 
			next = NULL; 
		} 
	}; 
	
	// Head of list 
	Node* head;

	// Function to delete the nth node from 
	// the end of the given linked list 
	Node* deleteNode(int key) 
	{

		// First pointer will point to 
		// the head of the linked list 
		Node *first = head; 

		// Second pointer will point to the 
		// Nth node from the beginning 
		Node *second = head; 
		for (int i = 0; i < key; i++) 
		{ 

			// If count of nodes in the given 
			// linked list is <= N 
			if (second->next == NULL) 
			{ 

				// If count = N i.e. 
				// delete the head node 
				if (i == key - 1) 
					head = head->next; 
				return head; 
			} 
			second = second->next; 
		} 

		// Increment both the pointers by one until 
		// second pointer reaches the end 
		while (second->next != NULL) 
		{ 
			first = first->next; 
			second = second->next; 
		} 

		// First must be pointing to the 
		// Nth node from the end by now 
		// So, delete the node first is pointing to 
		first->next = first->next->next; 
		return head; 
	} 

	// Function to insert a new Node 
	// at front of the list 
	Node* push(int new_data) 
	{ 
		Node* new_node = new Node(new_data); 
		new_node->next = head; 
		head = new_node; 
		return head; 
	} 

	// Function to print the linked list 
	void printList() 
	{ 
		Node* tnode = head; 
		while (tnode != NULL) 
		{ 
			cout << (tnode->data) << ( " "); 
			tnode = tnode->next; 
		} 
	} 
}; 

// Driver code 
int main() 
{ 
	LinkedList* llist = new LinkedList();
	int n;
	cout<<"enter no of nodes"<<endl;
	cin>>n;
	for(int i=0;i<n;i++){
	    int m;
	    cout<<"enter list elements"<<endl;
	    cin>>m;
	    llist ->head = llist->push(m);
	}

	cout << ("Created Linked list is:\n"); 
	llist->printList(); 

	int N = 1; 
	llist->head = llist->deleteNode(N); 

	cout << ("\nLinked List after Deletion is:\n"); 
	llist->printList(); 
} 

v) Delete a given node when a node is given(in O(1))

#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node { 
public: 
	int data; 
	Node* next; 
}; 

/* Given a reference (pointer to pointer) to the head 
	of a list and an int, push a new node on the front 
	of the list. */
void push(Node** head_ref, int new_data) 
{ 
	/* allocate node */
	Node* new_node = new Node(); 

	/* put in the data */
	new_node->data = new_data; 

	/* link the old list off the new node */
	new_node->next = (*head_ref); 

	/* move the head to point to the new node */
	(*head_ref) = new_node; 
} 

void printList(Node* head) 
{ 
	Node* temp = head; 
	while (temp != NULL) { 
		cout << temp->data << " "; 
		temp = temp->next; 
	} 
} 

void deleteNode(Node* node) 
{ 
	Node* prev; 
	if (node == NULL) 
		return; 
	else { 
		while (node->next != NULL) { 
			node->data = node->next->data; 
			prev = node; 
			node = node->next; 
		} 
		prev->next = NULL; 
	} 
} 

int main() 
{ 
	/* Start with the empty list */
	Node* head = NULL; 
	int m,n;
	cout<<"enter total number nodes "<<endl;
	cin>>m;

	/* Use push() to construct below list 
	1->12->1->4->1*/
	cout<<"enter no. to be pushed"<<endl;
	for(int i=0;i<m;i++){
	cin>>n;
	push(&head, n);}

	cout << "Before deleting \n"; 
	printList(head); 

	/* I m deleting the head itself. 
		You can check for more cases */
	deleteNode(head); 

	cout << "\nAfter deleting \n"; 
	printList(head); 
	return 0; 
}  

vi) Find the intersection point of Y linked list.


#include <iostream> 
using namespace std; 

// Link list node 
struct Node { 
	int data; 
	Node* next; 
}; 

// Function to get the intersection point 
// of the given linked lists 
int getIntersectionNode(Node* head1, Node* head2) 
{ 
	Node *curr1 = head1, *curr2 = head2; 

	// While both the pointers are not equal 
	while (curr1 != curr2) { 

		// If the first pointer is null then 
		// set it to point to the head of 
		// the second linked list 
		if (curr1 == NULL) { 
			curr1 = head2; 
		} 

		// Else point it to the next node 
		else { 
			curr1 = curr1->next; 
		} 

		// If the second pointer is null then 
		// set it to point to the head of 
		// the first linked list 
		if (curr2 == NULL) { 
			curr2 = head1; 
		} 

		// Else point it to the next node 
		else { 
			curr2 = curr2->next; 
		} 
	} 

	// Return the intersection node 
	return curr1->data; 
} 

// Driver code 
int main() 
{ 
	/* 
	Create two linked lists 

	1st Linked list is 3->6->9->15->30 
	2nd Linked list is 10->15->30 
	
	15 is the intersection point 
	*/

	Node* newNode; 
	Node* head1 = new Node(); 
	head1->data = 10; 
	Node* head2 = new Node(); 
	head2->data = 3; 
	newNode = new Node(); 
	newNode->data = 6; 
	head2->next = newNode; 
	newNode = new Node(); 
	newNode->data = 9; 
	head2->next->next = newNode; 
	newNode = new Node(); 
	newNode->data = 15; 
	head1->next = newNode; 
	head2->next->next->next = newNode; 
	newNode = new Node(); 
	newNode->data = 30; 
	head1->next->next = newNode; 
	head1->next->next->next = NULL; 

	// Print the intersection node 
	cout << getIntersectionNode(head1, head2); 

	return 0; 
} 

vii) Check if a linked list is palindrome or not

#include<bits/stdc++.h>
using namespace std;

/* Link list node */
struct Node { 
	char data; 
	struct Node* next; 
}; 

void reverse(struct Node**); 
bool compareLists(struct Node*, struct Node*); 

/* Function to check if given linked list is 
palindrome or not */
bool isPalindrome(struct Node* head) 
{ 
	struct Node *slow_ptr = head, *fast_ptr = head; 
	struct Node *second_half, *prev_of_slow_ptr = head; 
	struct Node* midnode = NULL; // To handle odd size list 
	bool res = true; // initialize result 

	if (head != NULL && head->next != NULL) { 
		/* Get the middle of the list. Move slow_ptr by 1 
		and fast_ptrr by 2, slow_ptr will have the middle 
		node */
		while (fast_ptr != NULL && fast_ptr->next != NULL) { 
			fast_ptr = fast_ptr->next->next; 

			/*We need previous of the slow_ptr for 
			linked lists with odd elements */
			prev_of_slow_ptr = slow_ptr; 
			slow_ptr = slow_ptr->next; 
		} 

		/* fast_ptr would become NULL when there are even elements in list. 
		And not NULL for odd elements. We need to skip the middle node 
		for odd case and store it somewhere so that we can restore the 
		original list*/
		if (fast_ptr != NULL) { 
			midnode = slow_ptr; 
			slow_ptr = slow_ptr->next; 
		} 

		// Now reverse the second half and compare it with first half 
		second_half = slow_ptr; 
		prev_of_slow_ptr->next = NULL; // NULL terminate first half 
		reverse(&second_half); // Reverse the second half 
		res = compareLists(head, second_half); // compare 

		/* Construct the original list back */
		reverse(&second_half); // Reverse the second half again 

		// If there was a mid node (odd size case) which 
		// was not part of either first half or second half. 
		if (midnode != NULL) { 
			prev_of_slow_ptr->next = midnode; 
			midnode->next = second_half; 
		} 
		else
			prev_of_slow_ptr->next = second_half; 
	} 
	return res; 
} 

/* Function to reverse the linked list Note that this 
	function may change the head */
void reverse(struct Node** head_ref) 
{ 
	struct Node* prev = NULL; 
	struct Node* current = *head_ref; 
	struct Node* next; 
	while (current != NULL) { 
		next = current->next; 
		current->next = prev; 
		prev = current; 
		current = next; 
	} 
	*head_ref = prev; 
} 

/* Function to check if two input lists have same data*/
bool compareLists(struct Node* head1, struct Node* head2) 
{ 
	struct Node* temp1 = head1; 
	struct Node* temp2 = head2; 

	while (temp1 && temp2) { 
		if (temp1->data == temp2->data) { 
			temp1 = temp1->next; 
			temp2 = temp2->next; 
		} 
		else
			return 0; 
	} 

	/* Both are empty reurn 1*/
	if (temp1 == NULL && temp2 == NULL) 
		return 1; 

	/* Will reach here when one is NULL 
	and other is not */
	return 0; 
} 

/* Push a node to linked list. Note that this function 
changes the head */
void push(struct Node** head_ref, char new_data) 
{ 
	/* allocate node */
	struct Node* new_node = new Node();

	/* put in the data */
	new_node->data = new_data; 

	/* link the old list off the new node */
	new_node->next = (*head_ref); 

	/* move the head to pochar to the new node */
	(*head_ref) = new_node; 
} 

// A utility function to print a given linked list 
void printList(struct Node* ptr) 
{ 
	while (ptr != NULL) { 
	    cout<<"->"<<ptr->data;
		ptr = ptr->next; 
	} 
	printf("NULL\n"); 
} 

/* Drier program to test above function*/
int main() 
{ 
	/* Start with the empty list */
	struct Node* head = NULL; 
	string str;
	cout<<"Enter the string to be checked"<<endl;
	cin>>str;
	int i; 

	for (i = 0; str[i] != '\0'; i++) { 
		push(&head, str[i]); 
		printList(head); 
		isPalindrome(head) ? printf("Is Palindrome\n\n") : printf("Not Palindrome\n\n"); 
	} 

	return 0; 
} 

viii) Reverse a linked list in groups.

#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node 
{ 
	public: 
	int data; 
	Node* next; 
}; 

/* Reverses the linked list in groups 
of size k and returns the pointer 
to the new head node. */
Node *reverse (Node *head, int k) 
{ 
	Node* current = head; 
	Node* next = NULL; 
	Node* prev = NULL; 
	int count = 0; 
	
	/*reverse first k nodes of the linked list */
	while (current != NULL && count < k) 
	{ 
		next = current->next; 
		current->next = prev; 
		prev = current; 
		current = next; 
		count++; 
	} 
	
	/* next is now a pointer to (k+1)th node 
	Recursively call for the list starting from current. 
	And make rest of the list as next of first node */
	if (next != NULL) 
	head->next = reverse(next, k); 

	/* prev is new head of the input list */
	return prev; 
} 

/* UTILITY FUNCTIONS */
/* Function to push a node */
void push(Node** head_ref, int new_data) 
{ 
	/* allocate node */
	Node* new_node = new Node(); 

	/* put in the data */
	new_node->data = new_data; 

	/* link the old list off the new node */
	new_node->next = (*head_ref);	 

	/* move the head to point to the new node */
	(*head_ref) = new_node; 
} 

/* Function to print linked list */
void printList(Node *node) 
{ 
	while (node != NULL) 
	{ 
		cout<<node->data<<" "; 
		node = node->next; 
	} 
} 

/* Driver code*/
int main() 
{ 
	/* Start with the empty list */
	Node* head = NULL; 

	/* Created Linked list is 1->2->3->4->5->6->7->8->9 */
	int m,n;
	cout<<"enter no of nodes"<<endl;
	cin>>m;
	for(int i=0;i<m;i++){
	    cin>>n;
	    push(&head, n); 

	}
	cout<<"Given linked list \n"; 
	printList(head); 
	head = reverse(head, 3); 

	cout<<"\nReversed Linked list \n"; 
	printList(head); 

	return(0); 
}

IX) Detect a cycle in a linkedlist

#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node { 
public: 
	int data; 
	Node* next; 
}; 

void push(Node** head_ref, int new_data) 
{ 
	/* allocate node */
	Node* new_node = new Node(); 

	/* put in the data */
	new_node->data = new_data; 

	/* link the old list off the new node */
	new_node->next = (*head_ref); 

	/* move the head to point to the new node */
	(*head_ref) = new_node; 
} 

int detectLoop(Node* list) 
{ 
	Node *slow_p = list, *fast_p = list; 

	while (slow_p && fast_p && fast_p->next) { 
		slow_p = slow_p->next; 
		fast_p = fast_p->next->next; 
		if (slow_p == fast_p) { 
			return 1; 
		} 
	} 
	return 0; 
} 

/* Driver code*/
int main() 
{ 
	/* Start with the empty list */
	Node* head = NULL; 

	push(&head, 20); 
	push(&head, 4); 
	push(&head, 15); 
	push(&head, 10); 

	/* Create a loop for testing */
	head->next->next->next->next = head; 
	if (detectLoop(head)) 
		cout << "Loop found"; 
	else
		cout << "No Loop"; 
	return 0; 
} 

X) Flattening a Linked list
 
#include <stdio.h> 
#include <stdlib.h> 

// A Linked List Node 
typedef struct Node 
{ 
	int data; 
	struct Node *right; 
	struct Node *down; 
} Node; 

/* A utility function to insert a new node at the beginning 
of linked list */
void push (Node** head_ref, int new_data) 
{ 
	/* allocate node */
	Node* new_node = (Node *) malloc(sizeof(Node)); 
	new_node->right = NULL; 

	/* put in the data */
	new_node->data = new_data; 

	/* link the old list off the new node */
	new_node->down = (*head_ref); 

	/* move the head to point to the new node */
	(*head_ref) = new_node; 
} 

/* Function to print nodes in the flattened linked list */
void printList(Node *node) 
{ 
	while (node != NULL) 
	{ 
		printf("%d ", node->data); 
		node = node->down; 
	} 
} 

// A utility function to merge two sorted linked lists 
Node* merge( Node* a, Node* b ) 
{ 
	// If first list is empty, the second list is result 
	if (a == NULL) 
		return b; 

	// If second list is empty, the second list is result 
	if (b == NULL) 
		return a; 

	// Compare the data members of head nodes of both lists 
	// and put the smaller one in result 
	Node* result; 
	if (a->data < b->data) 
	{ 
		result = a; 
		result->down = merge( a->down, b ); 
	} 
	else
	{ 
		result = b; 
		result->down = merge( a, b->down ); 
	} 

	result->right = NULL; 
	return result; 
} 

// The main function that flattens a given linked list 
Node* flatten (Node* root) 
{ 
	// Base cases 
	if (root == NULL || root->right == NULL) 
		return root; 

	// Merge this list with the list on right side 
	return merge( root, flatten(root->right) ); 
} 

// Driver program to test above functions 
int main() 
{ 
	Node* root = NULL; 

	/* Let us create the following linked list 
	5 -> 10 -> 19 -> 28 
	| |	 |	 | 
	V V	 V	 V 
	7 20 22 35 
	|		 |	 | 
	V		 V	 V 
	8		 50 40 
	|			 | 
	V			 V 
	30			 45 
	*/
	push( &root, 30 ); 
	push( &root, 8 ); 
	push( &root, 7 ); 
	push( &root, 5 ); 

	push( &( root->right ), 20 ); 
	push( &( root->right ), 10 ); 

	push( &( root->right->right ), 50 ); 
	push( &( root->right->right ), 22 ); 
	push( &( root->right->right ), 19 ); 

	push( &( root->right->right->right ), 45 ); 
	push( &( root->right->right->right ), 40 ); 
	push( &( root->right->right->right ), 35 ); 
	push( &( root->right->right->right ), 20 ); 

	// Let us flatten the list 
	root = flatten(root); 

	// Let us print the flatened linked list 
	printList(root); 

	return 0; 
} 















