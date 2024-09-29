# Coding Solutions

This repository contains solutions to various coding problems I have solved. Each problem is written in Kotlin, and I'll continue to update the list as I solve more.

## Problem List

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

**Approach**:  
The solution iterates over all pairs of elements in the array using a nested loop to find the pair that adds up to the target value. If such a pair is found, it returns their indices.

---

### 2. [Problem Title]  
(Add future problems as you solve them here)

**Problem**:  
(Describe the problem here)

**Solution**:  
(Add the solution here)

**Approach**:  
(Explain the approach here)

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
