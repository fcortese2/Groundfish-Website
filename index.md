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

*For the sake of continuity, we will refer to a reference of the `DBTools_Link` script as `_link`*

**IMPORTANT NOTE:** *We highly suggest you have a unique variable indicator within your scriptable object and referenced within the database fields as previously mentioned. A possible basic implementation of this is as follows:*
```c#
[HideInInspector]public string uniqueID;

private void Awake()
    {
        uniqueID = GenerateRandomString();
    }

    private string GenerateRandomString()
    {
        const string possibleChar = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890";
        char[] charArray = new char[12];
        for (int i = 0; i < charArray.Length; i++)
        {
            charArray[i] = possibleChar[Random.Range(0, possibleChar.Length)];
        }
        return new string(charArray);
    }
```
**You will then need to specify which field represents a unique value for each object in the *Field representing unique entry ID:* section of the *DBTools - Runtime* object inspector. WHenever you come across the default string value `root` within fields, it is a direct reference to this unique ID of the object.**

#### Initiating the databse and database creation

DBTools has internal functionality which allows the user to set the plugin to automatically generate the database on load. Should the user prefer to call the creation of the database through custom code, it is possible as follows:

```c#
_link.GenerateDB();
```

#### Getting entry key ID (equivalent to entry row number in the database)
This returns int by default. Finds the first field with a specific value within a specific field.
Possible inputs are int, string, float and bool. Please ensure the field value is of the same datatype as the values in the field being scanned.

```c#
_link.GetKeyFromVal(value, fieldName); 
```

#### Getting field/column value from specific Key

```c#
string value = _link.GetStringFromPosition(wantedValueName, wantedKey);
int value = _link.GetIntFromPosition(wantedValueName, wantedKey);
float value =  _link.GetFloatFromPosition(wantedValueName, wantedKey);
bool value = _link.GetBoolFromPosition(wantedValueName, wantedKey);
```

#### Getting field value from another field's value
We suggest not using this functionality in majority of cases, unless the known value is a entry-unique value such as a `root` value.
 
*Please keep in mind that it will only scan for the first object with the specified value. For cases in which you are unsure wether the entry even exists in the specified field, you will need to implement your own try-catch logic.*

```c#
string returnValue = _link.GetStringFromValue(knownFieldName, knownValue, wantedValueFieldName);
```
*overloads:*
```c#
GetStringFromValue(string currentField, object fieldValue, string wantedField);
GetIntFromValue(string currentField, object fieldValue, string wantedField);
GetFloatFromValue(string currentField, object fieldValue, string wantedField);
GetBoolFromValue(string currentField, object fieldValue, string wantedField);
```

#### Getting Unity custom objects from field Value or Key
If you want to access the Texture2D/Sprite/GameObject at a specific unique field value, only pass the method's first parameter. Leave the `columnName` parameter as the default `root`.

```c#
Texture2D returnValue = _link.GetTexture2DReflection(uniqueValueAsCorrectType);
Sprite returnValue = _link.GetSpriteReflection(uniqueValueAsCorrectType);
GameObject returnValue = _link.GetGameObjectReflection(uniqueValueAsCorrectType);
```

If the known value is not in the unique-value field, pass the field name as second parameter.

```c#
Texture2D returnValue = _link.GetTexture2DReflection(uniqueValueAsCorrectType, valueFieldName);
Sprite returnValue = _link.GetSpriteReflection(uniqueValueAsCorrectType, valueFieldName);
GameObject returnValue = _link.GetGameObjectReflection(uniqueValueAsCorrectType, valueFieldName);
```

### Nested Requests
To maximize functionality, we suggest the use of nested requests.
For example, you can nest requests such as
```c#
_link.GetTexture2DReflection(_link.GetKeyFromVal("testValue", "testColumn"));
```


## Upcoming Features
The following releases will include:
- Adding Scriptable Objects to DB at runtime through custom scripts (HIGH IMPORTANCE)
- Removing Scriptable Objects from DB at runtime through custom scripts (HIGH IMPORTANCE)
- Custom generic object support in `DBTools -- Reflector` tools (MEDIUM IMPORTANCE)
- Adding DB access requests visual representation in table/custom window (MEDIUM IMPORTANCE)
- Adding DB request return time log option for optimization purposes(MEDIUM/LOW IMPORTANCE)  
