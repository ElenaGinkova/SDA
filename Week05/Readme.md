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
