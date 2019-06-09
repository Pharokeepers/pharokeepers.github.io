---
layout: post
author: smi
date: 2019-09-06 10:00:00 +0200
categories: pharo
title: Comparing Ordered Dictionaries
comments: true
---

During second week of [GSoC 2019](<https://summerofcode.withgoogle.com/>) coding period on [Pharo](<http://pharo.org/>) project, I was learning more about existing implementations of Ordered dictionaries, comparing them and polishing [Containers-OrderPreservingDictionary](<https://github.com/Ducasse/Containers-OrderPreservingDictionary>) a little bit.

I couldn't help but notice all the similarities between Collections - OrderedDictionary and Containers-OrderPreservingDictionary. They both start from the same place, inheriting from Collections. The diagram below shows inheritance relationships:

![](/images/dictionaries.png)



All of these classes: OrderedDictionary, CTStandardOrderedDictionary and CTOrderPreservingDictionary had dictionaries that are keeping their key-value pairs in some sort of an order. I wanted to know what are the differences between these orders. Let's see:

+ OrderedDictionary

```smalltalk
| orderedDict |
orderedDict := OrderedDictionary   new. 
orderedDict at: 1 put: 'first'.
orderedDict at: 2 put: 'second'.
orderedDict at: 1 put: 'another first'.
orderedDict  >>> 'an OrderedDictionary(1->''another first'' 2->''second'')'
```

+ CTSTandardOrderedDictionary

```smalltalk
| standardOrederedDict |
standardOrederedDict := CTStandardOrderedDictionary  new. 
standardOrederedDict  at: 1 put: 'first'.
standardOrederedDict  at: 2 put: 'second'.
standardOrederedDict  at: 1 put: 'another first'.
standardOrederedDict  >>> 'a CTStandardOrderedDictionary(1->''another first'' 2->''second'')'
```

+ CTOrderPreservingDictionary

```smalltalk
| orderPreservingDict |
orderPreservingDict  := CTOrderPreservingDictionary new. 
orderPreservingDict at: 1 put: 'first'.
orderPreservingDict at: 2 put: 'second'.
orderPreservingDict  at: 1 put: 'another first'.
orderPreservingDict  >>> 'a CTOrderPreservingDictionary(1->''another first'' 2->''second'')'
```



**The order is preserved in all three classes in the same way.** 



If the order is same, what could be the other differences between all these classes from the diagram?

I decided to compare these pairs:

1. OrderedDictionary vs CTStandardOrderedDictionary
2. CTStandardOrderedDictionary vs CTOrderPreservingDictionary
3. OrderedIdentityDictionary vs CTStandardOrderedIdentityDictionary
4. CTOrderPreservingIdentityDictionary vs CTStandardOrderedIdentityDictionary
5. CTOrderPreservingDictionary vs CTOrderPreservingStringDictionary



### 1.  OrderedDictionary vs CTStandardOrderedDictionary

Both of these classes are subclass of Collections. Majority of their methods are *completely the same*. There are some differences though:

+ OrderedDictionary has methods that CTSODictionary doesn't like:

  + asValueHolder:
  + at:at:
  + at:at:ifAbsent:
  + at:at:put:
  + at:ifPresent:ifAbsentPut:
  + atRandom:
  + bindingOf;
  + bindingsDo:
  + declareFrom:
  + gtInspectorItemsIn:
  + hasBindingThatBeginsWith:
  + isHealthy
  + removeUnreferencedKeys
  + stonOn:
  + storeOn:
  + unreferencedKeys

  and on the class side:

  + inspectorClass
  + newFromKeysandValues:


+ CTStandardOrderedDictionary has methods that aren't in OrderedDictionary:

  + speciesNewFrom:
  + orderedKeysIdentityIndexOf:
  + copyEmpty:
  + errorValueNotFound:
  + isEmpty
  + isIdentityDictionary
  + isOrderPreservingDictionary
  + orderedKeysIdentityIndexOf: 

  All these methods are written keeping in mind portability to Squeak and GS

+ There are methods which has the same name and the same functionality only `ifAbsent`: was favored in CTSODictionary instead of `ifPresent:` again for portability purposes for Squeak and GS: 

```smalltalk
OrderedDictionary >> associationAt: aKey ifPresent: aBlock
	^ dictionary associationAt: aKey ifPresent: aBlock
```

```smalltalk
CTStandardOrderedDictionary >> associationAt: aKey ifPresent: aBlock
	"Squeak and GS do not have #associationAt:ifPresent: so it
	is reimplemented for portability"
	^ aBlock cull:
		(dictionary
			associationAt: aKey
			ifAbsent: [^ nil])
```

+ all the core functionalities like adding, removing and similar are completely the same.
+ both raise a `KeyNotFound` error when absent keys/values are accessed. 



### 2. CTStandardOrderedDictionary vs CTOrderPreservingDictionary 

We saw that the order is preserved in the same manner in both of these classes. 

**The difference:** By default, when CTStandardOrderedDictionary raises an exception and CTOrderPreservingDictionary returns a configurable default value (nil by default) instead of raising an exception. 

+ CTStandardOrderedDictionary

```
| dict |
dict := CTStandardOrderedDictionary new. 
dict at: #missing
>>> 'KeyNotFound'
```

+ CTOrderPreservingDictionary

```
| dict |
dict := CTOrderPreservingDictionary new. 
dict defaultValue: 666.
dict at: #missing
>>> 666
```

**In conclusion** several methods in CTOrderPreservingDictionary are overriden so that they return a default value. 

(OrderedDictionary like CTStandardOrderedDictionary raises an error)

### 3. OrderedIdentityDictionary vs CTStandardOrderedIdentityDictionary

All identity dictionaries have the feature of using == instead of = for key comparing.

+ CTStandardOrderedIdentityDictionary has one extra method that OrderedIdentityDictionary doesn't have:

```
isIdentityDictionary
	^ true
```

+ All other methods are completely the same

### 4. CTOrderPreservingIdentityDictionary vs CTStandardOrderedIdentityDictionary

+ all the methods are completely the same. The only difference is what `self` refers to which means CTOrderPreservingID has default values and CStandardOrderedID raises erros.

### 5. CTOrderPreservingDictionary vs CTOrderPreservingStringDictionary

What I expected from CTOrderPreserving**String**Dictionary based on its name was that they key values could only be Strings. That didn't make much sense and when I checked it didn't behave like that:

```smalltalk
| strDict |
 strDict  := CTOrderPreservingStringDictionary new. 
 strDict at: 1 put: 10.
 strDict at: 2 put: 20.
 strDict  >>> 'a CTOrderPreservingStringDictionary(1->10 2->20)'
```

So you can use other data types besides Strings for both keys and values. Then why *String* in the name of the class?

+ default values is set to ` ' ' `(empty string)

```smalltalk
CTOrderPreservingDictionary >> at: aKey
	^ self
		at: aKey
		ifAbsent: [defaultValue]
```

```smalltalk
at: aKey
	^ self
		at: aKey
		ifAbsent: ['']
```

+ CTOrderPresevingDicitonary has a few instance methods that CTOrderPreservingStringDict doesn't: 

  + copyEmpty:

  + defaultValue:

+ different class methods in CTOrderPresevingDicitonary :

  + defaultValue:
  + newWithDefaultValue:
  + newFrom:
  

  
## Conclusion:

  There are a lot of code repetitions in these classes and subclass behavior differences are not that big. One of the solutions that is being discussed with mentors is merging some classes and using strategy.



