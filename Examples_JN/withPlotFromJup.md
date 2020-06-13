
```{code-cell} ipython3
:echo: false
:message: false
:tags: [remove_output]
:warning: false

library(reticulate)
library(exams)
```

```{code-cell} ipython3
:echo: false
:name: data generation
:tags: [remove_output]

%%python
import random
import numpy as np
import array
r = random.sample([-.97, 0, .5, .97], 1)[0]
if np.random.uniform(size=1) < 1/3:
  mx=0
  my=0
  sx=1
  sy=1
else:
  mx= random.sample(list(10*np.arange(-5,5)),1)[0]
  my= random.sample(list(10*np.arange(0,5)),1)[0]
  sx= random.sample([1, 10, 20],1)[0]
  sy= random.sample([1,10,20],1)[0]

b= r* (sy/sx)
a= my - b*mx
x= np.random.normal(mx,sx,size=200)
y= b*x + np.random.normal(a,sy*np.sqrt(1-r**2),200)
questions = ['','','','']
explanations= ['','','','']
solutions= [True,True,True,True]

if (np.random.uniform(size=1)[0] < .5):
  questions[0] = 'The scatterplot is standardized.'
  solutions[0] = mx==0 and my==0 and sx==1 and sy==1
else:
  questions[0]= "The slope of the regression line is about 1."
  solutions[0]= abs(b-1) < .1
  explanations[0]= "The slope of the regression line is" + str(b)
  
if (solutions[0]): 
  explanations[0]= "X and Y have both mean 0 and variance 1." 
else: 
  explanations[0]="The scatterplot is not standardized, because X and Y do not both have mean 0 and variance 1."
   
   
if(np.random.uniform(size=1)[0] < .5):
  questions[1] = "The absolute value of the correlation coeffiient is at least .8"
  solutions[1] = abs(r) >= .8
else:
  questions[1]="The absolute value of the correlation coefficient is at most .8."
  solutions[1]= abs(r) <= .8
   
if(abs(r) >= .9):
  explanations[1]="A strong association between the variables is given in the scatterplot, so the absolute correlation coefficient is larger than .8."
elif(abs(r)==0):
  explanations[1]="No association between the variables is observed in the scatterplot. This implies a correlation coefficient close to 0."
else:
  explanations[1]="Only a slightly positive association between the variables is observable in the scatterplot"
 
if(np.random.uniform(size=1) <.5):
  questions[2] = "The standard deviation of X is at least 6"
  solutions[2] = sy >= 6
  explanations[2] = "The standard deviation of X is equal to " + str(sx)
else:
  questions[2]= "The standard deviation of Y is at least 6."
  solutions[2]= sy>=6
  explanations[2]= "The standard deviation of Y is equal to" + str(sy)
 
if(np.random.uniform(size=1) < .5):
  questions[3]= "The mean of X is at most 5."
  solutions[3]= mx<=5
  explanations[3]="The mean of X is about equal to" + str(mx)
else:
  questions[3]="The mean of Y is at least 30"
  solutions[3]= my>= 30
  explanations[3]= "The mean of Y is equal to" + str(my)
  
o= random.sample(list(np.arange(0,4)),4)
questions=[questions[i] for i in o]
solutions=[solutions[i] for i in o]
explanations= [explanations[i] for i in o]


```

Question
========

The following figure shows a scatterplot. Which of the following statements are correct?

```{code-cell} ipython3
:echo: false

plot(py$x,py$y,xlab="x",ylab="y")
```

```{code-cell} ipython3
:name: questionlist
:results: asis
:tags: [remove_input]

answerlist(py$questions, markup = "markdown")
```

Solution
========

```{code-cell} ipython3
:name: solutionlist
:results: asis
:tags: [remove_input]

answerlist(ifelse(py$solutions, "True", "False"), py$explanations, markup = "markdown")
```

Meta-information
================
extype: mchoice
exsolution: `r mchoice2string(py$solutions)`
exname: Scatterplot
