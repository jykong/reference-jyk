## Scikit-Learn Reference
Machine Learning library for Python

### Preprocessing
#### Standardization / Scaling Values
`StandardScaler` subtracts the mean and divides by the variance

    from sklearn.preprocessing import StandardScaler

    scaled_X = StandardScaler.fit_transform(X)

`MinMaxScaler` scales the values to the range `[0,1]`

    from sklearn.preprocessing import MinMaxScaler

    scaled_X = MinMaxScaler.fit_transform(X)

`MaxAbsScaler` scales the values to the range `[-1,1]`

    from sklearn.preprocessing import MaxAbsScaler

    scaled_X = MaxAbsScaler.fit_transform(X)

#### Binarization
`Binarizer` accepts a threshold and binarizes accordingly

    from sklearn.preprocessing import Binarizer

    binary_X = Binarizer.fit_transform(X)

#### Categorical Encoding
Scikit-learn models do not handle integer value encodings for categorical values as features well. For example, feature variable `weather` may have values `['sunny', 'rainy', 'cloudy']` represented as `[0, 1, 2]`. In order to fit models to this data, scikit-learn prefers that this variable be split into 3 one-hot features `'sunny'`, `'rainy'`, and `'cloudy'` each represented as binary values `[0, 1]`.

One-hot encoding can be done in Pandas using the method `get_dummies()`. Sci-kit learn provides `OneHotEncoder`.

### Feature Selection
Automated feature selection

    from sklearn.feature_selection import SelectKBest

    from sklearn.feature_selection import f_classif
    scoring_func = f_classif    # f_classif calculates ANOVA F-value
    n_top_features = 10
    selector = SelectKBest(scoring_func, k=n_top_features)

    selector.fit(titanic[predictors], titanic["Survived"])

    scores = -np.log10(selector.pvalues_)

### Clustering
#### K-means Clustering
Centroid clustering

    from sklearn.cluster import KMeans
    kmeans_model = KMeans(n_clusters=2, random_state=1)
    distances = kmeans_model.fit_transform(X_train)
    centroids = kmeans_model.cluster_centers
    cluster_assignments = kmeans_model.labels_    # from X_train
    cluster_assignments = kmeans_model.predict(X_test)

### Regression
#### Linear Regression
Use for continuous independent variable -> continuous dependent variable

    from sklearn.linear_model import LinearRegression

    reg = LinearRegression()
    reg.fit(x_train, y_train)
    pred_y_test = reg.predict(x_test)

**NOTE:** `x_train`, `y_train` and `x_test` must be 1 column matrices. i.e. calling `.shape` returns (n_rows, 1)

TODO: respond to this [stackexchange post](http://stackoverflow.com/questions/29934083/linear-regression-on-pandas-dataframe-using-sci-kit-learn)

#### Logistic Regression
Use for continuous independent variable -> binary classification

    from sklearn.linear_model import LogisticRegression

    reg = LinearRegression()
    reg.fit(x_train, binary_labels_train)
    pred_binary_labels = reg.predict(x_test)

Return predicted probabilities instead of labels

    pred_label_probabilities = reg.predict_proba(x_test)

Use `pred_label_probabilities[:,0]` for probability of 0 and `pred_label_probabilities[:,1]` for probability of 1.

Default predicted probability threshold for classification is 0.5

#### K-Nearest Neighbors
    from sklearn.neighbors import KNeighborsRegressor
    knn = KNeighborsRegressor(n_neighbors=5)
    knn.fit(X_train, y_train)
    pred = knn.predict(X_test)

### Classification
#### Decision Trees
    from sklearn.tree import DecisionTreeClassifier
    clf = DecisionTreeClassifier(random_state=1)
    clf.fit(X,y)

#### Support Vector Machines
    from sklearn.svm  import SVC
    clf = SVC(random_state=1)
    clf.fit(X,y)

[SVM Guide](http://scikit-learn.org/stable/modules/svm.html)

### Ensemble Classification
#### Random Forests
    from sklearn.ensemble import RandomForestClassifier

    RandomForestClassifier(random_state=1, n_estimators=10)

#### Gradient Boosting
    from sklearn.ensemble import GradientBoostingClassifier

    GradientBoostingClassifier(random_state=1, n_estimators=25)

### Textual Analytics
#### Count Vectorization
Turns list of terms into frequency counts with each term as a column variable

    from sklearn.feature_extraction.text import CountVectorizer

    vectorizer = CountVectorizer(stop_words='english')
    features = vectorizer.fit_transform(some_list_of_words)

[Text Feature Extraction Guide](http://scikit-learn.org/stable/modules/feature_extraction.html#text-feature-extraction)

#### Naive Bayes
    from sklearn.naive_bayes import MultinomialNB

    nb = MultinomialNB()
    nb.fit(train_features, train_target)
    pred = nb.predcit(test_features)

### Metrics
#### Receiver Operator Curve (ROC)
Use to evaluate classification thresholds

    from sklearn.metrics import roc_curve

    fpr, tpr, thresholds = roc_curve(test_labels, pred_prob_of_1)   # use predict_proba()[:,1]

#### ROC Area Under Curve Score
    from sklearn.metrics import roc_auc_score

    auc_score = roc_auc_score(test_labels, pred_prob)

#### Cross-Validation
Using `train_test_split`

    from sklearn.cross_validation import train_test_split

    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=1)

Using `KFold`

    from sklearn.cross_validation import KFold

    kf = KFold(n=n_rows, n_folds=3, random_state=1)

    predictions = []
    for train, test in kf:
        train_predictors = (data[predictors].iloc[train,:])
        train_target = titanic[target].iloc[train]
        model.fit(train_predictors, train_target)
        test_predictions = model.predict(data[predictors].iloc[test,:])
        predictions.append(test_predictions)

`cross_val_score` performs automatic model fitting score calculation

    from sklearn import cross_validation

    scores = cross_validation.cross_val_score(model, data[predictors], data[target], cv=10)
    scores_mean = scores.mean()
    scores_std = scores.std()

### Parameter Tuning
#### Grid Search
`GridSearchCV` iteratively performs fit & score on a specified model over all permutations of specified model parameters, passed in as dictionary of lists.

    from sklearn.grid_search import GridSearchCV

    c_values = [0.1, 0.3, 0.5, 0.7, 0.9, 1.0, 1.3, 1.5, 1.7, 2.0]
    kernel_values = ['linear', 'poly', 'rbf', 'sigmoid']
    param_grid = dict(C=c_values, kernel=kernel_values)
    model = SVC()
    kfold = cross_validation.KFold(n=num_instances, n_folds=num_folds, random_state=seed)

    grid = GridSearchCV(estimator=model, param_grid=param_grid, scoring=scoring, cv=kfold)
    grid_result = grid.fit(X, y)
    print("Best: %f using %s" % (grid_result.best_score_, grid_result.best_params_))
    for params, mean_score, scores in grid_result.grid_scores_:
        print("%f (%f) with: %r" % (scores.mean(), scores.std(), params))

### Pipelining
#### Pipelines
`Pipeline` used to specify a series of transformation steps to apply to the data before model fitting and a model to fit with. The pipeline can then be used as though it were a model.

    from sklearn.pipeline import Pipeline

    anova_filter = SelectKBest(f_regression, k=5)
    clf = svm.SVC(kernel='linear')

    pl = Pipeline([('anova', anova_filter), ('svc', clf)])
    pl.fit(X_train, y_train)
    pred = pl.predict(X_test)

    scores = cross_validation.cross_val_score(pl, X, y, cv=10)

#### Feature Union
`FeatureUnion` is used to specify a series of preprocessing and feature selection/extraction steps to perform on the data whose results are then concatenated. The `FeatureUnion` can then be used as transformation step in a `Pipeline`.

    from sklearn.pipeline import FeatureUnion

    feature_union = FeatureUnion([('pca', PCA(n_components=3)),('select_best', SelectKBest(k=6))]
    X_selected_features = feature_union.fit(X, y).transform(X)

    pl = Pipeline([('feature_selection', feature_union), ('classifier', clf)]))
