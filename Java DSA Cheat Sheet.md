# Java DSA Cheat Sheet 

## If Ctrl+Space is Not Available

``` java
System.out.println(obj.getClass());

import java.lang.reflect.Method;
for(Method m : obj.getClass().getMethods()){
    System.out.println(m.getName());
}
```

## Input

### Scanner

``` java
Scanner sc = new Scanner(System.in);
int n=sc.nextInt();
long l=sc.nextLong();
double d=sc.nextDouble();
String word=sc.next();
String line=sc.nextLine();
char ch=sc.next().charAt(0);
boolean b=sc.nextBoolean();
```
-----
```
Scanner sc = new Scanner(System.in);

// Integer
int x = sc.nextInt();

// Long
long l = sc.nextLong();

// Double
double d = sc.nextDouble();

// String (one word)
String s = sc.next();

// Full line
String line = sc.nextLine();

// Character
char ch = sc.next().charAt(0);

// Integer array
int[] arr = new int[n];
for(int i = 0; i < n; i++)
    arr[i] = sc.nextInt();

// String array
String[] str = new String[n];
for(int i = 0; i < n; i++)
    str[i] = sc.next();

// ArrayList<Integer>
ArrayList<Integer> list = new ArrayList<>();
for(int i = 0; i < n; i++)
    list.add(sc.nextInt());

// ArrayList<String>
ArrayList<String> words = new ArrayList<>();
for(int i = 0; i < n; i++)
    words.add(sc.next());

// Character array
char[] chars = sc.next().toCharArray();
```

### Read Array

``` java
int n=sc.nextInt();
int[] arr=new int[n];
for(int i=0;i<n;i++) arr[i]=sc.nextInt();
```

### BufferedReader

``` java
BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
int n=Integer.parseInt(br.readLine());
String s=br.readLine();
```

### StringTokenizer

``` java
StringTokenizer st=new StringTokenizer(br.readLine());
int a=Integer.parseInt(st.nextToken());
int b=Integer.parseInt(st.nextToken());
```




# Cheat Sheet

## 1. String

`length charAt substring indexOf lastIndexOf contains startsWith endsWith equals equalsIgnoreCase compareTo replace replaceAll split trim toUpperCase toLowerCase toCharArray valueOf matches repeat isEmpty isBlank concat join`


``` java
String s = "Hello";
s.length();
s.charAt(i);
s.substring(start);
s.substring(start, end);
s.indexOf('a');
s.lastIndexOf('a');
s.contains("ll");
s.equals(str);
s.equalsIgnoreCase(str);
s.compareTo(str);
s.startsWith("He");
s.endsWith("lo");
s.toUpperCase();
s.toLowerCase();
s.trim();
s.replace('a','b');
s.replaceAll(regex,"");
s.split(" ");
s.toCharArray();
```

## 2. Character

`isLetter isDigit isLetterOrDigit isWhitespace isUpperCase isLowerCase toUpperCase toLowerCase getNumericValue compare`

``` java
char c='A';
Character.isLetter(c);
Character.isDigit(c);
Character.isLetterOrDigit(c);
Character.isWhitespace(c);
Character.isUpperCase(c);
Character.isLowerCase(c);
Character.toUpperCase(c);
Character.toLowerCase(c);
Character.getNumericValue(c);
```

## 3. StringBuilder

`append insert delete deleteCharAt replace reverse length charAt setCharAt toString`

``` java
StringBuilder sb = new StringBuilder();
sb.append("abc");
sb.insert(1,"X");
sb.delete(1,3);
sb.deleteCharAt(0);
sb.replace(0,2,"Hi");
sb.reverse();
sb.length();
sb.charAt(i);
sb.setCharAt(i,'A');
sb.toString();
```

## 4. Arrays

`Arrays.sort Arrays.binarySearch Arrays.fill Arrays.equals Arrays.copyOf Arrays.copyOfRange Arrays.toString`

``` java
Arrays.sort(arr);
Arrays.binarySearch(arr,key);
Arrays.fill(arr,0);
Arrays.equals(arr1,arr2);
Arrays.copyOf(arr,n);
Arrays.toString(arr);
```

## 5. ArrayList

`add get set remove contains size clear isEmpty indexOf`

``` java
ArrayList<Integer> list = new ArrayList<>();
list.add(x);
list.add(index,x);
list.get(i);
list.set(i,x);
list.remove(i);
list.remove(Integer.valueOf(x));
list.size();
list.contains(x);
list.isEmpty();
list.clear();
Collections.sort(list);
Collections.reverse(list);
```

## 6. HashMap

`put putIfAbsent get getOrDefault containsKey containsValue remove replace keySet values entrySet`

``` java
HashMap<Integer,Integer> map = new HashMap<>();
map.put(key,val);
map.get(key);
map.getOrDefault(key,0);
map.containsKey(key);
map.containsValue(val);
map.remove(key);
map.size();
map.isEmpty();
for(Integer key: map.keySet()){}
for(Integer val: map.values()){}
for(Map.Entry<Integer,Integer> e: map.entrySet()){
 e.getKey(); e.getValue();
}
```

## 7. HashSet

`add remove contains size clear isEmpty`

``` java
HashSet<Integer> set = new HashSet<>();
set.add(x);
set.remove(x);
set.contains(x);
set.size();
set.isEmpty();
```

## 8. Stack

`push pop peek search isEmpty`

``` java
Stack<Integer> st = new Stack<>();
st.push(x);
st.pop();
st.peek();
st.isEmpty();
st.size();
```

## 9. Queue

`offer poll peek remove element`

``` java
Queue<Integer> q = new LinkedList<>();
q.offer(x);
q.poll();
q.peek();
q.isEmpty();
q.size();
```

## 10. PriorityQueue

`offer poll peek Collections.reverseOrder`

``` java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.offer(x);
pq.poll();
pq.peek();
PriorityQueue<Integer> max = new PriorityQueue<>(Collections.reverseOrder());
```

## 11. Math

`max min abs pow sqrt ceil floor round random`


``` java
Math.max(a,b);
Math.min(a,b);
Math.abs(x);
Math.pow(a,b);
Math.sqrt(x);
Math.ceil(x);
Math.floor(x);
Math.round(x);
```

## 12. Common Loops

``` java
for(int x: arr){}
for(int i=0;i<arr.length;i++){}
for(int i=0;i<s.length();i++){
 char c=s.charAt(i);
}
```

## 13. Useful Conversions

``` java
String.valueOf(123);
Integer.parseInt("123");
Long.parseLong("123");
Double.parseDouble("12.5");
char[] ch=s.toCharArray();
String s=new String(ch);
```

## 14. Sorting

``` java
Arrays.sort(arr);
Collections.sort(list);
Collections.reverse(list);
Collections.sort(list,(a,b)->a-b);
```

## 15. TreeMap

`put get remove containsKey firstKey lastKey higherKey lowerKey ceilingKey floorKey subMap headMap tailMap firstEntry lastEntry pollFirstEntry pollLastEntry keySet values entrySet`

- **Data Structure**: Self-balancing Red-Black Tree (sorted by keys in natural order or custom `Comparator`).
- **Time Complexity**:
  - `put`, `get`, `remove`, `containsKey`: `O(log N)`
  - `firstKey`, `lastKey`, `higherKey`, `lowerKey`, `ceilingKey`, `floorKey`: `O(log N)`
- **Key Characteristics**:
  - Keys are strictly sorted. Does **NOT** allow `null` keys when using natural ordering.
  - Allows `null` values.

### Basic Operations & Key Navigation
``` java
TreeMap<Integer, String> map = new TreeMap<>();
map.put(10, "Ten");
map.put(20, "Twenty");
map.put(5, "Five");
map.put(15, "Fifteen");

map.get(10);                        // "Ten" - O(log N)
map.containsKey(20);                // true - O(log N)
map.remove(5);                      // Removes key 5 and returns value - O(log N)

// Min / Max Key queries
map.firstKey();                     // 5 (smallest key)
map.lastKey();                      // 20 (largest key)

// Navigation Methods (Logarithmic Search)
map.higherKey(10);                  // 15 -> strictly greater (> 10)
map.lowerKey(10);                   // 5  -> strictly lower (< 10)
map.ceilingKey(10);                 // 10 -> smallest key >= 10
map.floorKey(12);                   // 10 -> largest key <= 12

// Entry-based queries (returns Map.Entry<K,V>)
Map.Entry<Integer, String> first = map.firstEntry(); // 5="Five"
first.getKey();                     // 5
first.getValue();                   // "Five"

// Polling (Extract & Remove)
map.pollFirstEntry();               // Removes & returns entry with lowest key (5="Five")
map.pollLastEntry();                // Removes & returns entry with highest key (20="Twenty")
```

### Range Queries (Sub-views)
``` java
// Range views - O(1) creation time (backed by original map)
map.subMap(5, 20);                  // Keys in range [5, 20)
map.subMap(5, true, 20, true);      // Keys in range [5, 20] (inclusive)
map.headMap(15);                    // Keys strictly < 15
map.headMap(15, true);              // Keys <= 15
map.tailMap(10);                    // Keys >= 10
```

### Custom Ordering & Common DSA Patterns
``` java
// 1. Descending Order TreeMap
TreeMap<Integer, String> descMap = new TreeMap<>(Collections.reverseOrder());

// 2. Custom Comparator for 2D Coordinate / Multi-field keys
TreeMap<int[], String> pointMap = new TreeMap<>((a, b) -> a[0] != b[0] ? a[0] - b[0] : a[1] - b[1]);

// 3. Dynamic Multi-set / Frequency Map with Order
TreeMap<Integer, Integer> freqMap = new TreeMap<>();
freqMap.put(x, freqMap.getOrDefault(x, 0) + 1); // Add item
// Decrement / Remove pattern
if (freqMap.get(x) == 1) freqMap.remove(x);
else freqMap.put(x, freqMap.get(x) - 1);
```

## 16. TreeSet

`add remove contains first last higher lower ceiling floor subSet headSet tailSet pollFirst pollLast size isEmpty descendingSet`

- **Data Structure**: NavigableSet backed by a `TreeMap` (Red-Black Tree).
- **Time Complexity**:
  - `add`, `remove`, `contains`: `O(log N)`
  - `first`, `last`, `higher`, `lower`, `ceiling`, `floor`: `O(log N)`
- **Key Characteristics**:
  - Elements are unique and maintained in sorted order.
  - Does **NOT** allow `null` elements in natural ordering.

### Basic Operations & Element Navigation
``` java
TreeSet<Integer> set = new TreeSet<>();
set.add(10);
set.add(20);
set.add(5);
set.add(15);

set.contains(15);                   // true - O(log N)
set.remove(10);                     // Removes 10 - O(log N)

// Min / Max element queries
set.first();                        // 5 (smallest element)
set.last();                         // 20 (largest element)

// Navigation Methods
set.higher(10);                     // 15 -> strictly greater (> 10)
set.lower(10);                      // 5  -> strictly lower (< 10)
set.ceiling(10);                    // 10 -> smallest element >= 10
set.floor(12);                      // 10 -> largest element <= 12

// Polling (Extract & Remove)
set.pollFirst();                    // Removes & returns 5 (lowest element)
set.pollLast();                     // Removes & returns 20 (highest element)

// Reverse View
NavigableSet<Integer> reverseSet = set.descendingSet(); // View in reverse order
```

### Range Queries (Sub-views)
``` java
// Range views - O(1) creation time (backed by original set)
set.subSet(5, 20);                  // Elements in range [5, 20)
set.subSet(5, true, 20, true);      // Elements in range [5, 20] (inclusive)
set.headSet(15);                    // Elements strictly < 15
set.tailSet(10);                    // Elements >= 10
```

### Custom Comparators & Common DSA Patterns
``` java
// 1. Descending Order TreeSet
TreeSet<Integer> maxSet = new TreeSet<>(Collections.reverseOrder());

// 2. Custom Object Sorting (e.g. Intervals [start, end])
TreeSet<int[]> intervalSet = new TreeSet<>((a, b) -> a[0] != b[0] ? a[0] - b[0] : a[1] - b[1]);

// 3. Sliding Window / Closest Value Search
// Find smallest element >= target - x
Integer val = set.ceiling(target - x);
if (val != null && val <= target + x) {
    // Found element within window range [target - x, target + x]
}
```

## 17. Collections

`sort reverse max min frequency swap shuffle binarySearch fill copy replaceAll disjoint nCopies singletonList emptyList`

- **Overview**: Static utility class providing algorithms for `Collection` and `List` implementations.

### Sorting & Reversing Algorithms
``` java
List<Integer> list = new ArrayList<>(Arrays.asList(3, 1, 4, 1, 5, 9));

// Ascending sort - O(N log N) using Timsort
Collections.sort(list);

// Descending sort
Collections.sort(list, Collections.reverseOrder());

// Custom Comparator Sort (e.g. by String length or custom object properties)
Collections.sort(stringList, (a, b) -> a.length() - b.length());
Collections.sort(pairList, (a, b) -> a[0] != b[0] ? Integer.compare(a[0], b[0]) : Integer.compare(a[1], b[1]));

// Reverse List in-place - O(N)
Collections.reverse(list);

// Random Shuffle - O(N)
Collections.shuffle(list);
```

### Searching & Querying
``` java
// Min / Max elements - O(N)
int maxVal = Collections.max(list);
int minVal = Collections.min(list);

// Frequency count - O(N)
int count = Collections.frequency(list, 1); // Returns count of 1 in list

// Binary Search - O(log N) for ArrayList / random access List
// NOTE: List MUST be sorted in ascending order before calling binarySearch!
int idx = Collections.binarySearch(list, 4); 
// Returns positive index if found.
// If NOT found, returns (-(insertion point) - 1). 
// To get insertion point when key is missing: int insertIdx = -idx - 1;

// Check if two collections share NO common elements - O(N)
boolean noCommon = Collections.disjoint(list1, list2);
```

### Modification & Utility Helpers
``` java
// Swap elements at index i and j - O(1)
Collections.swap(list, 0, 3);

// Fill entire list with a specific value - O(N)
Collections.fill(list, 0);

// Replace all occurrences of oldVal with newVal - O(N)
Collections.replaceAll(list, 1, 99);

// Immutable / Helper Collections
List<Integer> zeros = Collections.nCopies(5, 0);       // [0, 0, 0, 0, 0] (immutable list)
List<String> single = Collections.singletonList("A");  // Immutable single-item list
List<Integer> empty  = Collections.emptyList();          // Immutable empty list
```

## 18. Frequently or General Used DSA Patterns

-   Two Pointers
-   Sliding Window
-   Binary Search
-   BFS
-   DFS
-   Prefix Sum
-   Recursion

### Two Pointers

``` java
int left=0,right=arr.length-1;
```

### Sliding Window

``` java
int start=0;
for(int end=0;end<n;end++){
  while(condition){
    start++;
  }
}
```

### Binary Search

``` java
int low=0,high=n-1;
while(low<=high){
 int mid=low+(high-low)/2;
}
```

# Must-Memorize Methods

-   String: length, charAt, substring, contains, indexOf, split,
    replace, equals, compareTo, toCharArray
-   Character: isLetter, isDigit, isLetterOrDigit, isWhitespace,
    isUpperCase, isLowerCase, toUpperCase, toLowerCase
-   Arrays: sort, binarySearch
-   Collections: sort, reverse
-   ArrayList: add, get, set, remove, size
-   HashMap: put, get, getOrDefault, containsKey
-   Queue: offer, poll, peek
-   Stack: push, pop, peek

Focus for LSET: Arrays, Strings, Character, HashMap, ArrayList, Stack,
Queue, Two Pointers, Sliding Window, Binary Search, Recursion.

