# Interview-practice-questions
collection of all type of interview questions 

1) Array-
i)Find the duplicate in an array of N integers.
// C++ code to find
// duplicates in O(n) time
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
