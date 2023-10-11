给定两个大小分别为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的 中位数 。

class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    	vector<int>nums;
    	int i=0,j=0;
        int m = nums1.size(),  n = nums2.size();
        if ((m + n) & 1)
            return getKthNum(nums1, nums2, (m + n + 1) / 2);
        else
            return (getKthNum(nums1, nums2, (m + n) / 2) +
                    getKthNum(nums1, nums2, (m + n) / 2 + 1)) / 2.0;
    }

    int getKthNum(vector<int>& nums1, vector<int>& nums2, int k) {
        int m1 = 0, m2 = nums1.size(), n1 = 0, n2 = nums2.size();
        while(true) {
            if (m1 == m2)
                return nums2[n1 + k - 1];
            if (n1 == n2)
                return nums1[m1 + k - 1];
            if (k == 1)
                return min(nums1[m1], nums2[n1]);

            int mNextIndex = min(m1 + k / 2 - 1, m2 - 1);
            int nNextIndex = min(n1 + k / 2 - 1, n2 - 1);
            if (nums1[mNextIndex] <= nums2[nNextIndex]) {
                k -= mNextIndex - m1 + 1;
                m1 = mNextIndex + 1;
            } else {
                k -= nNextIndex - n1 + 1;
                n1 = nNextIndex + 1;
            }
        }
    }
};
