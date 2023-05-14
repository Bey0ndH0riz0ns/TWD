# The Winds of Daemons


Welcome to the companion repository for the interactive visualization project called 'The Winds of Daemons,' whose Tableau online visualization is found here. This visualization aims to enable computer scientists, software developers, and data scientists to analyze for decision-making purposes the global common category, historical trends, category correlations, and category popularity using the annual Stack Overflow surveys from 2011 to 2022. To make this visualization trustworthy and enable other interested people to embark on similar visualization challenges, we will go through the faced challenges, compromise solutions, and related material of this project.


## How to use the workbook


Assuming you have Tableau installed, open the workbook and unhide all charts by right-clicking the dashboards (the colored tabs) and left-clicking the 'Unhide all sheets' option. This allows you to see how these charts were made and what calculations they used.


## Problems


The integration of 11 online survey datasets with different amounts of rows and questions creates the following problems:


- Questionable explanatory power of self-identified answers
- Identification of relevant questions from many questions
- The changing format between datasets
- The large size of the dataset
- Different labels for the same data
- Multi-choice questions
- The potential effects of missing answers


Here is an example of the 'Questionable explanatory power of self-identified answers':


![image 1](https://github.com/Bey0ndH0riz0ns/TWD/blob/main/Images/Example_Problem_1.PNG)


As we can see, the compTotal variable has joke answers alongside serious compensation ranges, making processing this variable difficult.


Here is an example of the 'Identification of relevant questions from many questions':


![image 2](https://github.com/Bey0ndH0riz0ns/TWD/blob/main/Images/Example_Problem_2.PNG)


As we can see in this 2017 dataset, there are many interesting variables, but there is no reason to assume all of them are useful, so only the most relevant questions should be selected.


Here is an example of the 'The changing format between datasets' with 2011 dataset shown in the first picture and 2022 dataset shown in the second picture:


![image 3](https://github.com/Bey0ndH0riz0ns/TWD/blob/main/Images/Example_Problem_3_1.PNG)


![image 4](https://github.com/Bey0ndH0riz0ns/TWD/blob/main/Images/Example_Problem_3_2.PNG)


As we can see, there are some common things like country, but how they are named and how many more questions 2022 has makes integrating these datasets non-trivial.


Here is an example of 'The large size of the dataset':


![image 5](https://github.com/Bey0ndH0riz0ns/TWD/blob/main/Images/Example_Problem_4.PNG)


As we can see, the integrated dataset is quite huge, which makes it harder to handle with limited computational resources and different software limitations.


Here is an example of 'Different labels for the same data':


![image 6](https://github.com/Bey0ndH0riz0ns/TWD/blob/main/Images/Example_Problem_5.PNG)


As we can see with the marked categories, there are multiple labels for similar data, which makes the distributions distorted.


Here is an example of 'Multi-choice questions':


![image 7](https://github.com/Bey0ndH0riz0ns/TWD/blob/main/Images/Example_Problem_6.PNG)


As we can see, a single value has multiple answers delimited with ';', which makes it much more difficult to get the correct distributions.


Here is an example of 'The potential effects of missing answers':


![image 8](https://github.com/Bey0ndH0riz0ns/TWD/blob/main/Images/Example_Problem_7.PNG)


As we can see, there are a lot of empty answers due to this question not being in all of the surveys, which results in a distorted data distribution.


## Solutions


In order to solve these challenges, the following five compromises were made: 


- Central limit theorem is assumed
- Newer questions are prioritized
- Choice selection is enabled for multi-choice questions
- Regex matching is used to unify relevant lables
- The focus on drill down frequency calculations


The problem of the 'Questionable explanatory power of self-identified answers' is solved by assuming the central limit theorem, which means that all the variables approximate some kind of global normal distribution. This was done because we only have methodology material for the 2017-2022 datasets, and the integrated dataset has 560 000 responses, which means that there should be enough honest people to give good global approximations for the visualization.   


The problems of 'Identification of relevant questions from many questions'. 'The changing format between datasets' and 'The large size of the dataset' were solved with a suitable ![preprocess](https://github.com/Bey0ndH0riz0ns/TWD/blob/main/SO_survey_unified_preprocess_2011_2022.ipynb) with Numpy and Pandas prioritizing newer information over older information, forming variables that represent meta, demographic, education, employment, and technology information. The dataset formed by these variables was then stored as a .csv, which could be put into either a PostgreSQL table or a .hyper to enable Tableu to use it.


The problems of 'Different labels for the same data', 'Multi-choice questions', and 'The potential effects of missing answers' were solved in Tableau by separating multi-choice values into separate columns, using Regex matching to unify similar labels into relevant labels to calculate their frequencies and giving the visualization charts simple drill down filters to focus on different sides of the data. 

![image 9](https://github.com/Bey0ndH0riz0ns/TWD/blob/main/Images/Solution_5.PNG)

![image 10](https://github.com/Bey0ndH0riz0ns/TWD/blob/main/Images/Solution_6.PNG)

![image 11](https://github.com/Bey0ndH0riz0ns/TWD/blob/main/Images/Solution_7.PNG)


## Material

---



---
