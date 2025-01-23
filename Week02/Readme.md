# Бавни
## BubbleSort
```c
void optimizedBubbleSort(std::vector<int>& arr) {
	int lastSwappedIndex = arr.size() - 1;
	for (size_t i = 0; i < arr.size(); i++) {
		int currentSwappedIndex = 0; // what if we used -1?
		for (size_t j = 0; j < lastSwappedIndex; j++) {
			if (arr[j] > arr[j + 1]) {
				currentSwappedIndex = j;
				swap(arr[j], arr[j + 1]);
			}
		}

		if (currentSwappedIndex == 0) {
			return;
		}
		lastSwappedIndex = currentSwappedIndex;
	}
}
```
## SelectionSort
```c
void selectionSort(std::vector<int>& arr) {
    int N = arr.size();
    for(int i = 0; i < N - 1; i++)
    {
      int minI = i;
      for(int j = i + 1; j < N; j++)
      {
        if(arr[minI] > arr[j]) minI = j;
      }
      if(minI != i) swap(arr[minI], arr[i]);
    }
}
```
## SelectionSort
```c

```
