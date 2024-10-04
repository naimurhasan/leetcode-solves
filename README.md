# Coding Solutions

This repository contains solutions to various coding problems I have solved. Each problem is written in Kotlin, and I'll continue to update the list as I solve more.

## Problem List

* [Two Sum](#1-two-sum)
* [Contains Duplicate](#2-contains-duplicate)
* [Best Time to Buy and sell stock](#3-best-time-to-buy-and-sell-stock)
* [Valid Anagram](#4-valid-anagram)
* [Product of Array Except Self](#5-Product-of-Array-Except-Self)

### 1. Two Sum

**Problem**:  
Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to the target.

**Solution**:
```kotlin
class Solution {
    fun twoSum(nums: IntArray, target: Int): IntArray {
        for (i in 0 until nums.size - 1) {
            for (j in i + 1 until nums.size) {
                if (nums[i] + nums[j] == target) {
                    return intArrayOf(i, j)
                }
            }
        }
        return intArrayOf(-1, -1)
    }
}
```

**A little boost with adding hashmap trial before the bruetforce takes place**:

```
/**
 * You can edit, run, and share this code.
 * play.kotlinlang.org
 */

class Solution {
    fun twoSum(nums: IntArray, target: Int): IntArray {
        val m = mutableMapOf<Int, Int>()
        var index = 0

        // search through hashmap
        for(i in nums){
            m[i] = index
            index++
        }
        index = 0
        for(i in nums){
            val diff = target - i
            if(diff!=i && m[diff]!=null){
                return intArrayOf(index, m[diff]!!)
            }
            index++
        }

        // old ususal solution
        for(i in 0 until nums.size-1){
            for(j in i+1 until nums.size){
                if(nums[i]+nums[j]==target){
                    return intArrayOf(i, j)
                }
            }
        }
        
        return intArrayOf(-1, -1)
    }
}

fun main() {
    println(Solution().twoSum(intArrayOf(2,7,11,15), 9).contentToString())
}
```
**further optimization:**
```kt
fun twoSum(nums: IntArray, target: Int): IntArray {
        val m = mutableMapOf<Int, Int>()
        for((i, v) in nums.withIndex()){
            val diff = target - v
            if(m[diff]!=null){
                return intArrayOf(i, m[diff]!!)
            }else{
                m[v] = i
            }
        }        
        return intArrayOf(-1, -1)
    }
```

***without map:**
```
fun twoSum(nums: IntArray, target: Int): IntArray {
        val indexedNums = nums.withIndex().toList()
    
        val sortedNums = indexedNums.sortedBy { it.value }

        var left = 0
        var right = sortedNums.size - 1

        while (left < right) {
            val sum = sortedNums[left].value + sortedNums[right].value

            if (sum == target) {
                return intArrayOf(sortedNums[left].index, sortedNums[right].index)
            } else if (sum < target) {
                left++
            } else {
                right--
            }
        }

        return intArrayOf(-1, -1)
    }
```

**Approach**:  
The solution iterates over all pairs of elements in the array using a nested loop to find the pair that adds up to the target value. If such a pair is found, it returns their indices.

---

### 2. Contains Duplicate
Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

**Problem**:  
Example 1:

Input: nums = [1,2,3,1]

Output: true

Explanation:

The element 1 occurs at the indices 0 and 3.

**Solution**:  
```
class Solution {
    fun containsDuplicate(nums: IntArray): Boolean {
        val m = mutableMapOf<Int, Boolean>()
        for(v in nums){
            if(m[v]==null)
            	m[v]=true
            else
            	return true
        }
        return false
    }
}
```

**Approach**: 

The approach uses a hashmap to track elements while iterating through the array, returning true if a duplicate is found, otherwise adding new elements to the map.

---

Here's how you can write the note in the required format:

---

### 3. Best Time to Buy and Sell Stock
**Problem**:  
You are given an array `prices` where `prices[i]` is the price of a given stock on the ith day. You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock. Return the maximum profit you can achieve from this transaction. If no profit can be achieved, return 0.

**Solution**:
```kotlin
class Solution {
    fun maxProfit(prices: IntArray): Int {
        var leastSoFar = Int.MAX_VALUE
        var maxProfit = 0
        
        for (price in prices) {
            if (price < leastSoFar) {
                leastSoFar = price
            }
            
            val profitIfSoldToday = price - leastSoFar
            
            if (profitIfSoldToday > maxProfit) {
                maxProfit = profitIfSoldToday
            }
        }
        
        return maxProfit
    }
}
```

**Approach**:  
The approach uses a greedy strategy to track the minimum price encountered so far (`leastSoFar`) and calculates the profit if the stock is sold on the current day (`price - leastSoFar`). It then keeps updating the maximum profit found during the iteration. This ensures we find the best day to sell after buying on the cheapest day.

--- 

### 4. Valid Anagram

**Problem**:  
Given two strings s and t, return true if t is an 
anagram
 of s, and false otherwise.

**Solution**:  
```
class Solution {
    fun isAnagram(s: String, t: String): Boolean {
        if(s.length != t.length)
            return false
        
        val sM = mutableMapOf<Char, Int>()

        for(c in s){
            if(sM[c] != null){
                sM[c] = sM[c]!!+1
            }else{
                sM[c] = 1
            }
        }
        
        for((k, v) in sM){
            var count = 0;
            for(c in t){
                if(c==k){
                    count++
                }
            }
            if(count!=v){
                return false
            }
        }
        
        return true
    }
}
```

**Optimize from n^2 to n:**
```kt
fun isAnagram(s: String, t: String): Boolean {
        if(s.length != t.length)
            return false
        
        val sM = mutableMapOf<Char, Int>() // s Map

        for(c in s){
            if(sM[c] != null){
                sM[c] = sM[c]!!+1
            }else{
                sM[c] = 1
            }
        }
        
        for(c in t){
            if(sM[c] == null)
            	return false
            else if(sM[c]==0)
            	return false
           	else
            	sM[c] = sM[c]!!-1
        }
        
        return true
    }
```

**Approach**:  

The approach counts the frequency of characters in string s using a map, then compares these counts with the characters in string t to check if they match.

--- 

### 5. Product of Array Except Self

**Problem**:  
Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.
```
Example 1:

Input: nums = [1,2,3,4]
Output: [24,12,8,6]
Example 2:

Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

**Solution**:  

#### works but gets TLE
```
Example 1:

Input: nums = [1,2,3,4]
Output: [24,12,8,6]
Example 2:

Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

**accepted:**
```
class Solution {
    fun maxSubArray(nums: IntArray): Int {
        var maxSum = Int.MIN_VALUE
        var sum = 0
        for(v in nums){
        	sum += v
            
            if(sum>maxSum){
                maxSum = sum
            }
            
            if(sum<0){
                sum = 0
            }
            
        }        
        return maxSum
    }
}
```

**Approach**:  

Loop through array but skip index.

--- 

This format will help in organizing and documenting your solution for future reference!

### 0. [Problem Title]  
(Add future problems as you solve them here)

**Problem**:  


**Solution**:  


**Approach**:  

(Describe the problem here)

---

## How to Run

To run the solutions, you can copy the code into your preferred Kotlin environment or set up a Kotlin project.

1. Install Kotlin if you don't have it:
    ```bash
    brew install kotlin
    ```

2. Run the code using the following command:
    ```bash
    kotlinc <file_name>.kt -include-runtime -d <output_jar>.jar
    java -jar <output_jar>.jar
    ```

---

Feel free to clone this repository and try out the solutions for yourself. More problems and solutions will be added regularly.

---

This README will serve as a growing collection of all your solved coding problems. Let me know if you need further adjustments!
