#                                          Summary - Project 2 - CFPB Consumer Complaints Modeling


The Consumer Financial Protection Bureau (CFPB) is a U.S. government agency that makes sure financial companies treat their customers fairly. Their website allows customers of financial services to file complaints against financial companies and banks against unfair treatment if these companies are unable to resolve complaints to the customer’s satisfaction.


When customers choose to complain to the CFPB, financial companies incur additional costs to resolve such complaints.


On receipt, the CFPB routes complaints to the financial companies, who generally respond to the consumer within 15 days.  Once a response is provided, one of two things can happen:
  
  
  In most cases, consumers accept the response or remediation offered by the financial companies,
  
  
  In other cases, they choose to dispute the resolution offered by the company.  (flagged in the 'Consumer disputed?' field).  In these situations,    the bank has to perform additional investigations, and possibly offer further relief to the customers.  As a result, the cost of dealing with        disputes can be high.


**1.** Explore the data, familiarize yourself with the fields and perform some EDA.


**2.** Set your X (predictor) and y (predicted) variables. 
Use only the below variables as your predictors.  Ignore the other variables in the dataset.
'Product', 'Sub-product', 'Issue', 'State', 'Tags', 'Submitted via',  'Company response to consumer', 'Timely response?'
Use 'Consumer disputed?' as your y-variable.  Be sure to convert your y-variable to 0s and 1s so your model can use it.
 For example, you can use label encoder as below, or any other method you are comfortable using:
from sklearn import preprocessing
le = preprocessing.LabelEncoder()
y = le.fit_transform(complaints['Consumer disputed?'])


**3.** Split your data into a test and train set.  Use an 80/20 train-test split, and random_state=123 for the train-test split.
For example, using the below, appropriately adjusted to the variable names you are using:
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state = 123)


**4.** Check what proportion of complaints in your training dataset are disputed.  If this proportion is less than 30%, use random undersampling with random_state = 123 to balance your dataset. 
For example, you could use the below (adjusted for your choice of variables etc)
from imblearn.under_sampling import RandomUnderSampler
undersampler = RandomUnderSampler(random_state=123)
X_train, y_train = undersampler.fit_resample(X, y)


**5.** Train a predictive model to predict whether a complaint would be disputed using XGBoost Classifier using random_state=123
For example, using the below:
model_xgb = XGBClassifier(random_state = 123)


**6. **Evaluate the model on the test set, and create the classification report and confusion matrix.  (Remember, when we say ‘True Positive’, ‘False Negative’ etc, the second word, positive or negative, denotes the ground truth; and the first word, True or False, indicates whether we predicted correctly.)


**7.** Calculate the total cost in dollars for the test set.  Establish the ‘base-case’, ie the total cost if you were not using a model, using the test set only. 


**8.** Use the cost structure explained earlier (ie, $600 total for every disputed complaint, and $100 for every non-disputed complaint, and $90 for the extra due diligence.)


**9.** Now calculate the total cost in dollars based on the model results in the confusion matrix.  The below graphic might help you.  But you are free to use your own methods.
