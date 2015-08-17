i18next-ko
==========
With this awkwardly named library, you can easily translate your
[KnockoutJS](ko) applications. It uses [i18next](i18n), so you may want to read
[their documentation](i18ndoc) to know how to use variables and stuff.

Usage
=====

Initialization
--------------
To initialize i18next-ko, you need to call `i18nextko.init()`. It takes the
following parameters: `i18nextko.init(resourceStore, language, ko)`.

* The `resourceStore` is a i18next resource store. It looks like this:
```
  {
    en:
      translations: {
        'testTranslation': 'Test translation'
      }
    },

    de: {
      translations: {
        'testTranslation': 'Test-Übersetzung'
      }
    }
  }
```

* The `language` is the language that will be used by default.
  Defaults to `'en'`.
* You may set `ko` to your KnockoutJS object. Usually, this is not needed but
  it may solve some issues if you use Browserify and have some dependencies that
  require different versions of KnockoutJS.
  Defaults to `window.ko`.

Note that the i18nextko object basically is a singleton. Once you initialized
it, the translations and the `i18n` binding will be available everywhere.

Using translations
------------------
i18next-ko comes with exactly one new KnockoutJS binding: The `i18n` binding.

You can use the binding in three different ways:

1. Use a string:
   `data-bind="i18n: 'testTranslation'"` sets the content of the
   element to the translation with the key `testTranslation`.

   It is automatically updated whenever the language is changed.

2. Use a key and add variables:
   `data-bind="i18n: { key: 'greeting', options: { name: name } }"`
   sets the content of the element to the translation with the given key.

   The variable `__name__` in the translation is replaced with the value of the
   `name` property of the view model.

   It is automatically updated whenever the language is changed or the value of
   any observable variable is changed.

3. Mix both approaches and bind multiple attributes:
   `data-bind="i18n: { 'html': 'testTranslation', 'title': { key: 'greeting',
   options: { name: name } } }"` sets the content of the element to the
   translation with the key `testTranslation`.

   The `title` attribute to the translation with the key `greeting`, using the
   `name` property of the view model for the variable `__name__`.

   You can use as many attributes as you want. Translations are automatically
   updated whenever the language is changed or the value of any observable
   variable is changed.

Changing the language
---------------------
The language can be changed with `i18nextko.setLanguage('your-language')`. This
will update every translation, as documented above.