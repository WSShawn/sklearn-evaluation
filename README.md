#sklearn-evaluation

[![Build Status](https://travis-ci.org/edublancas/sklearn-evaluation.svg?branch=master)](https://travis-ci.org/edublancas/sklearn-evaluation) [![Documentation Status](https://readthedocs.org/projects/sklearn-evaluation/badge/?version=latest)](http://sklearn-evaluation.readthedocs.io/en/latest/?badge=latest)

The cool kids way to evaluate scikit-learn models. [Documentation](http://sklearn-evaluation.rtfd.io)

# Install  

```bash
pip install sklearn-evaluation
```

Works with Python 2. Support for Python 3 soon!

# Dependencies

The package only depends on scikit-learn and matplotlib to work. But if you want to use the reports module you need to install `mistune` and `tabulate` for the tables module

```bash
pip install mistune
pip install tabulate
```

#Usage

The package is divided in modules that have specific functionality.

##Plots module

Generate evaluation plots with a single function call.
```python
from sklearn_evaluation import plots

#code for data loading and model training

plots.confusion_matrix(y_true, y_pred, target_names=target_names)
```

![confusion matrix](examples/cm.png)

##Tables module

Generate good looking tables from your model results.

```python
from sklearn_evaluation import tables

#code for data loading and training

tables.feature_importances(model, feature_list)
```

```
+-----------+--------------+-----------+
| name      |   importance |       std |
+===========+==============+===========+
| Feature 0 |    0.250398  | 0.0530907 |
+-----------+--------------+-----------+
| Feature 1 |    0.232397  | 0.0523836 |
+-----------+--------------+-----------+
| Feature 2 |    0.148898  | 0.0331814 |
+-----------+--------------+-----------+
| Feature 3 |    0.0553634 | 0.0128296 |
+-----------+--------------+-----------+
| Feature 8 |    0.05401   | 0.0122248 |
+-----------+--------------+-----------+
| Feature 5 |    0.053878  | 0.01289   |
+-----------+--------------+-----------+
| Feature 6 |    0.0525828 | 0.0130225 |
+-----------+--------------+-----------+
| Feature 9 |    0.0510197 | 0.0129436 |
+-----------+--------------+-----------+
| Feature 7 |    0.0509633 | 0.0117197 |
+-----------+--------------+-----------+
| Feature 4 |    0.0504887 | 0.012844  |
+-----------+--------------+-----------+
```

Also, running this in Jupyter will generate a pandas-like output.

##Using the OOP interface

A simplified API is available by packing the results of your estimator in the `ClassifierEvaluator` class.

```python
from sklearn_evaluation import ClassifierEvaluator

# code for data loading and model training

ce = ClassifierEvaluator(classifier, y_test, y_pred, y_score,
                         feature_list, target_names)

# this plots the confusion matrix
ce.confusion_matrix
```

## Generating reports

Generate reports using Markdown templates.

```python
 
 template = '''
            # Report
            {estimator_type}
            {date}
            {confusion_matrix}
            {roc}
            {precision_recall}
            '''

ce.generate_report(template, path='report.html')
```


The code above will generate a report [like this one.](http://htmlpreview.github.com/?https://github.com/edublancas/sklearn-model-evaluation/blob/master/examples/report.html)

Reports are self-contained, all images are included in the html file using [base64](https://en.wikipedia.org/wiki/Base64).
