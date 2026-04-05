---
categories:
- '[[TechLearning]]'
tags:
- ossu
---
## Topics

- Strings (Type Conversions, Concatenation, Indexing, Slicing, FStrings)
- Inputs & Outputs
- Comparison & Logical operators (==, !=,)
- Branching; Conditionals

## Tasks

- Task 1: Taking input and printing the result after transforming the input

```python
# Asing the user input to a variable

youtinput = input('enter verb: ')

  

# Print the result: "I can <verb> <verb> <verb> <verb> <verb> beter than you"

# Use of slicing to remove the last space

print("I can "+ ((youtinput+' ')*5)[:-1]+" beter than you")
```

- Task 2: Find cube root using Newton Raphson Method

```python

# Find the cube root of a number using newton raphsons method
# Formula: next_guess = guess - f(guess) / f'(guess)
# Note: f'(guess) means the derivative of f(guess) w.r.t. guess

  

# Example:
# find g such that f(g,x) = g^3 - x = 0
# f'(g) = 3g^2

  

# Implement formula for next guess
# next_g = g - f(g) / f'(g)
# next_g = g - (g^3 - x) / 3g^2

 

# Writing the code

x = float(input('Value of x (To find cube root): '))
g = float(input('Enter first guess: '))
next_g = g - (g**3 - x) / (3*g**2)

  
print("Next guess: ", next_g)
```

- Task 3: Use **FStrings** for Taking input and printing the result after transforming the input

```python
yourinput = input('Enter a string: ')
  

print(f"I can {((yourinput+' ')*5)[:-1]} better than you")
```

- Task 4: Using Branching; Adding decision points in the program (Conditional Statements)

```python
# Write a program to guess the secret number

inputnum=int(input('guess the number: '))

secret = 41

  

if inputnum > secret:
    print("Your number is greater than actual")

elif inputnum < secret:
    print("Your number is less than actual")

else:
    print("You are right")
```
