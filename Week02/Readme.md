# Бавни
## BubbleSort - След всяка итерация на i, най-големият елемент "изплува" чрез последователни размени на съседни елементи.
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
## SelectionSort - Търси се индексът на най-малкия елемент на всяка итерация. След това се разменя с текущия.
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
## InsertionSort - Всеки елемент се тегли като карта. Търси се мястото му в ръката, като се изместват по-големите стойности с една позиция надясно.
```c
void insertionSort(std::vector<int>& arr) {
	int N = arr.size();
	for(int i = 1; i < N; i++)
	{
		int key = arr[i];
		int j = i - 1;
		while(key < arr[j] && j >= 0)
		{
			arr[j + 1] = arr[j--];
		}
		arr[j + 1] = key;
	}
    }
```
# Бързи
## MergeSort - Масивът се разделя на две половинки подмасиви. Всяка половинка продължава да се разделя. Процесът спира при достигане на масив с един елемент. Използваме индекси
```c
void _mergeSort(std::vector<int>& arr, size_t left, size_t right, std::vector<int>& buffer) {
	if(right - left <= 1) return;
	
	int mid = left + (right - left) / 2;
	_mergeSort(arr, left, mid buffer);
	_mergeSort(arr, mid, right, buffer);
	_merge(arr, left, mid, right, buffer);
}
void mergeSort(std::vector<int>& arr) {
	if(arr.size() <= 1)return;
	vector<int> buff(arr.size());
	_mergeSort(arr, 0, arr.size(), buff);
}
void _merge(std::vector<int>& arr, size_t left, size_t mid, size_t right, std::vector<int>& buffer) {
	size_t leftIdx = left;
	size_t rightIdx = mid;
	size_t index = 0;
	
	while (leftIdx < mid && rightIdx < right) {
        if (arr[leftIdx] <= arr[rightIdx]) {
            buffer[index++] = arr[leftIdx++];
        }
        else {
		buffer[index++] = arr[rightIdx++];
        }
	}

	while (leftIdx < mid) {
		buffer[index++] = arr[leftIdx++];
	}

	while (rightIdx < right) {
		buffer[index++] = arr[rightIdx++];
	}

	for (size_t i = 0; i < index; i++) {
		arr[left + i] = buffer[i];
	}
}
```
