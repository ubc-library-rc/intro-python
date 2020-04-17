---
layout: default
title: Data Structures
parent: Outline
nav_order: 2
---

## Data Structures


Please make sure you have downloaded the workshop data. See [Setup](../index.md) for instructions.
{: .prereq}


For a more detailed tutorial, please refer to the [Python documentation](https://docs.python.org/3/tutorial/index.html)


### Numbers

Additional information available [here](https://docs.python.org/3/tutorial/introduction.html#numbers)

Input
{: .label .label-green }
```python
x = 2.
y = 4.
```

Input
{: .label .label-green }
```python
x + y # sum
```

Input
{: .label .label-green }
```python
y**x # power
```

Input
{: .label .label-green }
```python
y / x # division
```

Be careful

Input
{: .label .label-green }
```python
y / 0 # division by 0
```

Output
{: .label .label-yellow }
```python
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: integer division or modulo by zero
```

### Strings

Additional information available [here](https://docs.python.org/3/tutorial/introduction.html#strings)



<img src="{{site.baseurl}}/content/figures/hello.png">

You can declare a variable to hold text (a.k.a String)

Input
{: .label .label-green }
```python
greetings = "Hello"
print(greetings)
```

***

You can combine or concatenate text

Input
{: .label .label-green }
```python
tutorial = "Python "
offered_by = "Research Commons"

print(tutorial + offered_by)
```

***

In a string, each character is stored at an index. You can obtain a substring by indicating which indexes you want `[start index:end index]`

A blank before the colon, e.g. `[:8]` means from the beginning up until index 8. 

A blank after the colon, e.g. `[5:]` means fro index 5 up until the end.

Input
{: .label .label-green }
```python
offered_by[:8] # check substring
```

***

We don't need to count each character. `index(some character)` will programmatically return an index for us

Input
{: .label .label-green }
```python
offered_by[:offered_by.index(" ")]  # we can get indexes programatically
```

Input
{: .label .label-green }
```python
idx = offered_by.index(" ")
offered_by[:idx]  # we can get indexes programatically
```

***

Strings are case sensitive

Input
{: .label .label-green }
```python
"Research" in offered_by # check if some string contains another
```


Input
{: .label .label-green }
```python
"RESEARCH" in offered_by
```


Input
{: .label .label-green }
```python
"Research".upper() # convert to upper
```

Input
{: .label .label-green }
```python
"Research".lower() # convert to  lowercase
```


***

### Why do I need to know about Strings? Introducing our practical problem


<img src="{{site.baseurl}}/content/figures/global_warming.jpeg">

Suppose we want to find all the sentences of a text file that explicitly mention `global` and `warming`


### First we need to open a file



Input
{: .label .label-green }
```python
with open('G20-2019.txt', 'r') as f:
    data = f.read()
    print(data)
```

### Then we need to split lines in the file. 

Python has a special character `\n` that represents a new line. Many programming languages have these escaped characters



Input
{: .label .label-green }
```python
with open('G20-2019.txt', 'r') as f:
    data = f.read().split('\n')
    print(data)
```

Output
{: .label .label-yellow }
```python
[
    'Good morning, this G20 meeting takes place in a moment of high tension, high political tension.', 
    'We have global warming, but we have also global political warming, and this can be seen in relation to trade and technology conflicts, it can be seen in relation to situations in several parts of the world, namely the Gulf.'
    ... 
]
```   


`data` is no longer a string. It is a **list**! We will get to arrays very soon.