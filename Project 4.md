## Project Objective
Figure out what factors may have contributed to passengers' survival rate. Take a look at which groups of people had the highest survival rate versus passengers who had the lowest survival rate. 

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
![pic1_img](https://github.com/Scara98/Portfolio/blob/main/pic1_img)
#### Replace any null values with identifiable values
```python
replacement_values = {'PassengerId': 9999, 'Survived': 9999, 'Pclass': 9999, 'Name': 'N/A', 'Sex': 'N/A','Age': 9999, 'SibSp': 9999, 'Parch': 9999, 'Ticket': 'N/A', 'Fare': 9999, 'Cabin': 'N/A', 'Embarked': 'N/A'}
df.fillna(replacement_values, inplace=True)
df.to_csv(csv_file_path, index=False)
```
![pic2_img](https://github.com/Scara98/Portfolio/blob/main/pic2_img)
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

childrenm=df[(df['Sex']== 'male') & (df['Age']<=17)].shape[0]
print('Number of males under 18:', childrenm)
childrenm_survived = df[(df['Sex'] == 'male') & (df['Survived'] == 1) & (df['Age']<= 17)].shape[0]
print('Number of males under 18 who survived:', childrenm_survived)

adultm=df[(df['Sex']== 'male') & (df['Age']>=18) & (df['Age'] <=64)].shape[0]
print('Number of males aged 18-64:', adultm)
adultm_survived = df[(df['Sex'] == 'male') & (df['Survived'] == 1) & (df['Age']>= 18) & (df['Age']<=64)].shape[0]
print('Number of males aged 18-64 who survived:', adultm_survived)

elderm=df[(df['Sex']== 'male') & (df['Age']>=65) & (df['Age']<9999)].shape[0]
print('Number of males 65 and over:', elderm)
elderm_survived = df[(df['Sex'] == 'male') & (df['Survived'] == 1) & (df['Age']>= 65) & (df['Age']<9999)].shape[0]
print('Number of males 65 and over who survived:', elderm_survived)

unknownm=df[(df['Sex']=='male') & (df['Age']==9999)].shape[0]
print('Number of unrecorded age males:', unknownm)
unknownm_survived=df[(df['Sex']=='male') & (df['Survived']==1) & (df['Age']==9999)].shape[0]
print('Number of unrecorded age males who survived:', unknownm_survived)
```

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

#### Ticket class and sex determining survival rate
```python
class4=df[(df['Pclass']==1) & (df['Sex']== 'female')].shape[0]
print('Number of 1st class female passengers:', class4)
class4_survived=df[(df['Pclass']==1) & (df['Sex']== 'female') & (df['Survived']==1)].shape[0]
print('Number of 1st class female passengers that survived:', class4_survived)

class5=df[(df['Pclass']==2) & (df['Sex']== 'female')].shape[0]
print('Number of 2nd class female passengers:', class5)
class5_survived=df[(df['Pclass']==2) & (df['Sex']== 'female') & (df['Survived']==1)].shape[0]
print('Number of 2nd class female passengers that survived:', class5_survived)

class6=df[(df['Pclass']==3) & (df['Sex']== 'female')].shape[0]
print('Number of 3rd class female passengers:', class6)
class6_survived=df[(df['Pclass']==3) & (df['Sex']== 'female') & (df['Survived']==1)].shape[0]
print('Number of 3rd class female passengers that survived:', class6_survived)

class7=df[(df['Pclass']==1) & (df['Sex']== 'male')].shape[0]
print('Number of 1st class male passengers:', class7)
class7_survived=df[(df['Pclass']==1) & (df['Sex']== 'male') & (df['Survived']==1)].shape[0]
print('Number of 1st class male passengers that survived:', class7_survived)

class8=df[(df['Pclass']==2) & (df['Sex']== 'male')].shape[0]
print('Number of 2nd class male passengers:', class8)
class8_survived=df[(df['Pclass']==2) & (df['Sex']== 'male') & (df['Survived']==1)].shape[0]
print('Number of 2nd class male passengers that survived:', class8_survived)

class9=df[(df['Pclass']==3) & (df['Sex']== 'male')].shape[0]
print('Number of 3rd class male passengers:', class9)
class9_survived=df[(df['Pclass']==3) & (df['Sex']== 'male') & (df['Survived']==1)].shape[0]
print('Number of 3rd class male passengers that survived:', class9_survived)
```

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

cabinc = df[df['Cabin'].str.startswith('C', na=False)].shape[0]
print('Number of passengers in Cabin C:', cabinc)
cabinc_survived= df[(df['Cabin'].str.startswith('C', na=False)) & (df['Survived']==1)].shape[0]
print('Number of Cabin C passengers that survived:', cabinc_survived)

cabind = df[df['Cabin'].str.startswith('D', na=False)].shape[0]
print('Number of passengers in Cabin D:', cabind)
cabind_survived= df[(df['Cabin'].str.startswith('D', na=False)) & (df['Survived']==1)].shape[0]
print('Number of Cabin D passengers that survived:', cabind_survived)

cabine = df[df['Cabin'].str.startswith('E', na=False)].shape[0]
print('Number of passengers in Cabin E:', cabine)
cabine_survived= df[(df['Cabin'].str.startswith('E', na=False)) & (df['Survived']==1)].shape[0]
print('Number of Cabin E passengers that survived:', cabine_survived)

cabinf = df[df['Cabin'].str.startswith('F', na=False)].shape[0]
print('Number of passengers in Cabin F:', cabinf)
cabinf_survived= df[(df['Cabin'].str.startswith('F', na=False)) & (df['Survived']==1)].shape[0]
print('Number of Cabin F passengers that survived:', cabinf_survived)

cabing = df[df['Cabin'].str.startswith('G', na=False)].shape[0]
print('Number of passengers in Cabin G:', cabing)
cabing_survived= df[(df['Cabin'].str.startswith('G', na=False)) & (df['Survived']==1)].shape[0]
print('Number of Cabin G passengers that survived:', cabing_survived)

cabint = df[df['Cabin'].str.startswith('T', na=False)].shape[0]
print('Number of passengers in Cabin T:', cabint)
cabint_survived= df[(df['Cabin'].str.startswith('T', na=False)) & (df['Survived']==1)].shape[0]
print('Number of Cabin T passengers that survived:', cabint_survived)

cabinna = df[df['Cabin']=='N/A'].shape[0]
print('Number of passengers in unknown Cabin:', cabinna)
cabinna_survived= df[(df['Cabin']=='N/A') & (df['Survived']==1)].shape[0]
print('Number of passengers in unknown Cabin that survived:', cabinna_survived)
```

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

#### Using fare and class to determine survival rate
```python
fare10_1=df[(df['Fare']<=9.99) & (df['Pclass']==1)].shape[0]
print('Number of people in 1st class who paid under $10 for their fare:', fare10_1)
fare10_1_survived=df[(df['Fare']<=9.99) & (df['Pclass']==1) & (df['Survived']==1)].shape[0]
print('Number of people in 1st class who paid under $10 fare who survived:', fare10_1_survived)

fare10_2=df[(df['Fare']<=9.99) & (df['Pclass']==2)].shape[0]
print('Number of people in 2nd class who paid under $10 for their fare:', fare10_2)
fare10_2_survived=df[(df['Fare']<=9.99) & (df['Pclass']==2) & (df['Survived']==1)].shape[0]
print('Number of people in 2nd class who paid under $10 fare who survived:', fare10_2_survived)

fare10_3=df[(df['Fare']<=9.99) & (df['Pclass']==3)].shape[0]
print('Number of people in 3rd class who paid under $10 for their fare:', fare10_3)
fare10_3_survived=df[(df['Fare']<=9.99) & (df['Pclass']==3) & (df['Survived']==1)].shape[0]
print('Number of people in 3rd class who paid under $10 fare who survived:', fare10_3_survived)

fare30_1=df[(df['Fare']>=10) & (df['Fare']<=29.99) & (df['Pclass']==1)].shape[0]
print('Number of people in 1st class who paid between $10 to $29.99 for their fare:', fare30_1)
fare30_1_survived=df[(df['Fare']>=10) & (df['Fare']<=29.99) & (df['Pclass']==1) & (df['Survived']==1)].shape[0]
print('Number of people in 1st class who paid between $10 to $29.99 fare who survived:', fare30_1_survived)

fare30_2=df[(df['Fare']>=10) & (df['Fare']<=29.99) & (df['Pclass']==2)].shape[0]
print('Number of people in 2nd class who paid between $10 to $29.99 for their fare:', fare30_2)
fare30_2_survived=df[(df['Fare']>=10) & (df['Fare']<=29.99) & (df['Pclass']==2) & (df['Survived']==1)].shape[0]
print('Number of people in 2nd class who paid between $10 to $29.99 fare who survived:', fare30_2_survived)

fare30_3=df[(df['Fare']>=10) & (df['Fare']<=29.99) & (df['Pclass']==3)].shape[0]
print('Number of people in 3rd class who paid between $10 to $29.99 for their fare:', fare30_3)
fare30_3_survived=df[(df['Fare']>=10) & (df['Fare']<=29.99) & (df['Pclass']==3) & (df['Survived']==1)].shape[0]
print('Number of people in 3rd class who paid between $10 to $29.99 fare who survived:', fare30_3_survived)

fare100_1=df[(df['Fare']>=30) & (df['Fare']<=99.99) & (df['Pclass']==1)].shape[0]
print('Number of people in 1st class who paid between $30 to $99.99 for their fare:', fare100_1)
fare100_1_survived=df[(df['Fare']>=30) & (df['Fare']<=99.99) & (df['Pclass']==1) & (df['Survived']==1)].shape[0]
print('Number of people in 1st class who paid between $30 to $99.99 fare who survived:', fare100_1_survived)

fare100_2=df[(df['Fare']>=30) & (df['Fare']<=99.99) & (df['Pclass']==2)].shape[0]
print('Number of people in 2nd class who paid between $30 to $99.99 for their fare:', fare100_2)
fare100_2_survived=df[(df['Fare']>=30) & (df['Fare']<=99.99) & (df['Pclass']==2) & (df['Survived']==1)].shape[0]
print('Number of people in 2nd class who paid between $30 to $99.99 fare who survived:', fare100_2_survived)

fare100_3=df[(df['Fare']>=30) & (df['Fare']<=99.99) & (df['Pclass']==3)].shape[0]
print('Number of people in 3rd class who paid between $30 to $99.99 for their fare:', fare100_3)
fare100_3_survived=df[(df['Fare']>=30) & (df['Fare']<=99.99) & (df['Pclass']==3) & (df['Survived']==1)].shape[0]
print('Number of people in 3rd class who paid between $30 to $99.99 fare who survived:', fare100_3_survived)

fare500_1=df[(df['Fare']<=100) & (df['Pclass']==1)].shape[0]
print('Number of people in 1st class who paid $100 or more for their fare:', fare500_1)
fare500_1_survived=df[(df['Fare']<=100) & (df['Pclass']==1) & (df['Survived']==1)].shape[0]
print('Number of people in 1st class who paid $100 or more for their fare who survived:', fare500_1_survived)

fare500_2=df[(df['Fare']<=100) & (df['Pclass']==2)].shape[0]
print('Number of people in 2nd class who paid $100 or more for their fare:', fare500_2)
fare500_2_survived=df[(df['Fare']<=100) & (df['Pclass']==2) & (df['Survived']==1)].shape[0]
print('Number of people in 2nd class who paid $100 or more for their fare who survived:', fare500_2_survived)

fare500_3=df[(df['Fare']<=100) & (df['Pclass']==3)].shape[0]
print('Number of people in 3rd class who paid $100 or more for their fare:', fare500_3)
fare500_3_survived=df[(df['Fare']<=100) & (df['Pclass']==3) & (df['Survived']==1)].shape[0]
print('Number of people in 3rd class who paid $100 or more for their fare who survived:', fare500_3_survived)
```

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

sibsp2=df[df['SibSp']==2].shape[0]
print('Number of passengers with two for siblings and/or spouse on board:', sibsp2)
sibsp2_survived=df[(df['SibSp']==2) & (df['Survived']==1)].shape[0]
print('Number of passengers with two for siblings and/or spouse on board who survived:', sibsp2_survived)

sibsp3=df[df['SibSp']==3].shape[0]
print('Number of passengers with three for siblings and/or spouse on board:', sibsp3)
sibsp3_survived=df[(df['SibSp']==3) & (df['Survived']==1)].shape[0]
print('Number of passengers with three for siblings and/or spouse on board who survived:', sibsp3_survived)

sibsp4=df[df['SibSp']==4].shape[0]
print('Number of passengers with four for siblings and/or spouse on board:', sibsp4)
sibsp4_survived=df[(df['SibSp']==4) & (df['Survived']==1)].shape[0]
print('Number of passengers with four for siblings and/or spouse on board who survived:', sibsp4_survived)

sibsp5=df[df['SibSp']==5].shape[0]
print('Number of passengers with five for siblings and/or spouse on board:', sibsp5)
sibsp5_survived=df[(df['SibSp']==5) & (df['Survived']==1)].shape[0]
print('Number of passengers with five for siblings and/or spouse on board who survived:', sibsp5_survived)

sibsp8=df[df['SibSp']==8].shape[0]
print('Number of passengers with eight for siblings and/or spouse on board:', sibsp8)
sibsp8_survived=df[(df['SibSp']==8) & (df['Survived']==1)].shape[0]
print('Number of passengers with eight for siblings and/or spouse on board who survived:', sibsp8_survived)
```

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

fam2=df[df['Parch']==2].shape[0]
print('Number of passengers with two for children and/or parents on board:', fam2)
fam2_survived=df[(df['Parch']==2) & (df['Survived']==1)].shape[0]
print('Number of passengers with two for children and/or parents on board who survived:', fam2_survived)

fam3=df[df['Parch']==3].shape[0]
print('Number of passengers with three for children and/or parents on board:', fam3)
fam3_survived=df[(df['Parch']==3) & (df['Survived']==1)].shape[0]
print('Number of passengers with three for children and/or parents on board who survived:', fam3_survived)

fam4=df[df['Parch']==4].shape[0]
print('Number of passengers with four for children and/or parents on board:', fam4)
fam4_survived=df[(df['Parch']==4) & (df['Survived']==1)].shape[0]
print('Number of passengers with four for children and/or parents on board who survived:', fam4_survived)

fam5=df[df['Parch']==5].shape[0]
print('Number of passengers with five for children and/or parents on board:', fam5)
fam5_survived=df[(df['Parch']==5) & (df['Survived']==1)].shape[0]
print('Number of passengers with five for children and/or parents on board who survived:', fam5_survived)

fam6=df[df['Parch']==6].shape[0]
print('Number of passengers with six for children and/or parents on board:', fam6)
fam6_survived=df[(df['Parch']==6) & (df['Survived']==1)].shape[0]
print('Number of passengers with six for children and/or parents on board who survived:', fam6_survived)
```

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

## Data Conclussions
Females had a higher survival rate than males with first class females having the highest percentage rate of survival in all combinations using sex and class. Males in second class had the lowest survival rate in four out of six combinations whereas third class males had the lowest rate for two out of the six combinations.
