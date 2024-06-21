# Collections

## Collection Types

Don't use non-generic collection types in the `System.Collections` namespace (e.g.: `ArrayList`, `Hashtable`, `Queue`, ...).

Only use collections from the following namespaces:
- `System.Collections.Generic`: 95% of the use cases
- `System.Collections.Concurrent`: used in multi-threaded code 
- `System.Collections.Immutable`

## Big-O notation

A notation used to classify the complexity of algorithms. In other words, it describes how many operations are required to execute certain operations.
For example, sorted from best to worst:
- `O(1)`: constant time
- `O(log n)`: logarithmic
- `O(n)`: linear time
- `O(n.log n)`: linearithmic
- `O(n²)`: quadratic
- `O(c^n)`: expontential

See [wikibooks][(https://en.wikipedia.org/wiki/Big_O_notation](https://en.wikibooks.org/wiki/A-level_Computing_2009/AQA/Problem_Solving,_Programming,_Operating_Systems,_Databases_and_Networking/Problem_Solving/Big_O_Notation)) for more information.

Each collection type has trade-offs, e.g.: sometimes insertion is fast, but lookup slow.
The choice of collection has a huge impact on performance, especially when big datasets are used.

## Generic Collections

See [msdn](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic?view=net-8.0).

- `List<T>`: Store items in order of insertion, use (Quick)sort and binary search for efficient retrieval. Resize is slow. Random access is fast.
- `LinkedList<T>`: Store items linked to previous/next. Resize/insert/delete is fast, random access is slow.
- `Dictionary<TKey, TValue>`: Store values based on a key, all key values must be unique.
- `HashSet<T>`: A set of values, all values must be unique.
- `Queue<T>`: Specialized list, store items in FIFO order (first in, first out).
- `Stack<T>`: Specialized list, store items in LIFO order (last in, first out).
- `SortedList<TKey, TValue>`: Specialized list/dictionary mix, items are stored sorted by key.
- `SortedDictionary<TKey, TValue>`: Specialized dictionary but acts more as a tree, items are stored sorted by key. Differs from SortedList in insertion/removal speed and memory use.
- `SortedSet<T>`: Store items in sorted order, no duplicates can exist.

## Concurrent Collections

- `ConcurrentBag<T>`: thread-safe, unordered collection of objects
- `ConcurrentDictionary<TKey, TValue>`: thread-safe dictionary
- `ConcurrentQueue<T>`: thread-safe queue
- `ConcurrentStack<T>`: thread-safe stack

## Immutable Collections

Immutable variants of dictionary, hashset, list, queue, stack, ... .
In other words: collections that can only be initialized, values cannot be added/removed.

## Other Collections

There are lot's of other collections, many of them are not implemented in the default .NET library but require your own implementation or third party NuGet packages.

e.g.:
- tree
- binary tree (btree): useful for database indices and filesystems
- red/black tree/AVL tree: self balancing binary search trees
- segment tree: useful when dealing with range queries
- trie (prefix tree): efficient retrieval of elements with a common prefix
- suffix array: used for string matching and search problems
- LRU cache: least recently used cache: useful when caching data when dealing with fixed size limits
- Deques (double ended queue): used to efficiently add/remove elements from both ends of the collection
- Adjaceny list/matrix: used in combination with graph data structures
- R-tree: specialized tree structure for multidimensional data (e.g. geo coords)