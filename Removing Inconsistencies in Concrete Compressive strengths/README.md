# Removing Inconsistencies in Concrete Compressive strength
<img src = 'https://www.fprimec.com/wp-content/uploads/2016/09/Compressive-Strength-Of_Concrete-Kobe.jpg'></img>

# Problem Statement

Andrew had an hour-long meeting with Smith regarding the frequent complaints he
had been receiving from their existing clientele. Smith was the sales representative
at a construction aggregates company and was facing difficulties in meeting his sales
targets. Smith believed that the reason for his difficulties was that the existing clients had
complaints regarding quality inconsistencies—this, when coupled with negative word of
mouth in the market, was making it tough for him to seal deals with potential customers.
Andrew, the plant supervisor, was Smith’s friend. At first Smith tried to find a solution
for this problem, but when things got out of his control, he decided to have a meeting
with Andrew.

There is usually friction between the production and sales departments in most
companies. Both of them usually fight over their yearly budgets and their plans for
meeting their annual targets. Smith knew this but he felt sure that things would be
different with Andrew as they had been friends for some time. However, as the meeting
kicked off and Smith presented the matter to Andrew, to his dismay Andrew wasn’t ready
to acknowledge any inconsistencies in production. As Smith recalled Andrew saying,
“These complaints don’t make any sense to me. You ask why! Well first of all, we had an
upgrade at our production plant in the last quarter, and you know for a fact that the raw
material we use goes through a thorough testing prior to being used for production.”
The meeting didn’t help Smith in any way, and he let the matter go for some time.
One day, when he was in a networking session during one of his company’s corporate
events, Smith heard some executives from the production department talking about
the recent upgrade of the plant. He recalled hearing one of the executives say, “Though
we don’t have any testing improvement in our recent upgrade for measuring concrete
compressive strength, then too our product quality is superior thanks to our robust
testing of raw material used.”

When Smith heard this, he did some research and was surprised to discover that the
complaints had gained momentum ever since the upgrade had taken place. However, he
also discovered that the procurement of the testing equipment was put on hold due to a
shortage of funds allocated to the procurement department. Smith knew for a fact that he
couldn’t afford to wait until the next year for the issue to resolve on its own, and he had to
find a way to make things right.

**Our main aim is to find the factors that mostly contribute to determination of concrete compressive strength and help Smith in overcoming this problem of rising complaints about their product.**

# Some Key Analysis
### 1. Correlation between features
![download](https://user-images.githubusercontent.com/69857637/119699865-37feeb80-be70-11eb-967d-4f67f06d3802.png)

- The presence of outliers are negligible in any of these varaibles.
- In some of scatterplots we see that maximum values are lurking on zero. The variables in relationship with concrete strength are Fly ash,Age,Superplasticizer,Furnace Slag
- We can see positive , negative and in some plots negative correlations.
#### Positive correlation exist between
- Concrete Strength and cement component
- Concrete strength and superplasticizer
#### Negative correlation exist between
- Concrete strength and Water Component
- Concrete strength and fine aggregate
- Concrete strength and Coarse aggregate
- Concrete strength and Fly ash
#### No correlation
- concrete strength and age
- concrete strength and Furnace slag

### 2. Mulitcollinearity
![download (1)](https://user-images.githubusercontent.com/69857637/119700183-89a77600-be70-11eb-9648-e6734eaeb694.png)

In many of the cases feature pairs don’t have a correlation between them. Exception lies in two cases—that is, cement component and furnace slag and cement component and fly ash—where we can see a strong negative correlation

### 3.Simple Linear Regression
![download (2)](https://user-images.githubusercontent.com/69857637/119700379-c2474f80-be70-11eb-9cac-b49a6ecd9aa2.png)

cement_component ------> 0.24239757657889227

fly_ash        ------>  0.07658587994453692

water_component ------>  0.09926973338079692

superplasticizer ------> 0.05732699810729469

coarse_agg   ----->     0.010810583900674353

### 4. Multiple Linear Regression
![download (3)](https://user-images.githubusercontent.com/69857637/119700587-063a5480-be71-11eb-86d2-5a653b07ce02.png)

Features: ['cement_component', 'fly_ash', 'water_component', 'superplasticizer', 'coarse_agg']
R2_score: 0.080054
Intercept: 40.011990
Coefficients: [ 4.27092993 -2.16623978 -1.1613041   1.81687336 -0.41577903]

We had no success with Multiple Linear regression, Ridge regression, Lasso regression, Decision trees, Random Forests. However single Gradient Boosting trees were giving best of all results. Hence, Gradient Boosting trees were finalized for the model.

### 5. Gradient Boosting 
![download (4)](https://user-images.githubusercontent.com/69857637/119701548-156dd200-be72-11eb-9316-63e4f77b6316.png)

Here we see some better r2 score and also observe that cement_component gave the best result of r2_score of 0.32.

### Final Thoughts
From all the above models we come to know that our most important features were cement_component', 'water-component' & 'coarse-aggregate'. Thus we can predict the concrete strength from these variables.

Feature : cement_component

New data : 120.300000

The predicted value of concrete strength from cement_component is [22.61132185]

--------------------------------------------------------------------------------
Feature : water_component

New data : 312.000000

The predicted value of concrete strength from water_component is [29.55239704]

--------------------------------------------------------------------------------
Feature : coarse_agg

New data : 1100.000000

The predicted value of concrete strength from coarse_agg is [19.96449128]

--------------------------------------------------------------------------------

# Conclusion
- Although upgrade took place at plant , results are not satifactory, so a testing unit should be implanted in the plant.
- Since we have found out the factors that can predict the concrete strength, these factors should be given at most priority during testing and a threshold value should be set for production of better concrete.


