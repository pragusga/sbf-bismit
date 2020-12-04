# Forms in Django 🤠

## Outline
* Regular forms vs Django forms
* How-tos (**forms.Form**)
  * Set up models.py
  * Create form class
  * Implement the views
  * Templating
    * form as p, as table, and as li
    * for loop nguli
* Introducing: **forms.ModelForm**
  * Set up new models.py
  * Create form class
  * Implement the views
  * Templating

Regular forms vs Django forms
---

Let's have a look on an example of a regular forms: **Multiple Choices using Checkboxes!**

1. Expected Results:


2. HTML Code:
    <br/> di template (`forms.html`):
    ```
    <input type="checkbox" id="vehicle1" name="vehicle1" value="Bike">
    <label for="vehicle1"> I have a bike</label><br>
    <input type="checkbox" id="vehicle2" name="vehicle2" value="Car">
    <label for="vehicle2"> I have a car</label><br>
    <input type="checkbox" id="vehicle3" name="vehicle3" value="Boat">
    <label for="vehicle3"> I have a boat</label><br>
    ```
    Imagine having 10++ choices on the form. Meaning that you'd have to re-do the input & label for each choices 🤮

4. Django Forms:
    <br/> di `forms.py`
    ```
    from django import forms
    from django.forms.widgets import CheckboxSelectMultiple

    BIRTH_YEAR_CHOICES = ['1980', '1981', '1982']
    FAVORITE_COLORS_CHOICES = [
        ('blue', 'Blue'),
        ('green', 'Green'),
        ('black', 'Black'),
    ]

    class SimpleForm(forms.Form):
        favorite_colors = forms.MultipleChoiceField(
            required=False,
            widget=forms.CheckboxSelectMultiple,
            choices=FAVORITE_COLORS_CHOICES,
        )
    ```

    <br/> di template (`forms.html`):
    ```
    <!DOCTYPE html>

    ...

    {{ form.as_p }}
    ```

How-tos (**forms.Form API**)
---
This section will explain on how you could utilize Django forms API to build a simple **facebook-like timeline status form**.

1. Set-up `models.py`
    <br/> Say we're making a form that asks username and status. So, we need to build a models class that stores those attributes.

    ```
3. Implement the `views.py`
    ezpz

    ```
    ```

4. Templating (say our template file is `statusfeedpage.html`
    haha

    ```
    ```

Introducing: **forms.ModelForm API**
---