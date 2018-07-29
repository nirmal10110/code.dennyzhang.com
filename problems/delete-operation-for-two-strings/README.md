
# Leetcode: Delete Operation for Two Strings     :BLOG:Hard:

---

Delete Operation for Two Strings  

---

Similar Problems:  

-   [Edit Distance](https://code.dennyzhang.com/edit-distance)
-   [Maximum Length of Repeated Subarray](https://code.dennyzhang.com/maximum-length-of-repeated-subarray)
-   [Interleaving String](https://code.dennyzhang.com/interleaving-string)
-   Tag: [#dynamicprogramming](https://code.dennyzhang.com/tag/dynamicprogramming), [#dp2order](https://code.dennyzhang.com/tag/dp2order)

---

Given two words word1 and word2, find the minimum number of steps required to make word1 and word2 the same, where in each step you can delete one character in either string.  

    Example 1:
    Input: "sea", "eat"
    Output: 2
    Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".

Note:  

1.  The length of given words won't exceed 500.
2.  Characters in given words can only be lower-case letters.

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/problems/delete-operation-for-two-strings)  

Credits To: [leetcode.com](https://leetcode.com/problems/delete-operation-for-two-strings/description/)  

Leave me comments, if you have better ways to solve.  

---

    // Blog link: https://code.dennyzhang.com/delete-operation-for-two-strings
    // Basic Ideas: dynamic programming
    //
    // dp(i, j): make word1[0:i] and word2[0:j]
    //
    // Complexity: Time O(n*m), Space O(n)
    func minDistance(word1 string, word2 string) int {
        dp := make([]int, len(word2)+1)
        for i, _ := range dp { dp[i] = i }
        for i:=1; i<=len(word1); i++ {
    	prev := i-1
    	dp[0] = i
    	for j:=1; j<=len(word2); j++ {
    	    cur := -1
    	    if word1[i-1] == word2[j-1] { 
    		cur = prev
    	    } else {
    	       // delete word1[i]
    		v := dp[j]+1
    		// delete word2[j]
    		if v>dp[j-1]+1 { v = dp[j-1]+1 }
    		cur = v
    	    }
    	    prev = dp[j]
    	    dp[j] = cur
    	}
        }
        return dp[len(word2)]
    }
