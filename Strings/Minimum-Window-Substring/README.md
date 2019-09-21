<p align="center">
<img src="../../Images/Minimum-Window-Substring.png" width="600">
</p>

---
### Solution 1: Sliding Window Approach

#### Motivation

The question asks us to return minimum window from `S` which has all the characters of `T`. Lets call a window `desirable` if it has all the characters from t. 

We can use a simple sliding window approach to solve this problem. In any sliding window based problem we have two pointers. One `right` pointer whose job is to expand the current window and then we have the `left` pointer whose job is to contract a given window. At any point in time only one of these pointers move and the other one remains fixed. e.g.

```
|
left, right

|------------------------------------>|
left                                right (some condition met)

                |---------------------|
                left                right (minimum valid window)
```                

#### Algorithm

* The solution is pretty intuitive. We keep updating the window by moving the right pointer. When the window has all the desired characters, we save the smallest window till now.

* The answer is the smallest desirable window.

  For eg. ` S = "ABAACBAB" T = "ABC" Then our answer window is "ACB" but shown below is one of the possible desirable windows.`
  <p align="center">
  <img src="../../Images/Minimum-Window-Substring-1.png" width="500">
  </p>
  
* Once we have a window with all the characters, we can move the left pointer ahead one by one. If the window is still a desirable one we keep saving it if its the minimum till now.

* If the window is not desirable any more. We try to make it desirable again by moving the right pointer this time.
  
  <p align="center">
  <img src="../../Images/Minimum-Window-Substring-2.png" width="500">
  </p>

* The above steps are repeated until we have looked into all the windows. The smallest window is returned.

  <p align="center">
  <img src="../../Images/Minimum-Window-Substring-3.png" width="500">
  </p>

#### Complexity Analysis

* Time Complexity: `O(|S| + |T|)`
In the worst case we might end up visiting every element of string `S` twice, once by left pointer and once by right pointer. |T| represents the length of string `T`.

* Space Complexity: `O(|S| + |T|)`
|S| when the window size is equal to the entire string `S`. |T| when `T` has all unique characters.


---
### Solution 2: Sliding Window With Optimization

#### Motivation

* A small improvement to the above approach can reduce the time complexity of the algorithm to `O(2*|filtered_S| + |S| + |T|)`, where `filtered_S` is the string formed from S by removing all the elements not present in `T`.

* This complexity reduction is evident when |filtered_S| <<< |S|.
This kind of scenario might happen when length of string `T` is way to small than length of string `S` and string `S` consists of numerous characters which are not present in `T`.

#### Algorithm

* Hence we create a list called `filtered_s` which has all the characters from string 'S' along with their indices in `S`, but these characters should be present in `T`.

  `S = "ABCDDDDDDEEAFFBC" T = "ABC"
  filtered_S = [(0, 'A'), (1, 'B'), (2, 'C'), (11, 'A'), (14, 'B'), (15, 'C')]
  Here (0, 'A') means in string S character A is at index 0.`


* We can now follow our sliding window approach on the reduced `filtered_S`.


#### Complexity Analysis

* Time Complexity: `O(|S| + |T|)`, where |S| and |T| represent the lengths of strings S and T. In certain cases where ∣filtered_S∣ <<< ∣S∣, the complexity would reduce. 

* Space Complexity: `O(|S| + |T|)`


#### Link to OJ

https://leetcode.com/problems/minimum-window-substring/

---
Article contributed by [Sachin](https://github.com/edorado93) and [Divya](https://github.com/DivyaGodayal)
