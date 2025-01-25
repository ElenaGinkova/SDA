INT_MAX < 10^9

-2^31 <= val <= 2^31 - 1 // но в рекурсивна зад или сбор не стига
```c
	std::cout << (*std::lower_bound(v.begin(), v.end(), target)) << std::endl;
	std::cout << (*std::upper_bound(v.begin(), v.end(), target)) << std::endl;
```
```c
int ternarySearch(const vector<int> &arr, int l, int r, int x) {
    while (r >= l) {
        int mid1 = l + (r - l) / 3;
        int mid2 = r - (r - l) / 3;
        if (arr[mid1] == x)
            return mid1;
        if (arr[mid2] == x)
            return mid2;
        if (x < arr[mid1]) {
            r = mid1 - 1;
        }
        else if (x > arr[mid2]) {
            l = mid2 + 1;
        }
        else {
            l = mid1 + 1;
            r = mid2 - 1;
        }
    }
    return -1;
}
```
