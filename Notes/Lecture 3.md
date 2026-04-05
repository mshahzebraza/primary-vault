---
categories:
- '[[TechLearning]]'
tags:
- ossu
---
## Topics

- Iterations
- 

## Tasks

```python
# ###################################
# Task 1: While Loop
# Repeatedly keep the user stuck unless he goes right
# ###################################

  
direction = 'right'

while direction!='left':

    direction = input("Enter the direction (left | right): ").lower()

    if direction=='right':
        print("🔴 You're still stuck")

    elif direction=='left':
        print("🟢 You have exited")

    else:
        print('⚠️ Invalid direction')
```

```python
# ###################################
# Task 2: While Loop
# Keep printing x'es unless the number reduces to zero
# ###################################

n = int(input("Enter the required X'es: "))

while n>0:
    print('X-'+str(n))
    n=n-1
```


```python
# ###################################
# Task 3: While Loop
# Factorial (n!)
# ###################################

  

n = int(input("What number do you want to find factorial for: "))
i = n

factorialsum=1

while i>0:
    print(i,factorialsum)
    factorialsum=factorialsum*i
    i=i-1

print(f"Factorial of {n} is: {factorialsum}")
```

```python
# ###################################
# Task 4: For Loop
# Running Sum (add 0 to n)
# ###################################
  
start_at=1
end_at=int(input("Sum until: "))
step=1

sum = 0
for i in range (start_at, end_at+1, step):
    sum+=i
  

print("Your sum: ",sum)
```