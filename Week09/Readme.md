
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
```c
#include <vector>
#include <iostream>
#include <queue>

struct Task
{
    int index;
    int start;
    int needs;

    Task(int _index, int _start, int _needs)
    {
        index = _index;
        start = _start;
        needs = _needs;
    }
};

struct byStartComparator
{
    bool operator()(const Task &left, const Task &right)
    {
        return left.start > right.start;
    }
};

struct byNeedIndexComparator
{
    bool operator()(const Task &left, const Task &right)
    {
        if (left.needs == right.needs)
        {
            return left.index > right.index;
        }
        return left.needs > right.needs;
    }
};

std::priority_queue<Task, std::vector<Task>, byStartComparator> pqToCome;
std::priority_queue<Task, std::vector<Task>, byNeedIndexComparator> pqWaiting;

int main()
{
    int N;
    std::cin >> N;

    int t, f;
    for (int i = 0; i < N; i++)
    {
        std::cin >> t >> f;
        Task task = Task(i, t, f);
        pqToCome.push(task);
    }

    long long time = 0;

    while (!pqToCome.empty() || !pqWaiting.empty())
    {
        while (!pqToCome.empty() && pqToCome.top().start <= time)
        {
            pqWaiting.push(pqToCome.top());
            pqToCome.pop();
        }

        if (pqWaiting.empty() && !pqToCome.empty())
        {
            time = pqToCome.top().start;
            continue;
        }

        Task newTask = pqWaiting.top();
        pqWaiting.pop();

        std::cout << newTask.index << " ";

        time += newTask.needs;
    }

    return 0;
}
```
