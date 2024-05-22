### Bucket Fill

```c++
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

const int N = 1e3 + 10;

typedef pair<int, int> PII;

int n, m;
char g[N][N];
bool st[N][N];

int dx[] = {1, -1, 0, 0}, dy[] = {0, 0, 1, -1};

void bfs(int x, int y) {
    queue<PII> q;
    q.push({x, y});
    st[x][y] = true;

    while (q.size()) {
        auto t = q.front();
        q.pop();
        x = t.first, y = t.second;

        for (int i = 0; i < 4; i++) {
            int ax = x + dx[i], ay = y + dy[i];
            if (ax >= 0 && ax < n && ay >= 0 && ay < m && g[ax][ay] == g[x][y] && !st[ax][ay]) {
                q.push({ax, ay});
                st[ax][ay] = true;
            }
        }
    }
}

int main() {
    vector<string> picture({"bbba", "abba", "acaa", "aaac"});

    n = picture.size(), m = picture[0].size();

    for (int i = 0; i < picture.size(); i++) {
        for (int j = 0; j < picture[i].size(); j++) {
            g[i][j] = picture[i][j];
        }
    }

    int ans = 0;
    for (int i = 0; i < picture.size(); i++) {
        for (int j = 0; j < picture[i].size(); j++) {
            if (!st[i][j]) {
                bfs(i, j);
                ans++;
            }
        }
    }
    cout << ans;
    return 0;
}
```

### Frequency Sort

```python
def sort_items(items):
  freq_counter = Counter(items)
  ans = sorted(items, key=lambda x: (freq_counter[x], x))
  return ans
```

### Minimum Processing Time

```java
import java.util.*;

class TaskScheduler {
    public static int calculateMinimumFinishTime(List<Integer> processorTimes, List<Integer> taskTimes) {
        // Sort the processor times in ascending order.
        Collections.sort(processorTimes);

        // Sort the task times in descending order to assign longer tasks to faster processors.
        Collections.sort(taskTimes, Collections.reverseOrder());

        int finishTime = 0;
        int currentTask = 0;

        for (int processorTime : processorTimes) {
            for (int i = 0; i < taskTimes.size() && currentTask < taskTimes.size(); ++i) {
                int completionTime = taskTimes.get(currentTask) + processorTime;
                currentTask++;
                finishTime = Math.max(finishTime, completionTime);
            }
        }

        return finishTime;
    }
}

public class TaskSchedulerApp {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the number of processors: ");
        int numProcessors = scanner.nextInt();

        ArrayList<Integer> processorTimes = new ArrayList<>();
        for (int i = 0; i < numProcessors; i++) {
            System.out.print("Enter processing time for processor " + (i + 1) + ": ");
            int processingTime = scanner.nextInt();
            processorTimes.add(processingTime);
        }

        System.out.print("Enter the number of tasks: ");
        int numTasks = scanner.nextInt();

        ArrayList<Integer> taskTimes = new ArrayList<>();
        for (int i = 0; i < numTasks; i++) {
            System.out.print("Enter execution time for task " + (i + 1) + ": ");
            int executionTime = scanner.nextInt();
            taskTimes.add(executionTime);
        }

        TaskScheduler taskScheduler = new TaskScheduler();
        int minimumFinishTime = taskScheduler.calculateMinimumFinishTime(processorTimes, taskTimes);

        System.out.println("Minimum Finish Time: " + minimumFinishTime);
    }
}
```

### KeyBoard

![image-20231009164211089](/Users/songpx/Library/Application Support/typora-user-images/image-20231009164211089.png)

```python
def calculate_steps(str, keyboard):
    # create a dictionary that maps each character to its position on the keypad
    char_to_pos = {}
    for i in range(len(keyboard)):
        for j in range(len(keyboard[i])):
            char_to_pos[keyboard[i][j]] = (i, j)

    # initialize the total steps to 0
    total_steps = 0

    # iterate through each pair of adjacent characters in the string
    for i in range(1, len(str)):
        # calculate the number of steps required to move the finger from the first character to the second character
        pos1 = char_to_pos[str[i-1]]
        pos2 = char_to_pos[str[i]]
        steps = abs(pos1[0] - pos2[0]) + abs(pos1[1] - pos2[1])

        # add the number of steps to the total steps
        total_steps += steps

    # return the total steps
    return total_steps
```

### Delivery Management System

```python
import heapq


def order(city_nodes, city_from, city_to, company):
    graph = [[] for _ in range(city_nodes)]
    for i in range(len(city_from)):
        graph[city_from[i] - 1].append((1, city_to[i] - 1))
        graph[city_to[i] - 1].append((1, city_from[i] - 1))

    heap = [(0, company - 1)]

    distance = [city_nodes + 1 for _ in range(city_nodes)]
    distance[company - 1] = 0

    city_order = []
    while heap:
        cur = heapq.heappop(heap)

        if cur[1] + 1 != company:
            city_order.append(cur[1] + 1)

        for vertex in graph[cur[1]]:
            if distance[cur[1]] + vertex[0] < distance[vertex[1]]:
                distance[vertex[1]] = distance[cur[1]] + vertex[0]
                heapq.heappush(heap, (distance[vertex[1]], vertex[1]))

    return city_order


city_nodes = 5
city_from = [1, 1, 2, 3, 1]
city_to = [2, 3, 4, 5, 5]
company = 1
print('Test Case 0: ', order(city_nodes, city_from, city_to, company))

```

### Extraordinary Substrings

```python
def countSubstrings(input_str: str) -> int:
  length = len(input_str)
  
  c2i = {'a': 1, 'b': 1}
  for i in range(2, 26):
    c2i[chr(ord('a') + i)] = (i - 2) // 3 + 2
    
  ans = 0
  for i in range(length):
    s = 0
    for j in range(i, length):
      c = input_str[j]
      s += c2i[c]
      if not s % (j - i + 1):
        ans += 1
  return ans
```

### Minimum Swaps

```python
def minSwap(arr, n): 
  temp = sorted(arr.copy(), reverse=True)
  
  h = {}
  for i in range(n): 
    h[arr[i]] = i 

  init = 0
  ans = 0
  for i in range(n): 
    if (arr[i] != temp[i]): 
      ans += 1
      init = arr[i]  

      arr[i], arr[h[temp[i]]] = arr[h[temp[i]]], arr[i]  
      h[init] = h[temp[i]] 

      h[temp[i]] = i
  return ans 
```

### Laser Grid

```python
def compute_cost(initR, initC, finalR, finalC, costRows, costCols):

  if initR > finalR: 
    return compute_cost(finalR, finalC, initR, initC, costRows, costCols)   

  if initC > finalC: 
    return compute_cost(initR, finalC, finalR, initC, costRows, costCols)

  return sum(costRows[initR:finalR]) + sum(costCols[initC:finalC])
```

### Alternating Prime Sequence

```python
def is_prime(n):
    if n <= 1:
        return False

    i = 2

    while i * i <= n:
        if n % i == 0:
            return False
        i += 1

    return True


def compute_min_penalty(arr):
    primes, comps = [], []

    for x in arr.sort(reverse=True):
        if is_prime(x):
            primes.append(x)
        else:
            comps.append(x)

    if len(primes) > len(comps):
        return sum(primes[len(comps)+1:])
    else:
        return sum(comps[len(primes)+1:])
```

### Document Chunking

```python
def mininumChunksRequired(totalPackets, uploadedChunks):

    uploadedChunks.sort()
    uploadedChunks.append([totalPackets+1, totalPackets+2])

    current = 0
    
    result = 0
    for start, end in uploadedChunks:
        result += bin(start - current - 1).count('1')
        current = end
    return result
```

### Maximum Distinct

unique_of_a + min(k, b有a没有的个数，a中重复的个数)

###  Autoscale Policy

```python
import math
def finalInstances(instances, averageUtil):

    maxInstances = 2 * 10 ** 8
    action = False
    stopCount = 0
    for util in averageUtil:
        print(util)
        
        if (action):
            stopCount += 1
            if (stopCount == 10):
                action = False
            continue

        if util > 60:
            if (instances * 2 < maxInstances):
                instances *= 2
                action = True
                stopCount = 0

        if util < 25:
            if (instances > 1):
                instances /= 2
                instances = math.ceil(instances)
                action = True
                stopCount = 0
        print(instances)

    return instances

```
