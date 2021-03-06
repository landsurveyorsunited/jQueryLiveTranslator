#jQueryLiveTranslator

jQueryLiveTranslator is a jQuery plugin to translate a static web site easily.

1.   It first loads asynchronously the translation files you supply to the plugin. It can be a string or an array of them.

1.   Then, if no options are specified, it translates the element based on the user's browser language. The plugin is also able to translate using a lang variable you supply, see demo for more information!

1.   Finally, if you supply a callback, it will be executed over every element to be translated.

Demo is in package.

## Usage & Documentation

Just include the plugin files in your file. 

### Use the "data-translate" attribute on DOM elements you want to be translated

```html
    <h1 data-translate="hello"> Hello! </h1>
    <img data-translate="img" alt="This is an image!" src="someimage.jpg" />
```

The "hello" and "img" words serve as sort of key so it's easier to locate the translation.

### Create a JSON language file with the translations:

- You can specify folder to hold translation files, by default, plugin look for files in "lang" folder

index-es.json:

```javascript
    {
      "hello": "Hola!"
      "img" : "Esto es una imagen!"
    }
```
    
### Call the plugin!

    $("[data-translate]").jqLTranslate('index');
    
## In-depth explanation and Documentation

The first argument the plugin receives, is the package that it has to load. You may have different packs for different parts of the website (header, dialogs, etc);

You can load more than one package like this:

```javascript
    $("[data-translate]").jqLTranslate(['index', 'header', 'footer']);
```

If the language of the user's browser is "es", the plugin will try to load:

* index-es.json
* header-es.json
* footer-es.json

If the language also has a country code, like "es-MX", the plugin will ALSO try to load the following:

* index-es-MX.json
* header-es-MX.json
* footer-es-MX.json

This can provide you more customization for different regions. Unfortunately, most of current browsers (desktop) only have the language portion though mobile ones use to have both.

### Options

An object containing parameters. Please, note that all parameters are optional.

> **asyncLangLoad** (*boolean*): Whether if the language should be loaded asynchronously or syncrhonously. **Default**: *true* (*asynchronously*)

> **cache** (*boolean*): Whether if the language packages should be cached or not. **Default**: *true*

> **defaultLang** (*string*): The default language of the Application, this language won't be loaded. **Default**: *null*

> **fallbackLang** (*string*): String that sets a fallback language to load in case it can't load the user language. **Default**: *null*

> **forceLang** (*string*): String that forces the language for the script, forgetting the user's language. **Default**: *null*

> **path** (*string*): This is the default path of the translation files. Useful if you want to locate your files in a separated folder. **Default**: *null*

> **onComplete** (*function*): Callback function triggered when a DOM element has been translated. *this* will point to the element.**Default**: *null*

> **skip**	(*array of strings*):  An array containing all the languages you want to avoid the translation. **Default**: *empty array*

### Advanced

Here are some advanced tricks you can use and some extra info.

First, let's see how the plugin reacts to the elements:

>  **input** : It first checks if it's a **placeholder** and, if it is, it translates it. If it doesn't it will change the input value to one supplied. 

>  **optgroup** : Get their **label** attribute translated

>  **img** : Get their **alt** attribute translated

>  *default* : Get their HTML replaced.

#### Changing multiple attributes for each element

If the key for a given value contains nested values, it will try change them all. Please, have in mind that **you** are responsible of supplying the correct attributes. For example:

index-es.json:

```javascript
    {
      "hello": "Hola!"
      "img" : {
      	"text" : "Esto es una imagen!",
      	"src" : "linktootherimage.jpg"
      }
    }
```

The *text* attribute will replace the normal behaviour and will follow the aforementioned rules to translate the element. The remaining attributes will be directly changed on the element.

## FAQ

### How can I translate my jQuery Mobile application?

#### Using jQuery Mobile 1.1 and further

```javascript
$(document).on('pagecreate','#home',function(event){
  $("[data-translate]").jqLTranslate('index', { asyncLangLoad: false });
});
```

## Credits & Licensing

Dual licensed under the GPL (http://dev.jquery.com/browser/trunk/jquery/GPL-LICENSE.txt) and MIT (http://dev.jquery.com/browser/trunk/jquery/MIT-LICENSE.txt) licenses.

Written by Ilyas Bakouch (@vladimire)

Based on Antonio Laguna's jqueryTranslator jQuery plugin.
https://github.com/Belelros/jqueryTranslator
