**Table of Contents**

=====================
[Introduction	4](#_Toc84790705)

[Data Processing	4](#_Toc84790706)

[Data Modelling	6](#_Toc84790707)

[Conclusion	7](#_Toc84790708)

























**Figures and Tables**


[Figure 1: Correlation matrix of dataset	6](#_Toc84791300)

[Figure 2: Grades distribution	6](#_Toc84791301)

[Figure 3: Model Performance	7](#_Toc84791302)



[Table 1: Feature Selection	4](#_Toc84791295)

[Table 2: Features Aggregation	5](#_Toc84791296)












# **Introduction**
`	`The final grade a student obtains in a course is affected by various metrics such as assignment scores, participation in the course, participation in discussions etc. If we can predict (with accuracy) the grade of students based on these metrics, the professor wouldn’t have to manually evaluate the performance of every student and he/she can focus on other things to make the course even better. Thus, in this project, we are going to build two machine learning models that will predict the grade of the students in an online course based on the data acquired from an online learning management system called Moodle.
# **Data Processing**
The main task performed during the data processing was feature selection and aggregation i.e., unnecessary features were removed and similar features were combined into ‘buckets’ (as shown in table 2). Features that had single unique values were removed as it would not be helpful in building the model. Also, the grade out of 100 was removed as it was basically the target variable itself. Likewise, ‘Status2’ was removed as it did not seem to affect the grade that much and would not be helpful in grade prediction (as shown in figure 1).

**Data Dictionary:**

- **Status0:** course / lectures / content related (Course module viewed, Course viewed, Course activity completion updated, Course module instance list viewed, Content page viewed, Lesson started, Lesson resumed, Lesson restarted, Lesson ended)
- **Status1:** assignment related (Quiz attempt reviewed, Quiz attempt submitted, Quiz attempt summary viewed, Quiz attempt viewed, Quiz attempt started, Question answered, Question viewed, Submission re-assessed, Submission assessed, Submission updated, Submission created, Submission viewed)
- **Status2:** grade related (Grade user report viewed, Grade overview report viewed, User graded, Grade deleted, User profile viewed, Recent activity viewed, User report viewed, Course user report viewed, Outline report viewed)
- **Status3:** forum related (Post updated, Post created, Discussion created, Some content has been posted, Discussion viewed)
- **9 grades** (Week2\_Quiz1, Week3\_MP1, ... Week7\_MP3)
- **36 logs** (Week1\_Stat0, Week1\_Stat1, Week1\_Stat2, Week1\_Stat3, …Week9\_Stat0, Week9\_Stat1, Week9\_Stat2, Week9\_Stat3)

*Table 1: Feature Selection*

| Removed Features |                                             | Reason |
| :--------------: | :-----------------------------------------: | :----: |
|                  |                                             |        |
|                  |                     ID                      |        | - Non-numeric and does not contain any relevant information for prediction                         |
|                  |                                             |        |                                                                                                    |
|                  |                Week1\_Stat1                 |        | - Contains only single unique value                                                                |
|                  |                                             |        |                                                                                                    |
|                  |                Week8\_Total                 |        | - It is essentially the same as the grade, which is the target variable for the predictive model   |
|                  |                                             |        |                                                                                                    |
|                  | <p>Stat2</p><p>(From combined features)</p> |        | - It did not have a meaningful correlation with the grades so it was deemed an unimportant feature |
|                  |                                             |        |                                                                                                    |
|                  |                                             |        |                                                                                                    |
*Table 2: Features Aggregation*

| Removed Features |         | Reason |
| :--------------: | :-----: | :----: |
|                  |         |        |
|                  |  Quiz   |        | - Quiz of week 2, 4, and 6 |
|                  |         |        |                            |
|                  |   MP    |        | - MP of week 3, 5, and 7   |
|                  |         |        |                            |
|                  |   PR    |        | - PR of week 3, 5, and 7   |
|                  |         |        |                            |
|                  | Status0 |        | - Stat0 of week 1 to 9     |
|                  |         |        |                            |
|                  | Status1 |        | - Stat1 of week 1 to 9     |
|                  |         |        |                            |
|                  | Status2 |        | - Stat2 of week 1 to 9     |
|                  |         |        |                            |
|                  | Status3 |        | - Stat3 of week 1 to 9     |

![](Aspose.Words.cda2408d-172c-4334-b89d-218dece9fd22.009.png)

*Figure 1: Correlation matrix of dataset*
# **Data Modelling**
`	`For modelling the data, the entire dataset was divided into training and test datasets in the ratio 70 to 30. As the distribution of the target variable (‘Grade’) was imbalanced (as shown in figure 2), the train and test datasets were stratified to address this problem. 

![](Aspose.Words.cda2408d-172c-4334-b89d-218dece9fd22.010.png)

*Figure 2: Grades distribution*



**Models Used**

For this project, two classification models were used viz. **Random Forest Classifier** and **Gaussian Naïve Bayes Classifier**. A basic model fitting and prediction were done using the training and test datasets and hyperparameters of Random Forest Classifier were tweaked to slightly increase the accuracy.

The performance of each model is shown in figure 3.

![](Aspose.Words.cda2408d-172c-4334-b89d-218dece9fd22.011.png)

*Figure 3: Model Performance*

`	`**Model Performance**

The RandomForestClassifier outperforms the GaussianNB in predicting student grades with higher accuracy of 93.94% than the GaussianNB, which has an accuracy of 78.7% in the test set. We can see a similar case in the validation accuracy.

A possible explanation for the underperformance of GaussianNB might be that it makes naive assumptions, such as assuming that all variables are uncorrelated with one another (which is not always correct like in our case). Furthermore, RandomForestClassifier has higher accuracy because it is generally good with numerical, categorical data, such as the data in our dataset.
# **Conclusion**
`	`At first, all of the features were fed into the model without aggregation which obtained a low accuracy (about 69%) in the Random Forest Classifier. The problem was solved by combining similar features into a single feature. 

Also, as the dataset was imbalanced (positively skewed) so the model was performing erratically in each re-run. It was solved by stratifying the train and test sets.

Overall, as the accuracy was only 94%, and thus, the model will incorrectly predict grades every now and then. However, it might be possible to increase the accuracy by feeding more data to the model.
9
