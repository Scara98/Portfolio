## Project Objective
Using Census data from 2022, I wanted to find some of the differences in job occupation and median pay for black men, white men, black women and white women.

## Data Sources
Job occupation median pay dataset was found on Census website:
  
[B24012 Sex by Occupation and Median Earnings in the Past 12 Months (in 2022 Inflation-Adjusted Dollars) for the Civilian Employed Population 16 Years and Over](https://data.census.gov/table/ACSDT1Y2022.B24012?t=Occupation&g=010XX00US)
   
  
Job occupations held by people datasets were found on Census website:
  
[B24010B Sex by Occupation for the Civilian Employed Population 16 Years and Over (Black or African American Alone)](https://data.census.gov/table/ACSDT1Y2022.B24010B?q=United+States&t=Black+or+African+American:Employment)
    
[B24010A Sex by Occupation for the Civilian Employed Population 16 Years and Over (White Alone)](https://data.census.gov/table/ACSDT1Y2022.B24010A?q=United+States&t=Employment:White)

## Data Tools 
* Excel
* PowerBI

## Excel
#### View occupation earnings dataset
![Project3_img](https://github.com/Scara98/Portfolio/assets/150705975/dc4a5620-a47e-4cba-acc9-c66d25bd6459)

The dataset distinguishes median pay for occupations by sex; however, it does not provide a breakdown by race. Despite a thorough search, I was unable to locate a Census dataset that provides a breakdown of median pay for occupations by both sex and race.

#### View white job occupation dataset
![Project3_img2](https://github.com/Scara98/Portfolio/assets/150705975/fdd11ded-8ef5-4bfe-a8c2-85880fd7d9c2)

#### View black job occupation dataset
![Project3_img3](https://github.com/Scara98/Portfolio/assets/150705975/b4870527-dbe2-491b-89a3-514945a3d171)

#### Remove all annotation and margin of error columns from occupation earnings dataset
![Project3_img4](https://github.com/Scara98/Portfolio/assets/150705975/16a88cb1-9540-401f-acb5-580bcd932a3c)

#### Remove all annotation and margin of error columns from white job occupation dataset
![Project3_img5](https://github.com/Scara98/Portfolio/assets/150705975/016f3945-a0e3-44e4-b983-af00272a92cd)

#### Remove all annotation and margin of error columns from black job occupation dataset
![Project3_img6](https://github.com/Scara98/Portfolio/assets/150705975/b50705d5-dca9-485c-bd03-3b86c0a38e43)

I made the datasets more concise by removing unnecessary annotation and margin of error columns. This simplification enhances the clarity and ease of working with the data for my specific comparisons and analyses.

#### Calculate percent of white males and white females in each occupation using white job occupation dataset
![Project3_img7](https://github.com/Scara98/Portfolio/assets/150705975/6832c08c-dbbc-4ea4-a285-ad935db89df3)
![Project3_img8](https://github.com/Scara98/Portfolio/assets/150705975/34a9fff5-35f2-4649-a481-4d6f9c1fc30f)

#### Calculate percent of black males and black females in each occupation using black job occupation dataset
![Project3_img9](https://github.com/Scara98/Portfolio/assets/150705975/42dc50e5-f68b-4c46-ba0f-714eaedf2b1f)
![Project3_img10](https://github.com/Scara98/Portfolio/assets/150705975/22c59799-7c77-46bf-86f9-42c9d6015755)

I calculated the percentage of individuals in each job field by dividing the number of people in a specific job field by the respective group's total. This process was executed using Excel's division function for each job field. This involved dividing the number of people in a specific job field by the corresponding group total for white women, black women, white men, and black men.

#### Create a new dataset that has columns that contain occupation, median earnings, sex, race, and percent of people in occupation
![Project3_img11](https://github.com/Scara98/Portfolio/assets/150705975/a76e943f-7096-411a-aa8c-17ed1ebeb1f5)

#### Split the new dataset into four datasets, splitting them by sex and race(white male, black male, white female, black female)
![Project3_img12](https://github.com/Scara98/Portfolio/assets/150705975/545243e1-ade9-4812-8bd1-3718127ac970)
![Project3_img13](https://github.com/Scara98/Portfolio/assets/150705975/7d261a47-f64d-4919-a5d8-4fa4fe0addd9)
![Project3_img14](https://github.com/Scara98/Portfolio/assets/150705975/4f1a2cb1-a6bb-4687-b3fc-7502159d0128)
![Project3_img15](https://github.com/Scara98/Portfolio/assets/150705975/ad6d7745-7f39-4694-8528-68039eb27381)

#### Use the new dataset to compare median earning occupation of men versus women by dividing women median earning by men median earning for each listed job occupation then calculate average of these differences
![Project3_img16](https://github.com/Scara98/Portfolio/assets/150705975/865eecb6-1d44-4724-b26f-a54e38086ecd)


![Pic1](https://github.com/Scara98/Portfolio/assets/150705975/061c87c5-c990-4611-97ff-7d40b46593a0)

* 27% of black women work in an occupation where the median income is 50k or more
* 37% of black women work in an occupation where the median income is 31k or less

![Pic2](https://github.com/Scara98/Portfolio/assets/150705975/636936e1-2d33-441b-8e04-3714688738a7)

* 33% of white women work in an occupation where the median income is 50k or more
* 28% of white women work in an occupation where the median income is 31k or less

![Pic3](https://github.com/Scara98/Portfolio/assets/150705975/0180c013-290f-4ef9-8881-6c646c69417e)

* 41% of black men work in an occupation where the median income is 50k or more
* 24% of black men work in an occupation where the median income is 31k or less

![Pic4](https://github.com/Scara98/Portfolio/assets/150705975/8b3fd3fa-bc0e-43b5-a5e2-a3f73f4730dc)

* 59% of white men work in an occupation where the median income is 50k or more
* 14% of white men work in an occupation where the median income is 31k or less

## Data Conclusions
Examining the data reveals significant differences in occupational opportunities and income across gender and race. White men are notably more likely than others—32% more than black women, 26% more than white women, and 18% more than black men—to be in occupations with a median income of $50,000 or more. Conversely, black women are 23% more likely than white men, 13% more likely than black men, and 9% more likely than white women to be in occupations with a median income of $31,000 or less. There is a consistent gender pay gap, with men earning, on average, a 24% higher median income compared to women in similar occupations. Additionally, black men are 10% more likely than white men to be in occupations with a median income of $31,000 or lower.

