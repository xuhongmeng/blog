LeetCode题目1-two-sum
---
1. 题目 
给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。
你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。
你可以按任意顺序返回答案。

---
示例
示例 1：

输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
示例 2：

输入：nums = [3,2,4], target = 6
输出：[1,2]
示例 3：

输入：nums = [3,3], target = 6
输出：[0,1]

---
分析
1. 暴力法
效率：O(n2)
	暴力法采用的是迭代数组中的每个元素，和其他元素的相加，判断是否等于target的值。
	
    <!--
    1. 如下图所示，
    1. ①值指向第一个值，②指向下一个值
    1. 把①指向值和②指向的值相加是否等于目标值。如果等于目标值，返回下标，结束。
    1. ②向后移动，重复步骤3。
    1. 当②移动到nums的最后。①往后移动一个单位，跳到步骤1
    [//]: #(![Alt text](baoli.png))
    <div align=center><img src="baoli1.jpg" width="  "></div>
    <div align=center><img src="流程图.jpg" width="  "></div>
    <video id="video" controls="" preload="none" >
        <source id="mp4" src="./1-two-sum.mp4" type="video/mp4">
    </video>
    ![](1-two-sum.mp4_20210817_111340.gif)
    -->

1. Hash法
效率:(O(n))
	对数组建立一个hash表，key为target-当前位置的值，value为当前的下标。遍历数组，对于每个值都在hash里面寻找，找到即可。
	对于本题目，可以在把找不到的匹配的数据加入到hash表中。在遍历的过程中建立hash表，不需要两次遍历。

---
1. C++代码
暴力法：
```
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		for (int i{}; i != nums.size(); ++i) {
			for (int j = i + 1; j < nums.size(); ++j) {
				if (nums[i] + nums[j] == target)
					return vector<int>{i, j};
			}
		}
		return vector<int>{0, 0};
	}
};
```
Hash法：
```
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		unordered_map<int, int> m;
		for (int i{}; i != nums.size(); ++i) {
			m.insert(std::pair<int,int>(target-nums[i], i));
		}
		for (int i{}; i != nums.size(); ++i) {
			auto it = m.find(nums[i]);
			if (it != m.end() && i != it->second) {
				return vector<int>{i, it->second};
			}
		}
		return vector<int>{0, 0};
	}
};
```

1. Go代码
暴力法：
```
func twoSum(nums []int, target int) []int {
	for i := 0; i < len(nums)-1; i++ {
		for j := i + 1; j < len(nums); j++ {
			if nums[i]+nums[j] == target {
				return []int{i, j}
			}
		}
	}
	return []int{0, 0}
}
```

Hash法：
```
func twoSum(nums []int, target int) []int {
	d := make(map[int]int)
	for i := 0; i < len(nums); i++ {
		if pos, ok := d[nums[i]]; ok && pos != i {
			return []int{i, pos}
		}
		d[target-nums[i]] = i
	}
	return []int{0, 0}
}
```

1. Java代码
暴力法：
```
class Solution {
    int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length -1; i++) {
            for (int j = i + 1; j < nums.length; j ++) {
                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        return new int[0];
    }
}
```

Hash法：
```
class Solution {
    int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> h = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length -1; i++) {
            if (h.containsKey(nums[i]) && h.get(Integer.valueOf(nums[i])) != Integer.valueOf(i)) {
                return new int[]{i, nums[i]};
            }
            h.put(nums[i], i);
        }
        return new int[0];
    }
}
```

1. Python代码
暴力法：
```
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        for i in range(len(nums)-1):
            j = i + 1
            while j < len(nums):
                if nums[i] + nums[j] == target:
                    return [i, j]
                j = j + 1
        return [0, 0]
```

Hash法
```
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        d = {}
        for i in range(len(nums)):
            if (nums[i] in d.keys()) and (i != d[nums[i]]):
                return [i, d[nums[i]]]
            d[target - nums[i]] = i
        return [0, 0]
```


注意的地方：
1、 数组中同一个元素在答案里不能重复出现