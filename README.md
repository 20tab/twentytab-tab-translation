twentytab-tab-translation
=========================

A django app to apply jQuery UI tab view to translated modeltranslation fields. 

## Installation

Use the following command: <b><i>pip install twentytab-tab-translation</i></b>

## Configuration

- Static files

Run collectstatic command or map static directory. If you use uWSGI you can map static files:

```ini
static-map = /static/tab_translation/=%(path_to_site_packages)/tab_translation/static/tab_translation
```

## Usage
- translation.py

```py
from modeltranslation.translator import translator, TranslationOptions
from testapp.models import ModelTest


class MyTranslationOptions(TranslationOptions):
    fields = ('text',)


translator.register(ModelTest, MyTranslationOptions)


```

- admin.py

```py

from django.contrib import admin
from testapp.models import ModelTest
from tab_translation.admin import TransAdmin


class ModelTestAdmin(TransAdmin):
    ...

    fieldsets = (
        ('', {'fields': (
            ('...',),),
        }
        ),
        ('', {'fields': (
            ('text',),),
            'classes': ('trans-fieldset',)
        }
        ),
    )

    ...

admin.site.register(ModelTest, ModelTestAdmin)

```