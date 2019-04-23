

347. Top K Frequent Elements
https://leetcode.com/problems/top-k-frequent-elements/

```Java

class Pair{
    int num;
    int count;
    public Pair(int num, int count){
        this.num=num;
        this.count=count;
    }
}

 class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        //count the frequency for each element
        HashMap<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++){
            if(map.containsKey(nums[i])){
                map.put(nums[i], map.get(nums[i])+1);
            }else{
                map.put(nums[i], 1);
            }
        }

        // create a min heap
        PriorityQueue<Pair> queue = new PriorityQueue<>(Comparator.comparing(Pair->Pair.count));

        //maintain a heap of size k.
        for(Map.Entry<Integer, Integer> entry: map.entrySet()){
            Pair p = new Pair(entry.getKey(), entry.getValue());
            queue.offer(p);
            if(queue.size()>k){
                queue.poll();
            }
        }

        //get all elements from the heap
        List<Integer> result = new ArrayList<>();
        while(queue.size()>0){
            result.add(queue.poll().num);
        }

        //reverse the order
        Collections.reverse(result);

        return result;
    }
}

```

//用hashmap存，再排序一遍，最后输出前k个.https://blog.csdn.net/Jin_Kwok/article/details/51549322
//Java中提供了HashMap类，它实现了Map接口，HashMap是一个泛型类（HashMap<key,value>），可以用来存储键/值对，为了统计数组个元素的频次，我们可以把元素数值作为“键”，对应元素出现的次数作为“值”，如此，我们只需要对数组进行一次遍历就可以得到一张包含不同数组元素和对应出现频次的“映射表”。
//方法一：Priorityqueue: 用一个minheap, 维持长度为K, 这样最后留下的内容就是最大的k 个元素。
//方法二：桶排序编号大的桶中元素出现的频次高，因此，我们“逆序”(先取桶编号大的桶的元素)获取桶中数据，直到获取数据的个数等于k，我们将当前桶的元素取尽（同一个桶中元素出现的频次相等）,然后停止取数据，完成！
//时间复杂度为O(nlongn)，空间复杂度为O(n)。
