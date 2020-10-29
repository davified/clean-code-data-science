# **Dispensables**

## Avoid comments

Comments can become problematic in a few ways:

- If some code needs comments, it's a smell for deeper issues (e.g. bad variable naming, violation of single responsibility principle, poor abstraction)
- Comments can grow stale and they can lie
- Comments can make code even harder to understand when there's too much of it.

With good variable names, proper abstraction of our code into functions with single responsibility and unit tests, we can understand our code without comments.

**Bad:**

```python
# Check to see if employee is eligible for full benefits
if (employee.flags and HOURLY_FLAG) and (employee.age > 65):
    # do something
```

**Good:**

```python
if employee.is_eligible_for_benefits():
    # do something
```

## Remove dead code

Dead code is code which is executed but whose result is never used in any other computation. Dead code is yet another unrelated thing that developers have to hold in our head when coding. It adds unnecessary cognitive load.

If there's code which does not change the result of the program whether it runs or not, then it's not required for the code to run. We should remove it to keep the codebase clean. When we make small and frequent commits, we need not fear losing code. If we ever need those lines of code again, we can easily recover it from the git history.

One common type of dead code are print statements (even glorified print statements such as `df.head()`, `df.describe()`, `df.plot()`). While these offer useful feedback when we're writing code, too much of it makes code hard to read. The team has to visually parse the notebook and spend mental effort to filter out inconsequential print statements in order to find the code that actually has an effect on the output.

When our codebase has unit tests, the feedback from unit tests replaces the manual/visual feedback we used to use (e.g. df.head()) to check if things are working. This allows us to remove these print statements and make our code more readable.

**Bad:**

```python
df = get_data()
print(df)
# do_other_stuff()
# do_some_more_stuff()
df.head()
print(df.columns)

# do_so_much_stuff()
model = train_model(df)

```

**Good:**

```python
df  = get_data()
model = train_model(df)
```
