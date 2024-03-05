## Project Objective
In my study of the Titanic's passenger survival rates, I aim to explore different factors that may have influenced who survived and who didn't. In addition, I will also be looking at different groups of passengers to see which groups had the highest and lowest chances of surviving the disaster.

## Project Data Source
[Titanic Dataset](https://www.kaggle.com/competitions/titanic/data?select=train.csv) Provided by Kaggle

## Data Tools Used
* Python
* PowerBi

## Python Code
#### Upload and view data

```python
import pandas as pd
csv_file_path='C:\\Users\\....\\OneDrive\\Documents\\Data Analytics Course\\Capstone Project 4\\Titanic\\titanic.py.csv'
df=pd.read_csv(csv_file_path)
print(df)
```

![pic1_img](https://github.com/Scara98/Portfolio/blob/imgs/pic1_img)

#### Replace any null values with identifiable values
```python
replacement_values = {'PassengerId': 9999, 'Survived': 9999, 'Pclass': 9999, 'Name': 'N/A', 'Sex': 'N/A','Age': 9999, 'SibSp': 9999, 'Parch': 9999, 'Ticket': 'N/A', 'Fare': 9999, 'Cabin': 'N/A', 'Embarked': 'N/A'}
df.fillna(replacement_values, inplace=True)
df.to_csv(csv_file_path, index=False)
```

![pic2_img](https://github.com/Scara98/Portfolio/blob/imgs/pic2_img)

#### Count number of males and females who survived versus who passed away
```python
females_survived = df[(df['Sex'] == 'female') & (df['Survived'] == 1)].shape[0]
print('Number of female survivors:', females_survived)

females_passed = df[(df['Sex'] == 'female') & (df['Survived'] == 0)].shape[0]
print('Number of females who lost their lives:',females_passed)

males_survived = df[(df['Sex'] == 'male') & (df['Survived'] == 1)].shape[0]
print('Number of male survivors:',males_survived)

males_passed = df[(df['Sex'] == 'male') & (df['Survived'] == 0)].shape[0]
print('Number of males who lost their lives:',males_passed)
```

![pic3_img](https://github.com/Scara98/Portfolio/blob/imgs/pic3_img)

#### Comparing ticket classes and survival rate
```python
class1=df[(df['Pclass']==1)].shape[0]
print('Number of 1st class passengers:', class1)
class1_survived=df[(df['Pclass']==1) & (df['Survived']==1)].shape[0]
print('Number of 1st class passengers that survived:', class1_survived)

class2=df[(df['Pclass']==2)].shape[0]
print('Number of 2nd class passengers:', class2)
class2_survived=df[(df['Pclass']==2) & (df['Survived']==1)].shape[0]
print('Number of 2nd class passengers that survived:', class2_survived)

class3=df[(df['Pclass']==3)].shape[0]
print('Number of 3rd class passengers:', class3)
class3_survived=df[(df['Pclass']==3) & (df['Survived']==1)].shape[0]
print('Number of 3rd class passengers that survived:', class3_survived)
```

![pic5_img](https://github.com/Scara98/Portfolio/blob/imgs/pic5_img)

#### Ticket class and sex determining survival rate
```python
class4=df[(df['Pclass']==1) & (df['Sex']== 'female')].shape[0]
print('Number of 1st class female passengers:', class4)
class4_survived=df[(df['Pclass']==1) & (df['Sex']== 'female') & (df['Survived']==1)].shape[0]
print('Number of 1st class female passengers that survived:', class4_survived)

class7=df[(df['Pclass']==1) & (df['Sex']== 'male')].shape[0]
print('Number of 1st class male passengers:', class7)
class7_survived=df[(df['Pclass']==1) & (df['Sex']== 'male') & (df['Survived']==1)].shape[0]
print('Number of 1st class male passengers that survived:', class7_survived)
```

The code was repeated for classes 2 and 3 for both males and females. 

![pic6_img](https://github.com/Scara98/Portfolio/blob/imgs/pic6_img)

![image1.png](https://github.com/Scara98/Portfolio/blob/imgs/image1.png)

This shows that as passenger class decreased, so did survival rates. First-class females had the highest survival rate at 97%, followed by second class at 92%, and third class at 50%. For males, the trend was similar, with first class at 37%, second class at 16%, and third class at 14%. This indicates a clear link between class and survival chances. Additionally, females overall had significantly higher survival rates compared to males.

#### Count number of males and females split by age survival rate
```python
childrenf=df[(df['Sex']== 'female') & (df['Age']<=17)].shape[0]
print('Number of females under 18:', childrenf)
childrenf_survived = df[(df['Sex'] == 'female') & (df['Survived'] == 1) & (df['Age']<= 17)].shape[0]
print('Number of females under 18 who survived:', childrenf_survived)

adultf=df[(df['Sex']== 'female') & (df['Age']>=18) & (df['Age']<=64)].shape[0]
print('Number of females aged 18-64:', adultf)
adultf_survived = df[(df['Sex'] == 'female') & (df['Survived'] == 1) & (df['Age']>= 18) & (df['Age']<=64)].shape[0]
print('Number of females aged 18-64 who survived:', adultf_survived)

elderf=df[(df['Sex']== 'female') & (df['Age']>=65) & (df['Age']<9999)].shape[0]
print('Number of females 65 and over:', elderf)
elderf_survived = df[(df['Sex'] == 'female') & (df['Survived'] == 1) & (df['Age']>= 65) & (df['Age']<9999)].shape[0]
print('Number of females 65 and over who survived:', elderf_survived)

unknownf=df[(df['Sex']=='female') & (df['Age']==9999)].shape[0]
print('Number of unrecorded age females:', unknownf)
unknownf_survived=df[(df['Sex']=='female') & (df['Survived']==1) & (df['Age']==9999)].shape[0]
print('Number of unrecorded age females who survived:', unknownf_survived)
```

The same code was repeated for males. 

![pic4_img](https://github.com/Scara98/Portfolio/blob/imgs/pic4_img)

![img7](https://github.com/Scara98/Portfolio/blob/imgs/img7.png)

Among males, those under 18 had a 40% survival rate, which decreased to 18% for those aged 18-64, and further to 9% for those 65 and older. Females under 18 had a 69% survival rate, while those aged 18-64 had a higher rate of 77%. There were no females 65 and older recorded. Males with unknown ages had a 13% survival rate, while females with unknown ages had 68%. Younger males had higher survival rates, but this correlation didn't apply to females, as older females had higher survival rates compared to younger ones.


#### Survival rate by cabin
```python
cabina = df[df['Cabin'].str.startswith('A', na=False)].shape[0]
print('Number of passengers in Cabin A:', cabina)
cabina_survived= df[(df['Cabin'].str.startswith('A', na=False)) & (df['Survived']==1)].shape[0]
print('Number of Cabin A passengers that survived:', cabina_survived)

cabinb = df[df['Cabin'].str.startswith('B', na=False)].shape[0]
print('Number of passengers in Cabin B:', cabinb)
cabinb_survived= df[(df['Cabin'].str.startswith('B', na=False)) & (df['Survived']==1)].shape[0]
print('Number of Cabin B passengers that survived:', cabinb_survived)
```

The same code was repeated for passengers in Cabins C, D, E, F, G, T, and passengers not listed in a Cabin.

![pic7_img](https://github.com/Scara98/Portfolio/blob/imgs/pic7_img)

![img3](https://github.com/Scara98/Portfolio/blob/imgs/img3.png)

Males in cabins had a 42% survival rate, compared to only 14% for those not in cabins. Similarly, females in cabins had a high survival rate of 94%, while those not in cabins had a lower rate of 65%. The data indicates that both men and women had significantly higher survival rates when they were in cabins.

#### Survival based on where passengers embarked
```python
embarkc=df[df['Embarked']=='C'].shape[0]
print('Number of people who boarded in Cherbourg:', embarkc)
embarkc_survived=df[(df['Embarked']=='C') & (df['Survived']==1)].shape[0]
print('Number of people who boarded in Cherbourg that survived:', embarkc_survived)

embarks=df[df['Embarked']=='S'].shape[0]
print('Number of people who boarded in Southampton:', embarks)
embarks_survived=df[(df['Embarked']=='S') & (df['Survived']==1)].shape[0]
print('Number of people who boarded in Southampton that survived:', embarks_survived)

embarkq=df[df['Embarked']=='Q'].shape[0]
print('Number of people who boarded in Queenstown:', embarkq)
embarkq_survived=df[(df['Embarked']=='Q') & (df['Survived']==1)].shape[0]
print('Number of people who boarded in Queenstown that survived:', embarkq_survived)

embarkna=df[df['Embarked']=='N/A'].shape[0]
print('Number of people who boarded in an unknown location:', embarkna)
embarkna_survived=df[(df['Embarked']=='N/A') & (df['Survived']==1)].shape[0]
print('Number of people who boarded in an unknown location that survived:', embarkna_survived)
```

![pic8_img](https://github.com/Scara98/Portfolio/blob/imgs/pic8_img)

![img2.png](https://github.com/Scara98/Portfolio/blob/imgs/img2.png)

Males boarding in Southampton had a survival rate of 17%, while those in Cherbourg had a higher rate of 31%, and those in Queenstown had the lowest rate at 7%. Conversely, females boarding in Southampton had a survival rate of 69%, those in Cherbourg had the highest rate at 88%, and those in Queenstown had a survival rate of 75%. Notably, two female passengers without recorded embarkation points both survived.Cherbourg had the highest survival rate overall, but the pattern differed between males and females across embarkation points.

#### Survival based on fare paid
```python
fare10=df[df['Fare']<=9.99].shape[0]
print('Number of people who paid under $10 for their fare:', fare10)
fare10_survived=df[(df['Fare']<=9.99) & (df['Survived']==1)].shape[0]
print('Number of people who paid under $10 fare who survived:', fare10_survived)

fare30=df[(df['Fare']>=10) & (df['Fare']<=29.99)].shape[0]
print('Number of people who paid between $10 to $29.99 for their fare:', fare30)
fare30_survived=df[(df['Fare']>=10) & (df['Fare']<=29.99) & (df['Survived']==1)].shape[0]
print('Number of people who paid between $10 to $29.99 fare who survived:', fare30_survived)

fare100=df[(df['Fare']>=30) & (df['Fare']<=99.99)].shape[0]
print('Number of people who paid between $30 to $99.99 for their fare:', fare100)
fare100_survived=df[(df['Fare']>=30) & (df['Fare']<=99.99) & (df['Survived']==1)].shape[0]
print('Number of people who paid between $30 to $99.99 fare who survived:', fare100_survived)

fare500=df[df['Fare']>=100].shape[0]
print('Number of people who paid $100 or more for their fare:', fare500)
fare500_survived=df[(df['Fare']>=100) & (df['Survived']==1)].shape[0]
print('Number of people who paid $100 or more fare who survived:', fare500_survived)
```

![pic9_img](https://github.com/Scara98/Portfolio/blob/imgs/pic9_img)

![img4.png](https://github.com/Scara98/Portfolio/blob/imgs/img4.png)

Among males, those who paid under $10 had an 11% survival rate, which increased to 21% for fares between $10 and $29.99, further to 33% for fares between $30 and $99.99, and peaked at 37% for fares of $100 or more. Similarly, females who paid under $10 had a 59% survival rate, which rose to 71% for fares between $10 and $29.99, further to 83% for fares between $30 and $99.99, and reached the highest rate of 94% for fares of $100 or more. This data indicates that both male and female passengers had better chances of survival as the fare they paid increased.

#### Using fare and class to determine survival rate
```python
fare10_1=df[(df['Fare']<=9.99) & (df['Pclass']==1)].shape[0]
print('Number of people in 1st class who paid under $10 for their fare:', fare10_1)
fare10_1_survived=df[(df['Fare']<=9.99) & (df['Pclass']==1) & (df['Survived']==1)].shape[0]
print('Number of people in 1st class who paid under $10 fare who survived:', fare10_1_survived)

fare30_1=df[(df['Fare']>=10) & (df['Fare']<=29.99) & (df['Pclass']==1)].shape[0]
print('Number of people in 1st class who paid between $10 to $29.99 for their fare:', fare30_1)
fare30_1_survived=df[(df['Fare']>=10) & (df['Fare']<=29.99) & (df['Pclass']==1) & (df['Survived']==1)].shape[0]
print('Number of people in 1st class who paid between $10 to $29.99 fare who survived:', fare30_1_survived)

fare100_1=df[(df['Fare']>=30) & (df['Fare']<=99.99) & (df['Pclass']==1)].shape[0]
print('Number of people in 1st class who paid between $30 to $99.99 for their fare:', fare100_1)
fare100_1_survived=df[(df['Fare']>=30) & (df['Fare']<=99.99) & (df['Pclass']==1) & (df['Survived']==1)].shape[0]
print('Number of people in 1st class who paid between $30 to $99.99 fare who survived:', fare100_1_survived)

fare500_1=df[(df['Fare']<=100) & (df['Pclass']==1)].shape[0]
print('Number of people in 1st class who paid $100 or more for their fare:', fare500_1)
fare500_1_survived=df[(df['Fare']<=100) & (df['Pclass']==1) & (df['Survived']==1)].shape[0]
print('Number of people in 1st class who paid $100 or more for their fare who survived:', fare500_1_survived)
```

The same code was repeated for passengers in 2nd and 3rd class. 

![pic10_img](https://github.com/Scara98/Portfolio/blob/imgs/pic10_img)

![img14.png](https://github.com/Scara98/Portfolio/blob/imgs/img14.png) 

The following was concluded for survival rates based on passengers' class and fare paid:

1st class passengers:
Under $10: 0% survival rate.
$10 to $29.99: 47% survival rate.
$30 to $99.99: 66% survival rate.
$100 or more: 74% survival rate.

2nd class passengers:
Under $10: 0% survival rate.
$10 to $29.99: 48% survival rate.
$30 to $99.99: 56% survival rate.
No passengers were recorded paying $100 or more in this class.

3rd class passengers:
Under $10: 21% survival rate.
$10 to $29.99: 35% survival rate.
$30 to $99.99: 20% survival rate.
No passengers were recorded paying $100 or more in this class.

In conclusion, for 1st and 2nd class passengers, higher fares correlated with higher survival rates. However for 3rd class passengers, higher fares did not necessarily correlate with higher survival rates; those who paid the most had the lowest survival rate.

#### Survival rate for siblings/spouse number
```python
sibsp0=df[df['SibSp']==0].shape[0]
print('Number of passengers with zero siblings or spouse on board:', sibsp0)
sibsp0_survived=df[(df['SibSp']==0) & (df['Survived']==1)].shape[0]
print('Number of passengers with zero siblings or spouse on board who survived:', sibsp0_survived)

sibsp1=df[df['SibSp']==1].shape[0]
print('Number of passengers with one sibling or spouse on board:', sibsp1)
sibsp1_survived=df[(df['SibSp']==1) & (df['Survived']==1)].shape[0]
print('Number of passengers with one sibling or spouse on board who survived:', sibsp1_survived)
```
The same code was repeated for passengers with 2, 3, 4, 5, and 8 siblings/spouse listed. 

![pic11_img](https://github.com/Scara98/Portfolio/blob/imgs/pic11_img)

![img5.png](https://github.com/Scara98/Portfolio/blob/imgs/img5.png)

The passengers' survival rates based on this factor are as follows:

Males:
No siblings or spouse: 17% survival rate.
1 sibling or spouse: 31% survival rate.
2 siblings and/or spouse: 20% survival rate.
3 siblings and/or spouse: 0% survival rate.
4 siblings and/or spouse: 8% survival rate.
5 siblings and/or spouse: 0% survival rate.
8 siblings and/or spouse: 0% survival rate.

Females:
No siblings or spouse: 79% survival rate.
1 sibling or spouse: 75% survival rate.
2 siblings and/or spouse: 77% survival rate.
3 siblings and/or spouse: 36% survival rate.
4 siblings and/or spouse: 33% survival rate.
5 siblings and/or spouse: 0% survival rate.
8 siblings and/or spouse: 0% survival rate.

This data shows that both males and females experienced fluctuating survival rates based on the number of siblings and or spouse aboard. No specific trend for males or females survival rate in correlation to the number of siblings and or spouse they had aboard.

#### Number of children/parents on board survival rate
```python
fam0=df[df['Parch']==0].shape[0]
print('Number of passengers with zero children or parents on board:', fam0)
fam0_survived=df[(df['Parch']==0) & (df['Survived']==1)].shape[0]
print('Number of passengers with zero children or parents on board who survived:', fam0_survived)

fam1=df[df['Parch']==1].shape[0]
print('Number of passengers with one child or parent on board:', fam1)
fam1_survived=df[(df['Parch']==1) & (df['Survived']==1)].shape[0]
print('Number of passengers with one child or parent on board who survived:', fam1_survived)
```
The same code was repeated for passengers with 2, 3, 4, 5, and 6 parents/children listed. 

![pic12_img](https://github.com/Scara98/Portfolio/blob/imgs/pic12_img)

![img.6png](https://github.com/Scara98/Portfolio/blob/imgs/img6.png)

For males, those with no children or parents on board had a survival rate of 17%. This rate increased to 33% when they had one child or parent. However, having two recorded for children and or parents resulted in a slightly lower survival rate of 32%. Notably, having 3, 4, or 5 recorded for children or parents led to a 0% survival rate. Similarly, females with no children or parents aboard had a high survival rate of 79%. This rate decreased slightly to 77% when they had one child or parent on board. However, having two recorded for children and or parents decreased the survival rate to 61%. Interestingly, having three children or parents increased the survival rate to 75%, but having four resulted in a 0% survival rate. Furthermore, having five led to a 25% survival rate, while having six resulted in a 0% survival rate. In summary, both males and females experienced fluctuations in survival rates based on the number of children or parents aboard, showing no clear trends for survival rates.

The following information shows the survival rates of the male and female passengers on board based on their parch:

Males:
No children or parents: 17% survival rate.
1 child or parent: 33% survival rate.
2 children and/or parents: 32% survival rate.
3 children and/or parents: 0% survival rate.
4 children and/or parents: 0% survival rate.
5 children and/or parents: 0% survival rate.
No males were recorded as having 6 children and/or parents aboard.

Females:
No children or parents: 79% survival rate.
1 child or parent: 77% survival rate.
2 children and/or parents: 61% survival rate.
3 children and/or parents: 75% survival rate.
4 children and/or parents: 0% survival rate.
5 children and/or parents: 25% survival rate.
6 children and/or parents: 0% survival rate.

Both males and females experienced fluctuations in survival rates based on the number of children and or parents aboard; this shows that there were no clear trends for survival rates based on the number of children and or parents passengers had aboard.

#### Highest survival rate when combining sex and class with third factor
```python
#highest percent combo(over 23ppl) out of all sex, class, and fare combinations
combo1=df[(df['Pclass']==1) & (df['Sex']== 'female') & (df['Fare']>=30) & (df['Fare']<=99.99)].shape[0]
print('Number of 1st class female passengers who paid between $30 to $99.99:', combo1)
combo1_survived=df[(df['Pclass']==1) & (df['Sex']== 'female') & (df['Fare']>=30) & (df['Fare']<=99.99) & (df['Survived']==1)].shape[0]
print('Number of 1st class female passengers who paid $30 to $99.99 that survived:', combo1_survived)

#highest percent combo(over 23ppl) out of all sex, class, and Embarked combinations
combo2=df[(df['Pclass']==1) & (df['Sex']== 'female') & (df['Embarked']=='C')].shape[0]
print('Number of 1st class female passengers who boarded in Cherbourg:', combo2)
combo2_survived=df[(df['Pclass']==1) & (df['Sex']== 'female') & (df['Embarked']=='C') & (df['Survived']==1)].shape[0]
print('Number of 1st class female passengers who boarded in Cherbourg that survived:', combo2_survived)

#highest percent combo(over 23ppl) out of all sex, class, and Cabin combinations
combo3=df[(df['Pclass']==1) & (df['Sex']== 'female') & (df['Cabin'].str.startswith('B', na=False))].shape[0]
print('Number of 1st class female passengers who were in Cabin B:', combo3)
combo3_survived=df[(df['Pclass']==1) & (df['Sex']== 'female') & (df['Cabin'].str.startswith('B', na=False)) & (df['Survived']==1)].shape[0]
print('Number of 1st class female passengers who were in Cabin B that survived:', combo3_survived)

#highest percent combo (over 23ppl) out of all sex, class, and Parch combinations
combo4=df[(df['Pclass']==1) & (df['Sex']== 'female') & (df['Parch']==0)].shape[0]
print('Number of 1st class female passengers who had no children or parents aboard:', combo4)
combo4_survived=df[(df['Pclass']==1) & (df['Sex']== 'female') & (df['Parch']==0) & (df['Survived']==1)].shape[0]
print('Number of 1st class female passengers who had no children or parents aboard that survived:', combo4_survived)

#highest percent combo (over 23ppl) out of all sex, class, and SibSp combinations
combo5=df[(df['Pclass']==1) & (df['Sex']== 'female') & (df['SibSp']==0)].shape[0]
print('Number of 1st class female passengers who had no siblings or spouse aboard:', combo5)
combo5_survived=df[(df['Pclass']==1) & (df['Sex']== 'female') & (df['SibSp']==0) & (df['Survived']==1)].shape[0]
print('Number of 1st class female passengers who had no siblings or spouse aboard that survived:', combo5_survived)

#highest percent combo (over 23ppl) out of all sex, class, and Age combinations
combo6=df[(df['Sex']== 'female') & (df['Age']>=18) & (df['Age']<=64) & (df['Pclass']==1)].shape[0]
print('Number of 1st class female passengers aged 18-64:', combo6)
combo6_survived = df[(df['Sex'] == 'female') & (df['Survived'] == 1) & (df['Age']>= 18) & (df['Age']<=64) & (df['Pclass']==1)].shape[0]
print('Number of 1st class female passengers aged 18-64 who survived:', combo6_survived)
```

Each combination was repeated with all classes, both sexes, and each different type within each category. For example using the cabins passengers stayed in with sex and class the code would be run with each different Cabin(A, B, C, D, E, F, G, T, N/A) and each Cabin would be tested with females in classes 1, 2, and 3 and also tested with males in classes 1, 2, and 3. So in this example using Cabins, there were 54 different combinations in total. The highest survival rate for each category is shown.

![pic13_img](https://github.com/Scara98/Portfolio/blob/imgs/pic13_img)

#### Lowest survival rate when combining sex and class with third factor
```python
#lowest percent combo(over 23ppl) out of all sex, class, and fare combinations
lcombo1=df[(df['Pclass']==3) & (df['Sex']== 'male') & (df['Fare']<=9.99)].shape[0]
print('Number of 3rd class male passengers who paid under $10:', lcombo1)
lcombo1_survived=df[(df['Pclass']==3) & (df['Sex']== 'male') & (df['Fare']<=9.99) & (df['Survived']==1)].shape[0]
print('Number of 3rd class male passengers who paid under $10 that survived:', lcombo1_survived)

#lowest percent combo(over 23ppl) out of all sex, class, and Embarked combinations
lcombo2=df[(df['Pclass']==3) & (df['Sex']== 'male') & (df['Embarked']=='Q')].shape[0]
print('Number of 3rd class male passengers who boarded in Queenstown:', lcombo2)
lcombo2_survived=df[(df['Pclass']==3) & (df['Sex']== 'male') & (df['Embarked']=='Q') & (df['Survived']==1)].shape[0]
print('Number of 3rd class male passengers who boarded in Queenstown that survived:', lcombo2_survived)

#lowest percent combo(over 23ppl) out of all sex, class, and Cabin combinations
lcombo3=df[(df['Pclass']==2) & (df['Sex']== 'male') & (df['Cabin']=='N/A')].shape[0]
print('Number of 2nd class male passengers who were in an unknown Cabin:', lcombo3)
lcombo3_survived=df[(df['Pclass']==2) & (df['Sex']== 'male') & (df['Cabin']=='N/A') & (df['Survived']==1)].shape[0]
print('Number of 2nd class male passengers who were in an unknown Cabin that survived:', lcombo3_survived)

#lowest percent combo (over 23ppl) out of all sex, class, and Parch combinations
lcombo4=df[(df['Pclass']==2) & (df['Sex']== 'male') & (df['Parch']==0)].shape[0]
print('Number of 2nd class male passengers who had no children or parents aboard:', lcombo4)
lcombo4_survived=df[(df['Pclass']==2) & (df['Sex']== 'male') & (df['Parch']==0) & (df['Survived']==1)].shape[0]
print('Number of 2nd class male passengers who had no children or parents aboard that survived:', lcombo4_survived)

#lowest percent combo (over 23ppl) out of all sex, class, and SibSp combinations
lcombo5=df[(df['Pclass']==2) & (df['Sex']== 'male') & (df['SibSp']==0)].shape[0]
print('Number of 2nd class male passengers who had no siblings or spouse aboard:', lcombo5)
lcombo5_survived=df[(df['Pclass']==2) & (df['Sex']== 'male') & (df['SibSp']==0) & (df['Survived']==1)].shape[0]
print('Number of 2nd class male passengers who had no siblings or spouse aboard that survived:', lcombo5_survived)

#lowest percent combo (over 23ppl) out of all sex, class, and Age combinations
lcombo6=df[(df['Sex']== 'male') & (df['Age']>=18) & (df['Age']<=64) & (df['Pclass']==2)].shape[0]
print('Number of 2nd class male passengers aged 18-64:', lcombo6)
lcombo6_survived = df[(df['Sex'] == 'male') & (df['Survived'] == 1) & (df['Age']>= 18) & (df['Age']<=64) & (df['Pclass']==2)].shape[0]
print('Number of 2nd class male passengers aged 18-64 who survived:', lcombo6_survived)
```

Each combination was repeated with all classes, both sexes, and each different type within each category. For example using the point where passengers Embarked with sex and class the code would be run with each different embarkation point(C, S, Q, N/A) and each embarkation point would be tested with females in classes 1, 2, and 3 and also tested with males in classes 1, 2, and 3. So in this example using Embarkation point, there were 24 different combinations in total. The lowest survival rate for each category is shown.

![pic14_img](https://github.com/Scara98/Portfolio/blob/imgs/pic14_img)

![img8](https://github.com/Scara98/Portfolio/blob/imgs/img8.png)

97% of first class females ages 18-64 survived verses only 7% of second class males ages 18-64 survived. 

![img9](https://github.com/Scara98/Portfolio/blob/imgs/img9.png)

100% of first class females in cabin B survived versus the 13% of second class males who were not in a cabin survived.

![img10](https://github.com/Scara98/Portfolio/blob/imgs/img10.png)

98% of first class females who embarked in Cherbourg survived whereas 8% of third class males who embarked in Queenstown survived. 

![img11](https://github.com/Scara98/Portfolio/blob/imgs/img11.png)

100% of first class females who paid $30-$99.99 survived but only 11% of third class males who paid under $10 survived.

![img12](https://github.com/Scara98/Portfolio/blob/imgs/img12.png)

98% of first class females who had no children or parents on board had a 98% survival rate and second class males who had no children or parents on board only had a 9% rate.

![img13](https://github.com/Scara98/Portfolio/blob/imgs/img13.png)

98% of first class females with no spouse or siblings on board survived but only 12% of second class males with no siblings or spouse survived. 

## Data Conclussions
Sex, Class, Fare, and being in a Cabin were factors that contributed to survival rate. When running all the different combinations no other factors were consistant in survival rate like sex and class were. First class females having the highest percentage rate of survival in all combinations using sex and class. Males in second class had the lowest survival rate in four out of six combinations whereas third class males had the lowest rate for two out of the six combinations.
