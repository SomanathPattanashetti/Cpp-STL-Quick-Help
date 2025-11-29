# 📚 C++ STL Quick Help

```
╔═══════════════════════════════════════════════════════════════════╗
║  Complete C++ STL Reference with Easy-to-Use Examples & Patterns  ║
║  Perfect for Competitive Programming & LeetCode Solutions         ║
╚═══════════════════════════════════════════════════════════════════╝
```

> 🔎 **EASY + IMPORTANT + MOST USED** examples handpicked for quick reference
> 💡 All examples are copy-paste ready for immediate use
> 🎯 Includes LeetCode problems for practice

---

## 📝 Priority Queue (Heap) - 4 Different Comparator Methods 🗻

### Default Declarations
```cpp
priority_queue<int> pq;                      // creates max-heap
priority_queue<int, vector<int>> pq;         // creates max-heap
```

### Method 1️⃣: In-Built Comparators
```cpp
priority_queue<int, vector<int>, greater<int>> pq;  // min-heap

// For pairs
priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> pq;
```

### Method 2️⃣: Struct-Based Comparator
```cpp
struct comp {
    bool operator()(int &a, int &b) {
        return a < b;  // max-heap
        // return a > b;  // min-heap
    }
};

priority_queue<int, vector<int>, comp> pq;  // usage
```

### Method 3️⃣: Function-Based Comparator
```cpp
static bool comp(int &a, int &b) {
    return a < b;  // max-heap
    // return a > b;  // min-heap
}

priority_queue<int, vector<int>, function<bool(int&, int&)>> pq(comp);
```

### Method 4️⃣: Lambda Function (Most Flexible) ⭐
```cpp
auto comp = [](int &a, int &b) {
    return a < b;  // max-heap
    // return a > b;  // min-heap
};

priority_queue<int, vector<int>, decltype(comp)> pq(comp);
```

### 🎯 Lambda with Captured Variables
```cpp
unordered_map<int, int> mp;

auto comp = [&mp](int &a, int &b) {
    return mp[a] < mp[b];  // sort by map values
};

priority_queue<int, vector<int>, decltype(comp)> pq(comp);
```

**Benefit:** No manual loop needed, clean and efficient heap operations

---

## 🚀 std::move() - Efficient Resource Transfer ⬅️

**Purpose:** Transfer resources from source to target without copying

### Example 1: String Transfer
```cpp
string source = "MIK";
string target = "";
target = std::move(source);

cout << "source = " << source << endl;  // source = (empty)
cout << "target = " << target << endl;  // target = MIK
```

### Example 2: Push to Vector
```cpp
vector<string> v;
string str = "example";
v.push_back(std::move(str));  // str becomes empty, no copy created
```

### Example 3: Move Nested Containers
```cpp
vector<int> temp{1, 2, 3};
vector<vector<int>> result;
result.push_back(std::move(temp));  // temp is now empty, no redundant copy

// temp is now: {}
// result is now: {{1, 2, 3}}
```

**Benefit:** Saves memory and time by eliminating unnecessary copies

---

## ➕ std::accumulate() - Sum & Aggregate Operations

### Basic Sum (Without Lambda)
```cpp
vector<int> nums{1, 3, 2, 5};
int sum = accumulate(begin(nums), end(nums), 0);

cout << sum;  // output: 11
```

### With Custom Lambda Operations
```cpp
auto lambda = [&](int s, long n) {
    return s + n*n;  // sum of squares
};

vector<int> nums{1, 3, 2, 5};
int sum = accumulate(begin(nums), end(nums), 0, lambda);

cout << sum;  // output: 39 (1² + 3² + 2² + 5²)
```

### Example: 2D Matrix Summation
```cpp
auto lambda = [&](int sum, vector<int> vec) {
    sum = sum + accumulate(begin(vec), end(vec), 0);
    return sum;
};

int result = accumulate(matrix.begin(), matrix.end(), 0, lambda);
```

**Benefit:** Replaces tedious for loops with elegant one-liner operations

**LeetCode Applications:**
- Leetcode-1577: Number of Ways Where Square of Number Equals Product
- Leetcode-1572: Matrix Diagonal Sum

---

## 😲 Finding Min/Max Elements

### Separate Functions
```cpp
vector<int> nums{1, 3, 2, 5};

int minimumValue = *min_element(begin(nums), end(nums));  // 1
int maximumValue = *max_element(begin(nums), end(nums));  // 5
```

### Combined Function (Efficient)
```cpp
auto itr = minmax_element(begin(nums), end(nums));

int minimumValue = *itr.first;   // 1
int maximumValue = *itr.second;  // 5
```

**Benefit:** No manual loops needed, efficient O(n) operations

---

## 📤 upper_bound() & lower_bound() - Binary Search

### For Sorted Vector
```cpp
vector<int> vec{10, 20, 30, 30, 20, 10, 10, 20};

auto up = upper_bound(begin(vec), end(vec), 35);   // first element > 35
auto low = lower_bound(begin(vec), end(vec), 35);  // first element >= 35

cout << "upper_bound at position " << (up - vec.begin()) << '\n';
cout << "lower_bound at position " << (low - vec.begin()) << '\n';
```

### For Ordered Set
```cpp
set<int> st;
st.upper_bound(35);   // returns iterator to first element > 35
st.lower_bound(35);   // returns iterator to first element >= 35
```

### For Ordered Map
```cpp
map<int, string> mp;
mp.upper_bound(35);   // returns iterator to first element > 35
mp.lower_bound(35);   // returns iterator to first element >= 35
```

**Benefit:** No manual binary search needed, like Java's TreeMap

**LeetCode Applications:**
- Leetcode-729: My Calendar I
- Leetcode-981: Time Based Key-Value Store
- Leetcode-744: Find Smallest Letter Greater Than Target
- Leetcode-1351: Count Negative Numbers in a Sorted Matrix

---

## 🌀 std::rotate - Array Rotation

### Left Rotate by K
```cpp
vector<int> vec{1, 2, 3, 4};
int k = 2;
rotate(vec.begin(), vec.begin() + k, vec.end());
// Result: {3, 4, 1, 2}
```

### Right Rotate by K
```cpp
vector<int> vec{1, 2, 3, 4};
int n = vec.size();
int k = 2;
rotate(vec.begin(), vec.begin() + n - k, vec.end());
// Result: {3, 4, 1, 2}
```

---

## 🌀 String Rotation Check

**Problem:** Check if string `s` can become string `t` through rotation

```cpp
string s = "abcde";
string t = "cdeab";

bool isRotation = (s.length() == t.length() && (s + s).find(t) != string::npos);
cout << isRotation;  // true
```

**Logic:** If `t` is a rotation of `s`, then `t` will always be a substring of `s+s`

---

## ➡️ std::next_permutation - Next Lexicographic Order

**Purpose:** Generate the next lexicographically greater permutation

```cpp
vector<int> vec{1, 2, 3, 4};

if(next_permutation(begin(vec), end(vec))) {
    cout << "Next permutation available" << endl;
    for(int &x : vec)
        cout << x << " ";
    // Output: 1 2 4 3
}
```

**Note:** Returns false if already at greatest permutation (descending order)

**Also See:** `std::prev_permutation()` for previous lexicographically smaller permutation

**LeetCode Applications:**
- Leetcode-31: Next Permutation

---

## ⏩ std::stringstream - String Parsing & Conversion

### Use Case 1: String to Number Conversion
```cpp
string s = "12345";
stringstream ss(s);

int x = 0;
ss >> x;
cout << x;  // 12345
```

### Use Case 2: Count Words in String
```cpp
stringstream s("hello world this is C++");
string word;
int count = 0;

while (s >> word)
    count++;

cout << count;  // 5
// Note: Tokenizes by space character by default
```

### Use Case 3: Extract Numbers from Complex String
```cpp
string complex = "1+1i";
stringstream ss(complex);

char justToSkip;
int real, imag;

ss >> real >> justToSkip >> imag >> justToSkip;
cout << real << ", " << imag;  // 1, 1
```

**LeetCode Applications:**
- Leetcode-151: Reverse Words in a String
- Leetcode-186: Reverse Words in a String II
- Leetcode-557: Reverse Words in a String III
- Leetcode-1108: Defanging an IP Address
- Leetcode-1816: Truncate Sentence
- Leetcode-884: Uncommon Words from Two Sentences
- Leetcode-537: Complex Number Multiplication
- Leetcode-165: Compare Version Numbers

---

## 🤖 std::transform - Apply Operations to Ranges

**Purpose:** Apply an operation to elements in a range and store results

### Convert String to Lowercase
```cpp
string line = "Hello world, this is MIK";
transform(begin(line), end(line), begin(line), ::tolower);
cout << line;  // hello world, this is mik
```

### Convert String to Uppercase
```cpp
string line = "Hello world, this is MIK";
transform(begin(line), end(line), begin(line), ::toupper);
cout << line;  // HELLO WORLD, THIS IS MIK
```

**Benefit:** One-liner string case conversion without loops

---

## 📟 std::regex_replace - Pattern Replacement

### Example 1: Remove All Vowels
```cpp
string s = "mika";
auto rgx = regex("[aeiouAEIOU]");
cout << regex_replace(s, rgx, "");  // mk
```

### Example 2: Replace Dots with Brackets
```cpp
string s = "1.2.3.4";
auto rgx = regex("\\.");
cout << regex_replace(s, rgx, "[.]");  // 1[.]2[.]3[.]4
```

**Tip:** Use complex regex patterns for advanced replacements

**LeetCode Applications:**
- Leetcode-1108: Defanging an IP Address
- Leetcode-1119: Remove Vowels from a String

---

## 🔢 std::count_if - Conditional Element Counting

**Purpose:** Count elements satisfying a specific condition

```cpp
vector<int> vec{1, 3, 2, 0, 5, 0};

auto lambda = [&](const auto& i) {
    return i == 0;
};

cout << count_if(begin(vec), end(vec), lambda);  // 2
```

**Flexibility:** Use any lambda/comparator for custom conditions

**LeetCode Applications:**
- Leetcode-1773: Count Items Matching a Rule

---

## 🔢 std::copy_if - Conditional Element Copying

**Purpose:** Copy elements matching a condition to another container

```cpp
vector<int> from_vec = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
vector<int> to_vec;

// Copy all even numbers
copy_if(from_vec.begin(), from_vec.end(), back_inserter(to_vec), 
        [](int n){ return n % 2 == 0; });

for(auto it : to_vec)
    cout << it << " ";
// Output: 2 4 6 8 10
```

**Syntax:** `copy_if(begin, end, destination, condition)`

**LeetCode Applications:**
- Leetcode-1796: Second Largest Digit in a String

---

## 🔢 Lambda with upper_bound/lower_bound for Pairs

### Example 1: Custom Comparator for Pairs
```cpp
vector<pair<int, string>> my_vector;
// ... populate vector ...

pair<int, string> ref = make_pair(timestamp, "");

auto lambda = [](const pair<int, string>& p1, const pair<int, string>& p2) {
    return p1.first < p2.first;
};

auto it = upper_bound(begin(my_vector), end(my_vector), ref, lambda);
```

### Example 2: Reverse-Sorted Vector (Non-Increasing)
```cpp
vector<int> vec{1, 0, -1, -2};
int idx = upper_bound(begin(vec), end(vec), 0, greater<int>()) - begin(vec);
// Output: idx = 2 (points to -1)
```

**LeetCode Applications:**
- Leetcode-981: Time Based Key-Value Store
- Leetcode-744: Find Smallest Letter Greater Than Target
- Leetcode-1351: Count Negative Numbers in a Sorted Matrix

---

## 🔢 Lambda with unordered_map - Function Storage

**Use Case:** Store different operations for different keys

```cpp
unordered_map<string, function<int(int, int)>> mp = {
    { "+", [] (int a, int b) { return a + b; } },
    { "-", [] (int a, int b) { return a - b; } },
    { "*", [] (int a, int b) { return a * b; } },
    { "/", [] (int a, int b) { return a / b; } }
};

int result = mp["+"](1, 2);  // 3
int result = mp["-"](5, 3);  // 2
int result = mp["*"](4, 2);  // 8
int result = mp["/"](8, 2);  // 4
```

**Benefit:** Clean dispatcher pattern for operations

**LeetCode Applications:**
- Leetcode-150: Evaluate Reverse Polish Notation

---

## 🔢 std::set_difference & std::back_inserter

**Purpose:** Find elements in set1 that don't exist in set2

```cpp
set<int> st1{1, 2, 3, 4, 5};
set<int> st2{2, 4, 6};
vector<int> v1;

// Find unique elements in st1
set_difference(begin(st1), end(st1), begin(st2), end(st2), back_inserter(v1));

// Result: v1 = {1, 3, 5}
for(auto x : v1)
    cout << x << " ";
```

**Key Points:**
- `set_difference`: Finds elements in s1 not in s2 (requires sorted containers)
- `back_inserter`: Adds elements to end of container

**LeetCode Applications:**
- Leetcode-2215: Find the Difference of Two Arrays

---

## 📐 std::hypot - Safe Distance Calculation

**Purpose:** Compute √(x² + y²) or √(x² + y² + z²) safely without overflow

### Example 1: Hypotenuse of Right Triangle
```cpp
double x = 3.0, y = 4.0;
double result = std::hypot(x, y);
cout << result;  // 5.0
```

### Example 2: 2D Distance Between Points
```cpp
double x1 = 1, y1 = 2;
double x2 = 4, y2 = 6;
double dist = std::hypot(x2 - x1, y2 - y1);
cout << dist;  // 5.0
```

### Example 3: 3D Distance (C++17)
```cpp
double x = 1, y = 2, z = 2;
double dist3D = std::hypot(x, y, z);
cout << dist3D;  // 3.0
```

**Benefits:**
- ✅ Numerically stable (avoids overflow/underflow)
- ✅ Cleaner than `sqrt(x*x + y*y)`
- ✅ Works with float, double, long double

**LeetCode Applications:**
- Leetcode-812: Largest Triangle Area

---

## 🎯 Quick Reference Cheat Sheet

| STL Function | Purpose | Time Complexity |
|-------------|---------|-----------------|
| `priority_queue` | Min/Max Heap | O(log n) per operation |
| `std::move()` | Efficient transfer | O(1) |
| `accumulate()` | Sum/Aggregate | O(n) |
| `min/max_element()` | Find extremes | O(n) |
| `upper/lower_bound()` | Binary search | O(log n) |
| `rotate()` | Array rotation | O(n) |
| `next_permutation()` | Next permutation | O(n) |
| `stringstream` | String parsing | O(n) |
| `transform()` | Apply operation | O(n) |
| `regex_replace()` | Pattern replace | O(n) |
| `count_if()` | Conditional count | O(n) |
| `copy_if()` | Conditional copy | O(n) |
| `set_difference()` | Set difference | O(n + m) |
| `hypot()` | Safe distance | O(1) |

---

## 💡 Pro Tips

1. **Always use iterators** with STL algorithms for consistency
2. **Prefer lambdas** for comparators - most flexible and readable
3. **Use `back_inserter`** when copying to empty or growing containers
4. **Move semantics** are crucial for performance with large objects
5. **Binary search** functions require sorted containers
6. **Capture variables** in lambdas using `[&]` for references or `[=]` for copies

---

```
╔═══════════════════════════════════════════════════════════════════╗
║  Master C++ STL · Solve LeetCode Problems · Ace Interviews       ║
║  Copy • Paste • Customize • Solve!                               ║
╚═══════════════════════════════════════════════════════════════════╝
```
