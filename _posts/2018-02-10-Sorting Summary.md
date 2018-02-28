---
layout: post  
title: 编程算法 Sorting Summary
subtitle: 
header-img: "img/1.jpg"
categories: [blog ]  
tags: [leetcode]
description: 「Leetcode 解题思路」  
---  




#### 1. Bubble sort

It has to run for n times, each time, it go through all the element and swap the two adjacent elements if their order is wrong. Thus in the end of each run, the last element would be guarenteed the largest. so we reduce our sorting size by one. And we would run until all the elements are sorted.

Running time: worst case O(N^2) when the list is reverse-ordered. best case O(N) when the list is corrected-ordered. Need O(1) space.

```
private static int[] bubbleSort(int[] list){
		for(int i = 0; i < list.length-1; i++){
			for(int j = 0; j < list.length-1-i; j++){
				if(list[j] > list[j+1]){
					int tmp = list[j];
					list[j] = list[j+1];
					list[j+1] = tmp;
				}
			}
		}
		return list;
}
```

#### 2. Selection Sort

选择排序无疑是最简单直观的排序。它的工作原理如下。

**步骤：**

1. 在未排序序列中找到最小（大）元素，存放到排序序列的起始位置。
2. 再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。
3. 以此类推，直到所有元素均排序完毕。

Selection sort is to run through the list to find out the smallest element and place it at place 0, and then find the second smallest element and place it at place 1 and so on.

Running time: O(n^2). Space: O(1)

```
private static int[] selectionSort(int[] nums){
		for(int i = 0; i < nums.length-1; i++){
			int min = nums[i];
			for(int j = i+1; j < nums.length; j++){
				if(nums[j] < min){
					nums[i] = nums[j];
					nums[j] = min;
					min = nums[i];
				}
			}
		}
		return nums;
	}
```



#### 3. Insertion Sort

**介绍：**

插入排序的工作原理是，对于每个未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。

**步骤：**

1. 从第一个元素开始，该元素可以认为已经被排序
2. 取出下一个元素，在已经排序的元素序列中从后向前扫描
3. 如果被扫描的元素（已排序）大于新元素，将该元素后移一位
4. 重复步骤3，直到找到已排序的元素小于或者等于新元素的位置
5. 将新元素插入到该位置后
6. 重复步骤2~5

Split the array into two parts: sorted and unsorted, each time, finds the first element in unsorted and put it to the correct place in sorted array side and grow the sorted size by 1. Keep doing this until the whole array is sorted.

Running time: O(n^2) Space: O(1)

```
private static int[] insertionSort(int[] nums){
		for(int i = 0; i < nums.length-1; i++){
			for(int j = i+1; j > 0; j--){
				if(nums[j]>nums[j-1])break;
				int tmp = nums[j];
				nums[j] = nums[j-1];
				nums[j-1] = tmp;
			}
		}
		return nums;
	}
```



#### 4. Shell Sort

**介绍：**

希尔排序，也称递减增量排序算法，实质是分组插入排序。由 Donald Shell 于1959年提出。希尔排序是非稳定排序算法。

希尔排序的基本思想是：将数组列在一个表中并对列分别进行插入排序，重复这过程，不过每次用更长的列（步长更长了，列数更少了）来进行。最后整个表就只有一列了。将数组转换至表是为了更好地理解这算法，算法本身还是使用数组进行排序。

First chose a int n and group the items by n. Then sort each group. Then combine everything and chose a different and smaller n and sort again. Continues to do this until everything is sorted.

```
private static int[] shellSort(int[] nums){
		int gap = 1, i,j,len = nums.length;
		int tmp;
		while(gap < len/3) // 初始步长 这个可能比较优秀
			gap = gap*3+1;
		for(; gap >0; gap/=3){
			for(i = gap; i < len; i++){
				tmp = nums[i];
				for(j = i - gap; j >= 0 && nums[j]>tmp; j-=gap)
					nums[j+gap] = nums[j];
				nums[j+gap] = tmp;
			}
		}
		return nums;	
	}
```

 

#### 5. Merge Sort

归并排序是采用分治法的一个非常典型的应用。`归并`排序的思想就是先递`归`分解数组，再`合`并数组。

先考虑合并两个有序数组，基本思路是比较两个数组的最前面的数，谁小就先取谁，取了后相应的指针就往后移一位。然后再比较，直至一个数组为空，最后把另一个数组的剩余部分复制过来即可。

再考虑递归分解，基本思路是将数组分解成`left`和`right`，如果这两个数组内部数据是有序的，那么就可以用上面合并数组的方法将这两个数组合并排序。如何让这两个数组内部是有序的？可以再二分，直至分解出的小组只含有一个元素时为止，此时认为该小组内部已有序。然后合并排序相邻二个小组即可。



```
private static int[] merge(int[] a, int[] b){
		int[] c = new int[a.length+b.length];
		int i = 0, j = 0, k = 0;
		while(i < a.length && j < b.length)
			c[k++] = (a[i]<b[j])?a[i++]:b[j++];
		while(i<a.length)c[k++]=a[i++];
		while(j<b.length)c[k++]=b[j++];
		return c;
	}

	private static int[] mergeSort(int[] nums){
		int l = nums.length;
		if(l < 2) return nums;
		int[] a = new int[l/2];
		int[] b = new int[l - l/2];
		a = Arrays.copyOfRange(nums, 0, l/2);
		b = Arrays.copyOfRange(nums, l/2, l);
		return merge(mergeSort(a),mergeSort(b));
	}
```



#### 6. Quicksort

Find a pivot, and divide the list into two sets, smaller and larger than pivot. Sort the two sets by recursively calling quicksort.

```
private static void quicksort(int[] nums, int low, int high){
		if(nums == null || nums.length == 0)return;
		if(low>=high)return;
		int pivot = nums[(high+low)/2];
		int i = low, j = high;
		while(i <= j){
			while(nums[i]<pivot)i++;
			while(nums[j]>pivot)j--;
			if(i<=j){
				int tmp = nums[i];
				nums[i++] = nums[j];
				nums[j--] = tmp;
			}
		}
		if(low<j)quicksort(nums,low,j);
		if(high>i)quicksort(nums,i,high);
	}
```

#### 7. Bucket Sort

**桶排序 (Bucket sort)**或所谓的**箱排序**，是一个排序算法，工作的原理是将数组分到有限数量的桶子里。每个桶子再个别排序（有可能再使用别的排序算法或是以递归方式继续使用桶排序进行排序）。桶排序是鸽巢排序的一种归纳结果。当要被排序的数组内的数值是均匀分配的时候，桶排序使用线性时间（Θ（*n*））。但桶排序并不是 比较排序，他不受到 O(n log n) 下限的影响。

桶排序以下列程序进行：

1. 设置一个定量的数组当作空桶子。
2. 寻访序列，并且把项目一个一个放到对应的桶子去。
3. 对每个不是空的桶子进行排序。
4. 从不是空的桶子里把项目再放回原来的序列中。


对该算法简单分析，如果数据是期望平均分布的，则每个桶中的元素平均个数为N/M。如果对每个桶中的元素排序使用的算法是快速排序，每次排序的时间复杂度为O(N/Mlog(N/M))。
则总的时间复杂度为O(N)+O(M)O(N/Mlog(N/M)) = O(N+ Nlog(N/M)) = O(N + NlogN - NlogM)。
当M接近于N是，桶排序的时间复杂度就可以近似认为是O(N)的。就是桶越多，时间效率就越高，
而桶越多，空间却就越大，由此可见时间和空间是一个矛盾的两个方面







### Sorting 二刷总结

1. Bubble sort：（依次sort最右到最左）

   2个for loop，外端0到len-1循环表示目前sort的长度，内端0到len-1-i循环，表示bubble swap的前一位位置。inside for loop swap if 后<前

2. Insertion Sort：（依次sort最左到最右）

   2个for loop，外端1到len循环表示pivot point（pivot左边sort完毕），内端i-1到0循环 表示找寻pivot在sort array中应该插入的位置

   inside for loop, 若左小于右则break，else swap。

3. Selection Sort：（依次sort最左到最右）

   两个for loop，外端0到len-1循环表示要找到该位的value，内端i到len-1循环表示历遍未sort部分求最小，inside for loop：update min when 找到value < min且swap。

4. Merge sort：（divide and conquer）

   若list足够小，直接return

   else，分成两个subset分别sort，then merge

5. Quick sort：pivoting （int low, int high, int[] nums）

   选pivot为中点

   while（左pointer <= 右pointer）//为了确保停止时候左pointer>右pointer

   ​	while loop寻找左侧那个大于pivot的value

   ​	while loop寻找右侧那个小于pivot的value

   ​	若左<=右 则swap 二者

   此时low到左都小于pivot，右到high都大于pivot。分别quicksort左右。

6. Bucket sort 分成n个bucket and put value in。当N=M时 O（N）

7. Shell sort - 最不熟悉 =。=



merge 3 lists

tree sum