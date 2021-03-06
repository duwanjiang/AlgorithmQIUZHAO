# 1. 布隆过滤器和LRU Cache
## 1.1 [布隆过滤器（Bloom Filter）](https://www.cnblogs.com/cpselvis/p/6265825.html)
布隆过滤器（Bloom Filter）的核心实现是一个超大的位数组和几个哈希函数。假设位数组的长度为m，哈希函数的个数为k 。
具体的操作流程：假设集合里面有3个元素{x,y,z}，哈希函数的个数为3。首先将位数组进行初始化，将里面每个位都设置为0。对于集合里面的每个元素，将元素依次通过3个哈希函数进行映射，每次映射都会产生一个哈希值，这个值对应位数组上面的一个点，然后将位数组对应的位置标记为1。查询W元素是否存在集合中的时候，同样的方法将W通过哈希映射到位数组上的3个点。如果3个点的其中有一个点不为1，则可以判断该元素一定不存在集合中。反之，如果3个点都为1，则该元素可能存在集合中。注意：此处不能判断该元素是否一定存在集合中，可能存在一定的误判率。
### 1.1.1 Bloom Filter vs Hash Table 
一个很长的二进制向量和一系列随机映射函数。布隆过滤器可以用于检索一个元素是否在一个集合中。
1. 优点：是空间效率和查询时间都远远超过一般的算法。
2. 缺点：是有一定的误识别率和删除困难。

### 1.1.2 实现源码
https://github.com/lovasoa/bloomfilter/blob/master/src/main/java/BloomFilter.java

## 1.2 LRU Cache （Least recently used）
1. 两个要素：大小和替换策略
2. 数据结构：HashTable + Double LinkedList
3. 时间复杂度：O(1) 查询，O(1) 修改、更新

# 2. [排序算法](https://www.cnblogs.com/onepixel/p/7674659.html)
* 九种排序算法动画：https://www.bilibili.com/video/av25136272
* 15种排序算法动画：https://www.bilibili.com/video/av63851336
## 2.1 初级排序 - O(n^2)
### 2.1.1 选择排序（Selection Sort）

![](selectionSort.gif)

每次找最小值，然后放到待排序数组的起始位置。
### 2.1.2 插入排序（Insertion Sort）

![](insertionSort.gif)

从前到后逐步构建有序序列；对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。
### 2.1.3 冒泡排序（Bubble Sort）

![](BubbleSort.gif)

嵌套循环，每次查看相邻的元素，如果逆序，则交换。
## 2.2 高级排序 - O(N*LogN)
### 2.2.1 快速排序（Quick Sort）

![](QuickSort.gif)

数组取标杆pivot，将小元素放在pivot左边，大元素放右侧，然后依次对左边和右边的子数组继续快排；以达到整个序列有序。
[代码示例:](https://shimo.im/docs/TX9bDbSC7C0CR5XO/read)
``` java
// 调用方法：quickSort(a, 0, a.length - 1);

public static void quickSort (int[] array, int begin, int end){
    if (end <= begin) return;
    int pivot = partition(array, begin, end);
    quickSort(array, begin, pivot - 1);
    quickSort(array, pivot - 1, end);
}

static int partition(int[] a, int begin, int end) {
    // pivot：标杆位置，counter：小于pivot的元素个数
    int pivot = end, counter = begin;
    for (int i = begin; i < end; i++){
        if (a[i] < a[pivot]) {
            // 将小于标杆的元素放到数组左边
            int temp = a[counter]; a[counter] = a[i]; a[i] = temp; 
            counter++;
        }
    }
    //将pivot放置到数组排序后该到的位置
    int temp = a[pivot]; a[pivot] = a[counter]; a[counter] = temp;  
    return counter;
}
```

### 2.2.2 归并排序（Merge Sort） -- 分治

![](MergeSort.gif)

1. 把长度为n的输入序列分成两个长度为n/2的子序列
2. 对这两个子序列分别采用归并排序
3. 将两个排序好的子序列合并成一个最终的排序序列

[代码示例:](https://shimo.im/docs/sDXxjjiKf3gLVVAU/read)
``` java
public static void mergeSort (int[] array, int left, int right) {
    if(right <= left) return;
    int mid = (left + right) >> 1;
    mergeSort(array, left, mid);
    mergeSort(array, mid + 1, right);
    merge(array, left, mid, right);
}
public static void merge (int[] arr, int left, int mid, int right) {
    int[] temp = new int[right - left + 1]; // 中间数组
    int i = left, j = mid + 1, k = 0;
    // 将2个子数组的元素排序放入temp数组
    while (i < mid && j <= right) temp[k++] = arr[i] <= arr[j] ? arr[i++] : arr[j++]; 
    while (i <= mid) temp[k++] = arr[i++]; // 将mid前子数组剩余元素放入temp数组
    while (j <= right) temp[k++] = arr[j++]; // 将mid后子数组剩余元素放入temp数组
    // 拷贝temp数组到arr
    // System.arraycopy(temp, 0, arr, left, temp.length);
    for (int p = 0; p < temp.length; p++) {
        arr[left + p] = temp[p];
    }
}
```

### 2.2.3 堆排序（Heap Sort） -- 堆插入O(logN)，取最大/最小O(1)

![](HeapSort.gif)

1. 数组元素依次建立小顶堆
2. 依次取堆顶元素，并删除

[代码示例](https://shimo.im/docs/M2xfacKvwzAykhz6/read):
``` java
public static void heapSort(int[] array) {
    if (array.length == 0) return;
    int length = array.length;
    for (int i = length / 2 - 1; i >= 0; i--) heapify(array, length, i);
    for (int i = length - 1; i >= 0; i--) {
        int temp = array[0]; array[0] = array[i]; array[i] = temp;
        heapify(array, i, 0);
    }
}

static void heapify(int[] array, int length, int i) {
    int left = 2 * i + 1, right = 2 * i + 2; // 左右子树位置
    int largest = i;
    if (left < length && array[left] > array[largest]) {
        largest = left;
    }
    if (right < length && array[right] > array[largest]) {
        largest = right;
    }

    if (largest != i) {
        int temp = array[i]; array[i] = array[largest]; array[largest] = temp;
        heapify(array, length, largest);
    }
}
```

## 2.3 特殊排序 - O(n)
### 2.3.1 计数排序（Counting Sort）

![](CountingSort.gif)

计数排序要求输入的数据必须是有特定范围的整数。将输入的数据值转化为键存储在额外开辟的数组空间中，然后依次把计数大于1的填充回原数组。
### 2.3.2 桶排序（Bucket Sort）

![](BucketSort.png)

假设输入数据服从平均分布，将数据分到有限数量的桶里，每个桶再分别排序（有可能再使用别的排序算法或是以递归方式继续使用桶排序进行排）
1. 设置一个定量的数组当作空桶
2. 遍历输入数据，并且把数据一个一个放到对应的桶里去
3. 对每个不是空的桶进行排序
4. 从不是空的桶里把排好序的数据拼接起来
### 2.3.3 基数排序（Radix Sort）

![](RadixSort.gif)

基数排序是按照低位先排序，然后收集；再按照高位排序，然后再收集；依次类推，直到最高位。有时候有些属性是有优先级顺序的，先按低优先级排序，再按高优先级排序。

# 3 字符串匹配算法
## 3.1 Boyer-Moore算法
参考：https://www.ruanyifeng.com/blog/2013/05/boyer-moore_string_search_algorithm.html
## 3.2 Sunday算法
参考：https://blog.csdn.net/u012505432/article/details/52210975
## 3.3 暴力算法（brute force）
代码示例：https://shimo.im/docs/8G0aJqNL86wWrPUE/read
## 3.4 Rabin-karp算法
代码示例：https://shimo.im/docs/1wnsM7eaZ6Ab9j9M/read
## 3.5 KMP算法
学习视频：https://www.bilibili.com/video/av11866460?from=search&seid=17425875345653862171
参考：http://www.ruanyifeng.com/blog/2013/05/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm.html