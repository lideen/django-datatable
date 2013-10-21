# Django-table

_____________________________________________________________________

![preview](http://redmine.funshion.com/redmine/attachments/download/54280/django-table.png)
_____________________________________________________________________

## Overview

Django-table is a simple Django app to origanize data in tabular form.
It is based on [datatable](http://datatables.net).

## Quick start
<br>
1. Setup Django-table application in Python environment:<br>

    $ python setup.py install
2. Add "table" to your INSTALLED_APPS setting like this:<br>

    INSTALLED_APPS = (
        ...,
        'table',
    )
3. Define a simple model named Person:<br>

    # example/app/models.py
    class Person(models.Model):
        name = models.CharField(max_length=100)
4. Add some data so you have something to display in the table.
Now define a PersonTable class without any options in table file.<br>

    # example/app/tables.py
    from models import Person
    from table import Table, Column
    
    class PersonTable(Table):
        id = Column(field='id')
        name = Column(field='name')

        class Meta:
            model = Person
            id = 'people'

And pass a table instance to the view.

    # example/app/views.py
    from django.shortcuts import render
    from app.tables import PersonTable

    def people(request):
        people = PersonTable()
        return render(request, "index.html", {'people': people})
5. Finally, implement the template:<br>

    {# example/templates/index.html}
    {% load static %}
    {% load table %}

    <link href="{% static 'css/bootstrap.min.css' %}" rel="stylesheet" media="screen">
    <script src="{% static 'js/jquery.min.js' %}"></script>
    <script src="{% static 'js/bootstrap.min.js' %}"></script>

    <!DOCTYPE html>
    <html>
        <head>
            <meta http-equiv="content-type" content="text/html; charset=utf-8" />
            <title>person</title>
        </head>
        <body>
            <div class="container" style="margin-top: 10px">
                <h1>people</h1>
                <br />
                {% render_table people %}
            </div>
        </body>
    </html>

## Reference

### Table
#### DataSource
* Model
* Dict-List
* Json
#### Options
* model
* id
* attrs
* sort
### Column
* Build-in Column
  * Text Column
  * Checkbox Column

* Custom Column

  If you want full control over the way the table is rendered, ignore the built-in Columns,
and instead pass an instance of your Table subclass into your own template.
