# Primitive-Root
#include <iostream>
#include <cmath>
#include <bits/stdc++.h>
using namespace std;

bool isPrime(int n)
{

    if (n <= 1) return false;
    if (n <= 3) return true;
    if (n%2 == 0 || n%3 == 0) return false;
    for (int a=5; a*a<=n; a=a+6)
    if (n%a == 0 || n%(a+2) == 0)
    return false;

    return true;
}

int power(int x, unsigned int y, int p)
{
    int res = 1;
    x = x % p;


    while (y > 0)
    {

        if (y & 1)
            res = (res*x) % p;

        y = y >> 1;
        x = (x*x) % p;
    }
    return res;
}


void findPrimefactors(unordered_set<int> &s, int n)
{

    while (n%2 == 0)
    {
        s.insert(2);
        n = n/2;
    }


    for (int a = 3; a <= sqrt(n); a = a+2)
    {
        while (n%a == 0)
        {
            s.insert(a);
            n = n/a;
        }
    }


    if (n > 2)
        s.insert(n);
}

int findPrimitive(int n)
{
    unordered_set<int> s;

    if (isPrime(n)==false)
        return -1;


    int phi = n-1;

    findPrimefactors(s, phi);


    for (int r=2; r<=phi; r++)
    {

        bool flag = false;
        for (auto it = s.begin(); it != s.end(); it++)
        {


            if (power(r, phi/(*it), n) == 1)
            {
                flag = true;
                break;
            }
        }


        if (flag == false)
        return r;
    }


    return -1;
}


int main()
{
    int n;
    cout << "Enter mode : ";
    cin >> n;
    cout << "Smallest primitive root of " << n
        << " is " << findPrimitive(n);
    return 0;
}



