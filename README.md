#include <iostream>
#include <sys/time.h>
#include <time.h>
#include <sys/resource.h>
using namespace std;
void insertionSort(int input[100], int n) {
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = input[i];
        j = i - 1;

        while (j >= 0 && input[j] > key) {
            input[j + 1] = input[j];
            j = j - 1;
        }
        input[j + 1] = key;
    }
}

int main() {
    struct timeval tv1, tv2;
    int size, input[50], i;
    struct rusage r_usage;

    cout << "Enter the input size: " <<endl;
    cin >> size;
    cout << "Enter the array elements: " <<endl;
    
    for (i = 0; i < size; i++) {
        cin >> input[i];
    }

    gettimeofday(&tv1, NULL);

    insertionSort(input, size);

    gettimeofday(&tv2, NULL);

    cout << "\nSorted array is: " <<endl;
    for (i = 0; i < size; i++) {
        cout << input[i] << "\t";
    }

    double time_microseconds = (double)(tv2.tv_usec - tv1.tv_usec);
    double time_seconds = (double)(tv2.tv_usec - tv1.tv_usec) / 1000000 + (double)(tv2.tv_sec - tv1.tv_sec);
    
    cout << "Time of insertion sort = " << time_microseconds << " microseconds" <<endl;
    cout << "Total time = " << time_seconds << " seconds" <<endl;

    getrusage(RUSAGE_SELF, &r_usage);
    cout << "Memory usage: " << r_usage.ru_maxrss << " kilobytes" <<endl;
}

