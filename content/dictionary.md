---
layout: default
title: Functions and Dictionaries
parent: Outline
nav_order: 4
---

## Data Structures (cont.)

### Answer to exercise at [arrays](arrays.md):


Input
{: .label .label-green }
```python
cnt_2019 = 0
with open('G20-2019.txt', 'r') as f:
    data = f.read().split('\n')
    for line in data:
        if 'global' in line and 'warming' in line:
            cnt_2019 += 1

cnt_2016 = 0
with open('G20-2016.txt', 'r') as f:
    data = f.read().split('\n')
    for line in data:
        if 'global' in line and 'warming' in line:
            cnt_2016 += 1            

print("Was global warming a concern in 2016? ", cnt_2016)
print("Was global warming a concern in 2019? ", cnt_2019)
```

Do not underestimate this code snippet. Had we have all world leader speeches, and enough computational power, we could check things like who discusses more about the environment, economy, or war. You can apply this idea to your interview data, numerical data, etc.
{: .note}


## Functions


It may be useful to wrap code around functions. You can read more about that [here](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)

Look at the answer for the array exercise. The only thing that changes is the **open file** line.
We can define a function to avoid code repetition.



Input
{: .label .label-green }
```python
def discusses_global_warming(speech):
    cnt = 0
    with open(speech, 'r') as f:
        data = f.read().split('\n')
        for line in data:
            if 'global' in line and 'warming' in line:
                cnt += 1
    return cnt            

cnt_greta = discusses_global_warming('greta.txt')
print(cnt_greta)
```


What if we also want to control the words that we look for?

Similarly to how we can split the file by lines `.split('\n')` we can split a sentence by word using `.split(' ')`

We can then check if any word in our list of words are in the list of words that we look for, a.k.a `topics`


Input
{: .label .label-green }
```python
def discusses_topic(speech, topic):
    cnt = 0
    with open(speech, 'r') as f:
        data = f.read().split('\n')
        for line in data:
            words_in_sentence = line.split(' ')
            if any(word in topic for word in words_in_sentence):
                cnt += 1
    return cnt            

global_warming_topic = ['global', 'warming', 'environment', 'crisis']
cnt_greta = discusses_topic('greta.txt', global_warming_topic)
print(cnt_greta)
```



## Dictionaries or Maps

Additional information available [here](https://docs.python.org/3/tutorial/datastructures.html#dictionaries):

Imagine that you have an excel or csv file, where each column contains some data. Certain columns have more rows than others and you want quick access to the data of a single column. 

This analogy simplifies the meaning of a dictionary:


Input
{: .label .label-green }
```python
data = dict(
    speecher=['Greta Thunberg', 'Barack Obama', 'UN Secretary-General'], 
    transcript=['greta.txt', 'G20-2016.txt', 'G20-2019.txt'], 
    year=[2020, 2016, 2019], 
    updated_on=2020, 
    updated_by="Arthur"
)
```

Input
{: .label .label-green }
```python
data
```


Output
{: .label .label-yellow }
```python
{'speecher': ['Greta Thunberg', 'Barack Obama', 'UN Secretary-General'], 'transcript': ['greta.txt', 'G20-2016.txt', 'G20-2019.txt'], 'year': [2020, 2016, 2019], 'updated_on': 2020, 'updated_by': 'Arthur'}
```

We can also make the output more readable using the `json` library 


Input
{: .label .label-green }
```python
print(json.dumps(data, indent=4, sort_keys=True))
```


Output
{: .label .label-yellow }
```python
{
    "updated_on": 2020,
    "speecher": [
        "Greta Thunberg",
        "Barack Obama",
        "UN Secretary-General"
    ],
    "transcript": [
        "greta.txt",
        "G20-2016.txt",
        "G20-2019.txt"
    ],
    "updated_by": "Arthur",
    "year": [
        2020,
        2016,
        2019
    ]
}
```

### Dictionary operations

Input
{: .label .label-green }
```python
data['transcript']
```

Input
{: .label .label-green }
```python
data['speecher']
```

Input
{: .label .label-green }
```python
data['conference']
```


Input
{: .label .label-green }
```python
data['updated_on'] = 2019 # overrides key with new value
```

Input
{: .label .label-green }
```python
del data['year'] # deletes a key
```

Input
{: .label .label-green }
```python
# creates a new key with a list as its value
data['conference'] = ['Climate Summit', 'G20', 'G20'] 
```

Input
{: .label .label-green }
```python
# Modify existing keys
# We need to know the type of each field. 
# Otherwise, problems might occur
data['conference'].append('UN annual summit')
data["updated_by"] += " Matty"
```

Input
{: .label .label-green }
```python
data['conference'] += 'UN annual summit'
print(data['conference'])
```

Input
{: .label .label-green }
```python
data['updated_by'] += 1
print(data['updated_by'])
```


***

### Why do I need to know about Dictionaries? Back to our practical problem


<img src="{{site.baseurl}}/content/figures/global_warming.jpeg">


Thus far, we used Python mostly for textual data. Let's move to some numerical data.

Suppose we have at our disposal a csv file with three columns, `year`, `average temperature`, and `average carbon dioxide emission`.
We want to extract this data from the file, put it into memory, and check whether there is correlation between carbon dioxide emission earth's average temperature.


1. First create and empty dictionary with 3 keys. All our keys will be lists


Input
{: .label .label-green }
```python

data = dict(
    year=[],
    temperature=[],
    carbon_emission=[]
)
```

2. Then, we will read the file line by line using `readlines()`. Ignore the `if` conditional for now. 


Input
{: .label .label-green }
```python

current_line = 0
with open('year_temperature_carbon_emission.csv', 'r') as f:
    lines = f.readlines() 
    for line in lines:
        print(line)
        current_line += 1
        if current_line > 5:
            break
```

Output
{: .label .label-yellow }
```python
"","year","avg_temp","AverageCarbonEmission"

"1",1958,18.9421732093664,315.33

"2",1959,18.825205922865,315.981666666667

"3",1960,18.8870130853994,316.908333333333

"4",1961,18.9235654269972,317.645

"5",1962,18.6938474517906,318.453333333333
```

3. It seems we have some pre-processing steps ahead:
    - The extra line between each print means that there is a `\n` in the line variable. Remove it with `.replace('\n', '')`
    - We need to split lines by comma `.split(',')` and store the result in a variable `aux`
    - create three variables year, temp, carbon whose value will be equal to `aux[some index]`
    - append the variables to our dictionary keys, e.g., `data['temperature'].append(temp)`
    - how do we skip the first line with the header?


If we are on track, try to do that on your own.
{: .warn}

<br>

Don't spoil the fun. The stick figure is watching you



<img src="{{site.baseurl}}/content/figures/watch.png" width="30%">





