```python
# recursion
def recursion(level, param1, param2,...):
  # recursion terminator
  if level > MAX_LEVEL:
    print_result
    return
  
  # process logic in current level
  process_data(level, data,...)
  
  # drill down
  self.recursion(level + 1, p1, ...)
  
  # reverse the current level status if needed
  reverse_state(level)
```

```python
# divide and conquer

def divide_conquer(problem, param1, param2, ...):
  # recursion terminatior
  if problem is None:
    print_result
    return
  
  # prepare data
  data = prepare_data(problem)
  subProblems = split_problem(problem, data)
  
  # conquer subProblems
  subResult1 = self.divide_conquer(subProblems[0], p1, ...)
  subResult2 = self.divide_conquer(subProblems[1], p1, ...)
  subResult3 = self.divide_conquer(subProblems[2], p1, ...)
  ...
  
  # process and generate the final result
  result = process_result(subResult1, subResult2, subResult3, ...)
```
