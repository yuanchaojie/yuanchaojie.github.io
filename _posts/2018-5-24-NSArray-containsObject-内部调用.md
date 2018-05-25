### 哈希wiki 引用
***

> 在计算中，散列表（哈希映射）是一种实现关联数组抽象数据类型的数据结构，这种结构可以将键映射到值。哈希表使用哈希函数来计算索引到一个桶或槽的阵列中，从中可以找到所需的值。
> 
> In computing, a hash table (hash map) is a data structure which implements an associative array abstract data type, a structure that can map keys to values. A hash table uses a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.

> 理想情况下，散列函数会将每个键分配给一个独特的桶，但是大多数散列表设计使用了不完美的散列函数，这可能会导致散列冲突，其中散列函数为多个键生成相同的索引。必须以某种方式解决这种冲突。
> 
> Ideally, the hash function will assign each key to a unique bucket, but most hash table designs employ an imperfect hash function, which might cause hash collisions where the hash function generates the same index for more than one key. Such collisions must be accommodated in some way.


> 在尺寸合理的哈希表中，每次查找的平均成本（指令数量）与存储在表中的元素数量无关。许多散列表设计还允许以每次操作的（摊销[2]）恒定平均成本任意插入和删除键值对。[3] [4]

> In a well-dimensioned hash table, the average cost (number of instructions) for each lookup is independent of the number of elements stored in the table. Many hash table designs also allow arbitrary insertions and deletions of key-value pairs, at (amortized[2]) constant average cost per operation.[3][4]

> 在许多情况下，散列表结果平均来说比搜索树或任何其他表查找结构更高效。由于这个原因，它们被广泛用于多种计算机软件中，特别是关联数组，数据库索引，缓存和集合

> In many situations, hash tables turn out to be on average more efficient than search trees or any other table lookup structure. For this reason, they are widely used in many kinds of computer software, particularly for associative arrays, database indexing, caches, and sets.
> 


NSObject isEqual:方法描述(NSArray containsObject: 内部调用了isEqual 方法)

> This method defines what it means for instances to be equal. For example, a container object might define two containers as equal if their corresponding objects all respond YES to an isEqual: request. See the NSData, NSDictionary, NSArray, and NSString class specifications for examples of the use of this method.



> If two objects are equal, they must have the same hash value. This last point is particularly important if you define isEqual: in a subclass and intend to put instances of that subclass into a collection. Make sure you also define hash in your subclass.






