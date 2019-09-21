<p align="center">
<img src="../../Images/Cracking-the-Safe.png" width="600">
</p>

The question can seem to be a bit confusing at first. So the first thing we will do is
explain what the question is asking for exactly. 

So, the question says that we can enter a string representing some characters in a range into 
a safe and the safe's algoritm will consider the last `n` digits only as password. If the password is 
correct, the safe would open. We are to provide the smallest string that would 
cover all the possible passwords. 

So, let us explain the example in the question itself. We are given n = 2 and k = 2. This means that the 
password would consist of 2 digits and the digits can range from `[0,1]` since k = 2. Let us look at all possible passwords
of length 2 only composed of 0s and 1s. 

```
00
01
10 and 
01
``` 

We enter one digit at a time into the safe and the last 2 entered digits are matched against the 
password. One possible sequence of digits entered are

```
0 --> 00 --> 001 --> 0010 --> 001011. 
This sequence would cover all the passwords. 
00 --> 00
001 --> 01
0010 --> 10
001011 --> 11 
```

But, the question here is, is this the smallest sequence covering all of the possible passwords ? The answer is NO!
Have a look at the following sequence which is indeed the smallest for this example
 
```
0 --> 00 --> 001 --> 0011 --> 00110
00 --> 00
001 --> 01
0011 --> 11
00110 --> 10
``` 

Hopefully, you have understood the question. Now let us move on to the solution for this problem. 
Let us consider the current sequence that we have already entered into the safe. Say that sequence is represented 
by `S` and is of length `l`. 

---
### Solution 1: Recursive Approach

#### Algorithm

1. The last password that the safe would have considered was `S[l-n:]` i.e. the last `n` characters.
Now, we can enter one more digit from the range of possible digits that we have i.e. `0 .. k`. After entering this 
digit, the new password that would be considered by the safe would be `S[(l+1) - n:]` since the new length of the sequence would be `l+1`. 

2. Now consider the example we discussed above and let us look at the following sequence `001`. 
We can consider a `1` here as the new character and that would give us `0011` with `11` being the new
password that the safe would consider. Or we can try entering a `0` to get `0010` where the 
safe would consider `10` as the new password. At this point, both these options 
seem good enough. 

3. But, we know that choosing a `1` here leads to the optimal solution and not a `0`.
Choosing a `0` leads to the situation `0010` where we should not enter another `0` 
because we have already tried the password `00` in the very beginning. Also, entering a `1` would
give us a redundant password in `01`. So, we have to enter 2 `1`s here to make the safe
try the final remaining password of `11`. 

4. The main approach here is this. We start with an `n` digit password where each of the digits are the same i.e.
either `0000...n` or `kkkk...n`. and we keep on trying out one digit at a time and we recurse. 
The shortest sequence would be the one that makes the safe consider a new, unseen password everytime 
we enter a new digit unlike the first option in the example above where we had to 
enter two digits `11` so that the safe could consider this new password. 

Hopefully, the following sequence of diagrams would make the algorithm clearer. 

 <p align="center">
 <img src="../../Images/cracking-safe-diag-1.png" width="600">
 </p>
 
 This diagram shows the optimal solution for the example that we considered. Look at the next
 diagram to understand the graphical view of the problem. 
 
 <p align="center">
 <img src="../../Images/cracking-safe-diag-2.png" width="600">
 </p>

Hope you understood the problem statement and the approach as well. Look at the code for even better understanding from an implementation perspective.

#### Complexity Analysis

* Time Complexity = `O(K^(K^N))` because the final sequence will have a length of `K^N` and each position has `K` possible digits to choose from. Note that since these are digits, the max value of `K` can be 9. 
* Space Complexity = `O(K^N)` since these are all the possible combinations that should be covered by the resultant string. That's the length of a single recursion and hence the space occupied by the recursion stack.

#### Link to OJ

https://leetcode.com/problems/cracking-the-safe/

---
Article contributed by [Sachin](https://github.com/edorado93) and [Divya](https://github.com/DivyaGodayal)
