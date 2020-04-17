---
layout: default
title: Practical Problem
parent: Outline
nav_order: 6
---

## A Sample Python Program

We might skip this program depending on group needs
{: .warn}

### Fetching data from the UN and assessing the most discussed topics 

Assume you have a function that is a black-box. You don't need to understand it, just use it to get data from a web page.
The function `get_text_from` takes a resource `r` and return the text from that resource as a `list`.

Input
{: .label .label-green }
```python

import requests
from bs4 import BeautifulSoup
# https://stackoverflow.com/questions/328356/extracting-text-from-html-file-using-python
def get_text_from(r):
    page = requests.get(r)
    soup = BeautifulSoup(page.text)    
    for script in soup(["script", "style", "pre"]):
        script.extract()
    text = soup.get_text()

    lines = (line.strip() for line in text.splitlines())
    chunks = (phrase.strip() for line in lines for phrase in line.split("  "))
    txt = '\n'.join(chunk for chunk in chunks if chunk)

    return txt.split('\n')
```


- For more details, we encourage you to register into the [Introduction to Web Scraping Workshop](https://ubc-library-rc.github.io/intro-web-scraping/)
{: .note}

Input
{: .label .label-green }
```python
def discusses_topic(speech, topic):
    cnt = 0
    for line in speech:
        words_in_sentence = line.split(' ')
        if any(word in topic for word in words_in_sentence):
            cnt += 1
    return cnt
```



We want to define some topics, e.g., climate change, economy, peace, etc. We will use the `discusses_topic` to create a dictionary with the topic and how often it appears in UN discussions. 


As for UN statements, consider:

- [Opening remarks at press conference on WMO State of the Climate 2019 Report](https://www.un.org/sg/en/content/sg/speeches/2020-03-10/wmo-state-of-the-climate-2019-report-remarks)
- [Remarks at the Organizational Meeting of the 2020 Session of the Special Committee on Decolonization](https://www.un.org/sg/en/content/sg/speeches/2020-02-21/2020-session-of-special-committee-decolonization-remarks)
- [Remarks on Sustainable Development and Climate Change](https://www.un.org/sg/en/content/sg/speeches/2020-02-16/remarks-sustainable-development-and-climate-change)
- [Remarks at the "Blue Economy" event](https://www.un.org/sg/en/content/sg/speeches/2020-02-08/remarks-the-blue-economy-event)
- [Opening remarks at virtual press encounter to launch the Report on the Socio-Economic Impacts of COVID-19](https://www.un.org/sg/en/content/sg/speeches/2020-03-31/remarks-launch-of-report-the-socio-economic-impacts-of-covid-19)
- [Remarks at G-20 Virtual Summit on the COVID-19 Pandemic](https://www.un.org/sg/en/content/sg/speeches/2020-03-26/remarks-g-20-virtual-summit-covid-19-pandemic)
- [Opening remarks at press encounter with Prime Minister Erna Solberg of Norway](https://www.un.org/sg/en/content/sg/speeches/2018-06-19/remarks-press-encounter-pm-solberg-norway)
- [Comments of the UN Secretary-General to the 44th G7 Summit](https://www.un.org/sg/en/content/sg/speeches/2018-06-09/secretary-general-comments-44th-g7-summit)
- [Opening remarks to journalists on priorities for 2020 and the work of the organization](https://www.un.org/sg/en/content/sg/speeches/2020-02-04/remarks-journalists-priorities-for-2020-and-work-of-organization)
- [Remarks at the Paris Peace Forum](https://www.un.org/sg/en/content/sg/speeches/2019-11-11/remarks-the-paris-peace-forum)


Input
{: .label .label-green }
```python
un_statements = [
  "https://www.un.org/sg/en/content/sg/speeches/2020-03-10/wmo-state-of-the-climate-2019-report-remarks",
  "https://www.un.org/sg/en/content/sg/speeches/2020-02-21/2020-session-of-special-committee-decolonization-remarks",
  "https://www.un.org/sg/en/content/sg/speeches/2020-02-16/remarks-sustainable-development-and-climate-change",
  "https://www.un.org/sg/en/content/sg/speeches/2020-02-08/remarks-the-blue-economy-event",
  "https://www.un.org/sg/en/content/sg/speeches/2020-03-31/remarks-launch-of-report-the-socio-economic-impacts-of-covid-19",
  "https://www.un.org/sg/en/content/sg/speeches/2020-03-26/remarks-g-20-virtual-summit-covid-19-pandemic",
  "https://www.un.org/sg/en/content/sg/speeches/2018-06-19/remarks-press-encounter-pm-solberg-norway",
  "https://www.un.org/sg/en/content/sg/speeches/2018-06-09/secretary-general-comments-44th-g7-summit",
  "https://www.un.org/sg/en/content/sg/speeches/2020-02-04/remarks-journalists-priorities-for-2020-and-work-of-organization",
  "https://www.un.org/sg/en/content/sg/speeches/2019-11-11/remarks-the-paris-peace-forum"
]

peace = ["peace", "war", "cease", "together", "heal", "truce", "reconciliation", "union", "treaty"]
environment = ["global", "environment", "climate", "change", "natural", "warming", "temperature", "resources"]
economy = ["economy", "business", "development", "employment", "progress", "job", "capital", "dollars"]
```


Input
{: .label .label-green }
```python
cnt_peace = 0
cnt_environment = 0
cnt_economy = 0

for resource in un_statements:
  txt = get_text_from(resource)
  cnt_peace += discusses_topic(txt, peace)
  cnt_environment += discusses_topic(txt, environment)
  cnt_economy += discusses_topic(txt, economy)

data = dict(
  topic=["peace", "environment", "economy"],
  count=[cnt_peace, cnt_environment, cnt_economy]
)
```


Input
{: .label .label-green }
```python
sns.barplot(x='topic', y='count', data=data)
```

Output will be similar to:
{: .label .label-yellow }
<img src="{{site.baseurl}}/content/figures/bar_plot.png">