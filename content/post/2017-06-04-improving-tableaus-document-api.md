---
title: "Improving Tableau's Document API"
date: 2017-06-04
draft: false
categories : [
    "Tinkerer",
]
tags: ["Tableau",
       "Python", ]
highlight : true
---

# 1) What is Tableau's Document API?

With the release of Tableau 10, Tableau released a [python utility](https://github.com/tableau/document-api-python) called the Tableau Document API (or TDA for short). TDA allows users to easily programmatically modify tableau workbooks. Modifying tableau workbooks without using Tableau Desktop was possible before as tableau files `.twb` are actually just xml files. However manually editing the xml of `.twb` files could easily result in an unusable corrupted workbook. Fortunately with the release of this tool it is now much simpler to modify workbooks without using Tableau Desktop.

# 2) Using Tableau's Document API

TDA is written in Python so using it is as simple as `pip install TableauDocumentApi` and `import TableauDocumentApi`. For example if you needed to update the connection strings in a dozen local tableau files you could use the following script to update them all.

```python
from TableauDocumentApi import Workbook
import glob, os

os.chdir("my_folder")
for file in glob.glob("*.twb"):
  tableau_workbook = tda.Workbook(file)
  for datasource in tableau_workbook.datasources:
    for connection in datasource.connections:
      connection.server = 'my-new-host'
tableau_workbook.save()
```

# 3) Tableau's Query Bands & Initial SQL

Taking a step away from TDA for a moment Tableau has two less visible but still immensely useful features: [Initial SQL](http://onlinehelp.tableau.com/current/pro/desktop/en-us/examples_teradata.html#initial_sql) & [querybands](http://onlinehelp.tableau.com/current/pro/desktop/en-us/examples_teradata.html#query_band). I've personally used these features to stage temporary tables & tag each query(There are so many...) that tableau runs.

# 4) How does this relate to the TableauDocumentAPI

The [first version I used of Tableau's Document API](https://github.com/t8y8/document-api-python/blob/3a38058f168e29874dc95af4f697888bba71a4fe/tableaudocumentapi/connection.py) did not support modifying initial sql & query bands. After being faced with modifying 1,000+ workbooks to use query bands I decided to review the library and see if support could be easily added. Glancing at the source code I could see that each of the properties of a connection was cleanly defined. Using Port as an example I was able to submit a [pull request](https://github.com/tableau/document-api-python/pull/123) implementing the functionality. Fortunately, the Tableau team was very responsive and quickly merged the pull request.

# 5) Tying it all together

So now if you find yourself in a situation where you need to modify the query bands or the initial sql in your workbooks you can use the TDA to save yourself some time.

Cheers!
