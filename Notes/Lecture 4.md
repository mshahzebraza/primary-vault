---
categories:
- '[[TechLearning]]'
tags:
- ossu
---
## Topics

- Loops over Strings
- Algo: Guess-and-Check 
- Binary

## Tasks
#### Task 1: Even numbers in the rage

```python
 
start_at=1
end_at=int(input("Sum until: "))
step=1

sum = 0
for i in range (start_at, end_at+1, step):
    sum+=i
  

print("Your sum: ",sum)
```

#### Task 2: Loops and strings (For Loops can iterate through strings)

```python
 
  

sentence = "This is a big and long sentence to testing you"

# for char in sentence:

#     if char=='i' or char =='u':

#         print('There is an "i" or "u"')

  

# A better way (if str1 in str2)

for char in sentence:

    if char in 'iu':

        print('There is an "i" or "u"')
```

#### Task 3: Robot Cheerleaders

```python
 
an_letters = "aefhilmnorsx"

  

word = input("Word to cheer for: ")

intensity = int(input("Intensity: "))

  

for letter in word:

    if letter.lower() in an_letters:

        print(f"Give me an {letter}: {letter}")

    else:

        print(f"Give me a {letter}: {letter}")

  

print("What does that spell?")

  

for i in range(intensity):

    print(f"{word}!!!")
```

#### Task 4: Print unique letters in a string

```python
 
  

str = "hellowworld"

  

uniqueStr=''

  

for letter in str:

    if letter.lower() not in uniqueStr.lower():

        uniqueStr+=letter

    # else:

    #     pass # * "pass" skips the loop iteration

  

print("Unique String: ", uniqueStr)

print("Unique String Count: ", len(uniqueStr))
```

#### Task 5: Guess and check - Root of a perfect square

```python


checksquare = int(input('Enter number to check if its a valid square: '))
sqrtguess = 0


# Unoptimized solution
# for i in range(checksquare+1):
#     if i**2==checksquare:
#         sqrtguess=i
#         break

# if sqrtguess !=0:
#     print(f"🟢 Sq. Root of {checksquare} is {sqrtguess}")
# else:
#     print(f"🔴 Number {checksquare} is not a perfect square")


# Optimized solution
# Run unless guess exceeds the check-square values
while sqrtguess**2 < checksquare:
    sqrtguess+=1


if sqrtguess**2==checksquare:
    print(f"🟢 Sq. Root of {checksquare} is {sqrtguess}")
else:
    print(f"🔴 Number {checksquare} is not a perfect square")
    # Handle negative numbers by warning user
    if checksquare<0:

        print(f"⚠️ Did you mean to {-checksquare} instead?")
```

#### Task 6: Guess and check - secret value in a give range

```python
 
  

secret = 11

limit = int(input('Enter limit: '))

  

found=False

# Unoptimized solution

for i in range(limit+1):

    if secret==i:

        found=True

        print('Found: ',i)

        break

  

if not found:

    print('Not found')
```

#### Task 7: Guess and check - Word Problems

```python
 
# Alyssa = x
# Ben = x-2
# Cindy = 2*x
# Total = 10

  

# Alyssa + Ben + Cindy = Total

total = 10
found = False
  

for x in range(total+1):
    a = x # Alyssa
    b = x - 2 # Ben
    c = 2 * x # Cindy

    if a+b+c==total:
        found=True
        break

  
if found==True:
    print(f"Alyssa ({a}),Ben ({b}) and Cindy ({c})")
else:
    print("No solution found")
```
