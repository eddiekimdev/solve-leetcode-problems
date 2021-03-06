# Different Ways to Add Parentheses

Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are `+`, `-` and `*`.

**Example 1**

Input: `"2-1-1"`.
```
((2-1)-1) = 0
(2-(1-1)) = 2
```
Output: `[0, 2]`

**Example 2**

Input: `"2*3-4*5"`
```
(2*(3-(4*5))) = -34
((2*3)-(4*5)) = -14
((2*(3-4))*5) = -10
(2*((3-4)*5)) = -10
(((2*3)-4)*5) = 10
```
Output: `[-34, -14, -10, -10, 10]`

**Solution:**
```java
public class Solution {
  public List<Integer> diffWaysToCompute(String input) {
    List<Integer> res = new ArrayList<Integer>();

    for (int i = 1; i < input.length(); i++) {
      char c = input.charAt(i);

      if (c == '+' || c == '-' || c == '*') {
        String s1 = input.substring(0, i);
        String s2 = input.substring(i + 1);

        List<Integer> l1 = diffWaysToCompute(s1);
        List<Integer> l2 = diffWaysToCompute(s2);

        for (Integer n1 : l1) {
          for (Integer n2 : l2) {
            switch (c) {
              case '+': res.add(n1 + n2); break;
              case '-': res.add(n1 - n2); break;
              case '*': res.add(n1 * n2); break;
            }
          }
        }
      }
    }

    if (res.size() == 0) {
      res.add(Integer.valueOf(input));
    }

    return res;
  }
}
```