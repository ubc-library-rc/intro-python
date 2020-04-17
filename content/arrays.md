---
layout: default
title: Arrays
parent: Outline
nav_order: 3
---

## Data Structures (cont.)


### Lists or Arrays


Additional information available [here](https://docs.python.org/3/tutorial/introduction.html#lists) and also [here](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists)


Lists are a "little" similar to Strings in the sense that there is some information stored at some index

Input
{: .label .label-green }
```python
brics = ["Brazil", "Russia", "India", "China", "South Africa"]
```

| index | content 
| --- | --- 
| 0 | `"Brazil"`
| 1 | `"Russia"`
| 2 | `"India"`
| 3 | `"China"`
| 4 | `"South Africa"`

***

Input
{: .label .label-green }
```python
brics[0] # get the 1st element of the list
```

Input
{: .label .label-green }
```python
brics[4] # get last element
```

Input
{: .label .label-green }
```python
brics[-1] # also get last element
```

***

Input
{: .label .label-green }
```python
brics[5]
```


Output
{: .label .label-yellow }
```python
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
```

***

Input
{: .label .label-green }
```python
# append adds an element to the list
brics.append('Philippines')
```

***

Input
{: .label .label-green }
```python
# finds the position of an element in the list
brics.index('Philippines')
```

***

Input
{: .label .label-green }
```python
# deletes an element from the list
# bye Brazil
del brics[0]
```

### Loops



Input
{: .label .label-green }
```python
for country in brics:
    print("This is a loop. I am iterating over the list. variable country = ", country)
```

- After the `for` statement, read from **right** to **left** as in:
    - for the elements in list `brics` we have a variable `country`  that will store one of the values in the list (starting with `Brazil`)
    - For that value, we execute everything in the indentation block
    - After we are done. We repeat and country is `Russia` then `India` and so forth
{: .note}



Output
{: .label .label-yellow }
```python
('This is a loop. I am iterating over the list. variable country = ', 'Brazil')
('This is a loop. I am iterating over the list. variable country = ', 'Russia')
('This is a loop. I am iterating over the list. variable country = ', 'India')
('This is a loop. I am iterating over the list. variable country = ', 'China')
('This is a loop. I am iterating over the list. variable country = ', 'South Africa')
```    



### Back to our practical problem

Suppose we want to find all the sentences of a text file that explicitly mention `global` and `warming`

Input
{: .label .label-green }
```python
with open('G20-2019.txt', 'r') as f:
    data = f.read().split('\n')
    print(data)
```

We need to add a loop iterating over the data. We also need a **condition** to identify a sentence that explicitly mentions `global` and `warming`. 


### Conditionals

Let's start small. We wan sentences that just mention `global`


Input
{: .label .label-green }
```python
with open('G20-2019.txt', 'r') as f:
    data = f.read().split('\n')
    for line in data:
        if 'global' in line:
            print(line)
            print()
```



Output
{: .label .label-yellow }
```python
We have global warming, but we have also global political warming, and this ....

And it is also a moment in which there are uncertainties about the global economy ...

... we need to make sure that we do not reach more than 1.5 degrees Celsius of global warming at the end of the century.
``` 


### More than one conditional


Input
{: .label .label-green }
```python
with open('G20-2019.txt', 'r') as f:
    data = f.read().split('\n')
    for line in data:
        if 'global' in line and 'warming' in line:
            print(line)
            print()
```


Input
{: .label .label-green }
```python
with open('G20-2019.txt', 'r') as f:
    data = f.read().split('\n')
    for line in data:
        if 'global' in line or 'warming' in line:
            print(line)
            print()
```



If we are on track, try to:
{: .warn}

### 1. create two numeric variables `cnt_2016` and `cnt_2019`

### 2. Open G20-2019.txt

### 3. Iterate the lines in the file `counting` every line that mentions global warming 

increment `cnt_2019` for every line that  mentions global warming 

### 4. Open G20-2016.txt

### 5. Iterate the lines in the file `counting` every line that mentions global warming 

increment `cnt_2016` for every line that  mentions global warming 

### 6. print the two numeric variables

<br>

Don't spoil the fun. The stick figure is watching you




<img src="{{site.baseurl}}/content/figures/watch.png" width="30%">

