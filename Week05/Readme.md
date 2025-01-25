```c
string removeDuplicates(string str) {
        string result;
        for(char ch : str)
        {
            if(result.size() == 0)
            {
                result.push_back(ch);
                continue;
            }
            if(result.back() == ch)
            {
                result.pop_back();
            }
            else
            result.push_back(ch);
        }
        return result;
    }
```
```c
  vector<int> dailyTemperatures(vector<int>& temperatures) {
        vector<int> result(temperatures.size(), 0);
        
        // contains indexes of elements in decreasing order
        stack<int> ms; // ms - monotonic stack
        for(size_t i = 0; i < temperatures.size(); i++) {
            // pop all indexes of elements which are lower than the new temperature
            while(!ms.empty() && temperatures[ms.top()] < temperatures[i]) {
                // for each popped index write in the result
                result[ms.top()] = i - ms.top();
                ms.pop();
            }
            
            ms.push(i);
        }
        
        return result;
    }
```
## sliding window
```c
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        // head - current max
        // next elements - potential max elements
        deque<int> dq;
        vector<int> result;
        
        for(int i = 0; i < nums.size(); i++) {
            // keep the dq monotonic
            while(!dq.empty() && nums[i] >= nums[dq.back()]) {
                dq.pop_back();
            }
            dq.push_back(i);
            // pop the front if it is now outside the window!
            if(dq.front() <= i - k) {
                dq.pop_front();
            }

            // start working on the result after you have passed atleast one window (k elements) to the dq
            if(i >= k - 1) {
                result.push_back(nums[dq.front()]);
            }
        }
        
        return result;
    }
```
