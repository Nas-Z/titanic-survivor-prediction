# titanic-survivor-prediction
This ML project explores the titanic dataset and train a model based on Random Forest algorithim to predict whether a specific passengers is survived or not.

## Dataest:
The dataset has multiple attributes that describe each passenger:
- Pclass: the passenger calss with 1, 2, or 3 where higher numbers indicates lower classes.
- SibSp: represents the number of siblings or spouses a passenger had aboard the Titanic.
- Parch: represents the number of parents or children a passenger had on board the ship.
- Embarked: indicates the port where passengers boarded the ship. The possible values are: "C" for Cherbourg, "Q" for Queenstown, and "S" for Southampton.

| PassengerId | Pclass | Name                                             | Sex    | Age  | SibSp | Parch | Ticket              | Fare     | Cabin | Embarked |
|-------------|--------|--------------------------------------------------|--------|------|-------|-------|---------------------|----------|-------|----------|
| 892         | 3      | Kelly, Mr. James                                 | male   | 34.5 | 0     | 0     | 330911              | 7.8292   | NaN   | Q        |
| 893         | 3      | Wilkes, Mrs. James (Ellen Needs)                 | female | 47.0 | 1     | 0     | 363272              | 7.0000   | NaN   | S        |
| 894         | 2      | Myles, Mr. Thomas Francis                        | male   | 62.0 | 0     | 0     | 240276              | 9.6875   | NaN   | Q        |
| 895         | 3      | Wirz, Mr. Albert                                 | male   | 27.0 | 0     | 0     | 315154              | 8.6625   | NaN   | S        |
| 896         | 3      | Hirvonen, Mrs. Alexander (Helga E Lindqvist)     | female | 22.0 | 1     | 1     | 3101298             | 12.2875  | NaN   | S        |
| ...         | ...    | ...                                              | ...    | ...  | ...   | ...   | ...                 | ...      | ...   | ...      |
| 1305        | 3      | Spector, Mr. Woolf                               | male   | NaN  | 0     | 0     | A.5. 3236           | 8.0500   | NaN   | S        |
| 1306        | 1      | Oliva y Ocana, Dona. Fermina                      | female | 39.0 | 0     | 0     | PC 17758            | 108.9000 | C105  | C        |
| 1307        | 3      | Saether, Mr. Simon Sivertsen                     | male   | 38.5 | 0     | 0     | SOTON/O.Q. 3101262  | 7.2500   | NaN   | S        |
| 1308        | 3      | Ware, Mr. Frederick                              | male   | NaN  | 0     | 0     | 359309              | 8.0500   | NaN   | S        |
| 1309        | 3      | Peter, Master. Michael J                         | male   | NaN  | 1     | 1     | 2668                | 22.3583  | NaN   | C        |



## Preprocessing Data Pipeline:
By exploring the dataset I noticed some data that must be handled:
- There are some missing values in Age column.
- There are categorical columns like `Sex` and `Embarked`.
- Some columns are not helpful for training such as `Name`, `Ticket`.

So, to preprocess the data we need the following pipeline:

### 1. Age Imputer:
Filling the missing values of `Age` column with the average (mean).

### 2. Feature Encoder:
Convert categorical columns into numbers to be meaningful in the training process. The method used is One-Hot encoding which turns them into 1s and 0s.

### 3. Feature Dropper:
Drop columns we don't need for they are not helpful in training.

### 4. Scaling Features:
Normalize features so they all have mean = 0 and standard deviation = 1 using `StandardScaler`.


## Training process:
For the training I used `RandomForestClassifier`, along with `GridSearchCV` to help automatically test different combinations of parameters:
| Parameter           | Values Tested        |
| ------------------- | -------------------- |
| `n_estimators`      | \[10, 100, 200, 500] |
| `max_depth`         | \[None, 5, 10]       |
| `min_samples_split` | \[2, 3, 4]           |


## Results:
- Final Accuracy: 0.82 (82%)

Example of predicted results:
| PassengerId | Survived |
|-------------|----------|
| 892         | 0        |
| 893         | 0        |
| 894         | 0        |
| 895         | 0        |
| 896         | 1        |
| ...         | ...      |
| 1305        | 0        |
| 1306        | 1        |
| 1307        | 0        |
| 1308        | 0        |
| 1309        | 0        |
