django-matrix-field
===================

A Django app providing database and form fields for matrices (arrays of arrays).

Examples
--------

Database Field
~~~~~~~~~~~~~~

.. code:: python

    from django.db import models
    from matrix_field import MatrixField

    class MyModel(models.Model):
        matrix1 = MatrixField(datatype='float', dimensions=(3, 2))
        matrix2 = MatrixField(datatype='str', dimensions=(2,))

    my_inst = MyModel(
        matrix1=[[5.1, -1.2], [4.2, 0.0], [3.14, 2.71]],
        matrix2=['a list', 'of strings'],
    )
    my_inst.full_clean()  # validates datatype, dimensions
    my_inst.save()        # values stored in DB as json

    m1 = my_inst.matrix1  # values retrieved as matrices
    repr(m1)              # '[[5.1, -1.2], [4.2, 0.0], [3.14, 2.71]]'


Form Field
~~~~~~~~~~

.. code:: python

    import json
    from django import forms
    from matrix_field import MatrixFormField

    class MyForm(forms.Form):
        matrix = MatrixFormField(datatype='int', dimensions=(2, 1))

    my_form = MyForm({
        'matrix': json.dumps([[2], [1]]),  # assignment of json representation
    })
    my_form.full_clean()                   # validates datatype, dimensions

    m = my_form.cleaned_data['matrix']  # values retrieved as matrices
    repr(m)                             # '[[2], [1]]'


Found a Bug?
------------

To file a bug or submit a patch, please head over to `django-matrix-field on github`__.


__ https://github.com/Sharmaxz/django-matrix-field
