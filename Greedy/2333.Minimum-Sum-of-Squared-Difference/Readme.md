### 2333.Minimum-Sum-of-Squared-Difference

这道题和```2233.Maximum-Product-After-K-Increments```非常类似。我们令```nums[i]=abs(nums1[i]-nums2[i])```和```k=k1+k2```，那么就是要在nums里面的元素最多做k次减一的操作，使得所有元素的平方和最小。

将nums降序排列之后，我们必然试图先减小最大值nums[0]。当最大值降到nums[1]的时候，如果还有操作余地，那就试图将两个当前并列最大的元素将至nums[2]，依次执行。所以我们显然可以找到一个位置i，使得不超过k次操作可以将前i个元素都降到nums[i]一样大，条件就是```presum[i] - nums[i]*(i+1) <= k```.

之后我们可能还有多余的操作次数```diff = k - (presum[i] - nums[i]*(i+1))```，这些操作可以让前i+1个元素都再降一些，但又不足以降至nums[i+1]。显然，我们可以将这些diff平均分配给这i+1个元素，这样大家都可以再降```diff/(i+1)```。如果除不尽，那么意味着有部分元素可以再降1. 

最终答案就是将三部分元素的平方和相加即可。