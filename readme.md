# Instructions to run this project

Please make sure you have pip and pipenv installed first. 

```sh
git clone https://github.com/hhss16/Lab3
cd Lab3
pipenv shell
pipenv install 
python manage.py makemigrations 
python manage.py migrate
python manage.py runserver
```

Extra `djangorestframework-xml` was installed using `pipenv`

## Previews & Information

Then access `http://127.0.0.1:8000/api/menu-items` or `http://127.0.0.1:8000/api/menu-items/1` - full support for **GET** and **POST** for *menu items* and full support for **GET**, **PUT**, **PATCH** and **DELETE** for *single menu item*. 

![Preview Lab 3](https://res.cloudinary.com/dpebhamdp/image/upload/v1667824082/Labs/Lab3/lab3-input_kubpjx.png)

It has full validation support done in the `serializers.py` - check that extra_kwargs section. Price cannot be less than 2 and inventory cannot be negative.

```python
class MenuItemSerializer(serializers.ModelSerializer):
    class Meta:
        model = MenuItem
        fields = ['id','title','price','inventory']
        extra_kwargs = {
            'price': {'min_value': 2},
            'inventory':{'min_value':0}
        }
```

![validation](https://res.cloudinary.com/dpebhamdp/image/upload/v1667824082/Labs/Lab3/lab3-validation_cea6ni.png)

JSON XMLRenderer is added in the settings.py file  

```python
REST_FRAMEWORK = {
    'DEFAULT_RENDERER_CLASSES': [
        'rest_framework.renderers.JSONRenderer',
        'rest_framework.renderers.BrowsableAPIRenderer',
        'rest_framework_xml.renderers.XMLRenderer',
    ]
}
```

And you can access `http://127.0.0.1:8000/api/menu-items?format=xml` and `http://127.0.0.1:8000/api/menu-items?format=json`

![JSON](https://res.cloudinary.com/dpebhamdp/image/upload/v1667824081/Labs/Lab3/lab3-json_mg8mhf.png)

![XML](https://res.cloudinary.com/dpebhamdp/image/upload/v1667824082/Labs/Lab3/lab3-xml_oqab97.png)

