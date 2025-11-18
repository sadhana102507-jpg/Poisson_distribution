# Fitting Poisson  distribution
# Aim : 

To fit poisson distribution for the arrival of objects per minute from the feeder

# Software required :  

Python and Visual component tool

# Theory:

The Poisson distribution is the discrete probability distribution of the number of events occurring in a given time period, given the average number of times the event occurs over that time period.

![image](https://user-images.githubusercontent.com/104613195/166248326-fd042076-8b0b-40c4-8b11-1d8e8fcb74db.png)

 Conditions for Poisson Distribution:

1. An event can occur any number of times during a time period.
2. Events occur independently. I
3. The rate of occurrence is constant.
4. The probability of an event occurring is proportional to the length of the time period. 
 
# Procedure :

![image](https://user-images.githubusercontent.com/104613195/166251988-d0c53205-6080-4f7b-ae4c-398178586637.png)

# Experiment :

![image](https://user-images.githubusercontent.com/103921593/230282876-f4a5afbf-cac1-4648-a1b0-c78840638a8e.png)

# Program :
```
Name:SADHANA R
Register No:25017643
Slot Name:3P1-1
```
```
import numpy as np
import math
import scipy.stats
L=[int(i)for i in input().split()]
N=len(L)
M=max(L)
X=list()
f=list()
for i in range(M+1):
  c=0
  for j in range(N):
    if L[j]==i:
      c=c+1
  f.append(c)
  X.append(i)
sf=np.sum(f)
p=list()
for i in range(M+1):
  p.append(f[i] /sf)
mean=np.inner(X,p)
p=list()
E=list()
xi=list()
print("X P(X=x)  Obs.Fr  Exp.Fr  xi")
print("------------------------------")
for x in range (M+1):
  p.append(math.exp(-mean)*mean**x / math.factorial(x))
  E.append(p[x]*sf) # Fixed this line as well. Previously it was p[x*sf] which seems like a typo.
  xi.append(((f[x]-E[x])**2)/E[x]) # Corrected the chi-square term to (Obs - Exp)^2 / Exp
  print("%2d  %.3f  %4d  %.2f  %.3f"%(x,p[x],f[x],E[x],xi[x]))
print("-----------------------------")
cal_chi2_sq=np.sum(xi)
print(f"Calculated value of Chi square is {cal_chi2_sq:.4f}")
table_chi2=scipy.stats.chi2.ppf(1-0.01,df=M)
print(f"Table value of Chi square at 1% level is {table_chi2:.4f}")
if cal_chi2_sq<table_chi2:
  print("The given data can be fitted in Poisson Distribution at 1% LOS")
else:
  print("The given data cannot be fitted in Poisson Distribution at 1% LOS")
```
 https://colab.research.google.com/drive/1E2Qlb3rZgWSM9Rz1n4mhxEsasEEdWTsO?usp=sharing

# Output : 
```
5 3 8 4 7 9 5 4 
X P(X=x)  Obs.Fr  Exp.Fr  xi
------------------------------
 0  0.004     0  0.03  0.029
 1  0.020     0  0.16  0.162
 2  0.057     0  0.46  0.456
 3  0.107     1  0.86  0.024
 4  0.150     2  1.20  0.527
 5  0.169     2  1.35  0.308
 6  0.159     0  1.27  1.269
 7  0.128     1  1.02  0.000
 8  0.090     1  0.72  0.112
 9  0.056     1  0.45  0.679
-----------------------------
Calculated value of Chi square is 3.5676
Table value of Chi square at 1% level is 21.6660
The given data can be fitted in Poisson Distribution at 1% LOS
```


# Results

The Poisson distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 
 
