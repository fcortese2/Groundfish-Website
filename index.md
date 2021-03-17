# Welcome to DBTools
## Made by Filippo Cortese

DBTools is a unity plugin which enables runtime virtual database creation in Unity. Writing, reading and interacting with the virtual database.

### Visual Setup

Once you have imported the package into your Unity project, firstly you can add all of the objects (only Serializable Objects) to the *INCLUDED OBJECTS* section of the inspector int the *DBTools -- Settings* object found in the hierarchy view.

![Adding objects before runtime](https://fcortese2.github.io/Groundfish-Website/AddObjectsUI.PNG)


After adding the items, you must specify which fields will be included in the virtual database. You can do so by clicking the *+* button under the *DATABASE FIELDS* section of the same inspector. If the field name has been entered correctly, a tick will appear next to the entry. If it has not been entered correctly, an error message and a cross will appear, as well as play mode exiting as soon as you try to enter play mode in-engine. Please remember to specify the datatype of the field correctly.

The only available datatypes are currently `string`, `int`, `float` and `bool`.


![Specifying fields](https://fcortese2.github.io/Groundfish-Website/FieldsSelection.PNG)

Should you need to add further fields to the database which cannot be converted to a basic type such as `int`, `float`, `bool` and `string`, navigate to the scene object called *DBTools -- Reflector*. In this object's inspector window, proceed to select one of the following types from the drop-down menu : `Texture2D`, `Sprite` or `GameObject`. Currently these are the only unity-specific types which can be stored in the virtual database, but more will be added at a later stage. You may then drag into the appropriate slots each object's value.

*For ease of use, you may also select through which field you would like to see each of the entries labeled as by selecting a different option from the drop-down menu labeled 'Reference to display:'.*

![Pre-connection Reflector](https://fcortese2.github.io/Groundfish-Website/ReflectorConnection.PNG)

_Pre-connection reflector settings_

![Post-connection Reflector](https://fcortese2.github.io/Groundfish-Website/ReflectorPostConnection.PNG)

_Post-connection reflector settigns_



### Custom script interaction with DBTools

Because of the nature of the plugin, it is necessary for the user to be able to access data from the virtual database through custom scripts.

**IMPORTANT NOTE:** *When accessing external DBTools functionalities, please **ONLY** reference the script `DBTools_Link` attached to the automatically generated scene object called "DBTools - Runtime". The methods designed to be interacted with externally are all publicly accessible through the instance of the `DBTools_Link` script.*




```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/fcortese2/Groundfish-Website/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
