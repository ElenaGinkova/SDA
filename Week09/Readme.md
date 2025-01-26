
```c
struct Struct {
	int a, b;
};

!!!callable
struct StructMaxComparator {
	bool operator()(const Struct& s1, const Struct& s2) {
		return s1.a < s2.a;
	}
};

struct StructMinComparator {
	bool operator()(const Struct& s1, const Struct& s2) {
		return s1.a > s2.a;
	}
};

int main() {
	// change to StructMinComparator to make it min heap
	std::priority_queue<Struct, std::vector<Struct>, StructMaxComparator> pq;
}
```
```c
        priority_queue<int> pq(stones.begin(), stones.end());
```
```c
 std::make_heap(nums.begin(), nums.end());
 current = nums.front();
std::pop_heap(nums.begin(), nums.end());
std::push_heap(nums.begin(), nums.end());
```
```c
priority_queue<int> pq(nums.begin(), nums.end());
```
```c
int findKthLargest(vector<int> &nums, int k)
    {
        std::make_heap(nums.begin(), nums.end());

        for (int i = 1; i < k; i++)
        {
            std::pop_heap(nums.begin(), nums.end());
            nums.pop_back(); // the element is not deleted only moved to the end of the vector
        }

        return nums.front();
    }
```
