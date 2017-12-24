# Swap the elements
A nice question from codility lessons [pdf](https://codility.com/media/train/2-CountingElements.pdf).

# Description
You have two arrays A and B of n integers. All elements in A and B is less or equal than m and greater or equal than 1 (1 <= A[i] <= m, 1 <= B[i] <= m).

The goal is to check whether there is a swap operation which can be performed on these arrays in such a way that the sum of elements in array A equals the sum of elements in array B after the swap. By swap operation we mean picking one element from array A and one element from array B and exchanging them.

# Trivial Solution
For each element in A, for each element in B, swap it and caculate the sums of two arrays.

This algorithm take O(n^3) time complexity and O(1) space complexity.

# Better Solution
We can caculate the sums of two array at first. For each pair, we can get the sum of each array by applying an addition and a substraction to the initial sum. 

It take O(n^2) time complexity and O(1) space complexity.

```python
def slow_solution(A, B, m):
  n = len(A)
  sum_A = sum(A)
  sum_B = sum(B)
  for i in xrange(n):
    for j in xrange(n):
      change = B[j] - A[i]
      sum_a += change
      sum_b -= change
      if sum_a == sum_b:
        return True
  return False
```

# Solution with Counting
If we can get the same sums of A and B by swap A[i] and B[j], let d = B[j] - A[i], then
1. A[i] = B[j] - d
2. sum(B) - sum(A) = 2d
3. sum(B) - sum(A) is even

By these properties, we can write our code by only counting array A.

```python
def fast_solution(A, B, m):
  sum_a = sum(A)
  sum_b = sum(B)
  
  # By prop 3
  if (sum_b - sum_a) % 2 == 1:
    return False

  # By prop 2
  d = (sum_b - sum_a) // 2 

  count = counting(A, m)
  for j in xrange(n):
    target_a = B[j] - d
    if 0 <= target_a and target_a <= m and count[target_a] > 0:
      return True
  return False
```

