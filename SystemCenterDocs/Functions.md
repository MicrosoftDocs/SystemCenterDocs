---
title: Functions
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4552c484-d0c0-49e4-b963-fe360ea3f20e
---
# Functions
By using [!INCLUDE[orchlong](./Token/orchlong_md.md)], you can manipulate string data from text files, Published Data, or other sources, and convert it into a usable form. You can also perform simple arithmetic operations, such as calculating sums and differences, and performing division and multiplication operations. For example, you can extract text from a text file by using a **Text File Management** activity, trim leading and trailing spaces from the text, and then retrieve specific parts of the text that you can pass to other activities as returned data items.

For a complete list of the functions that you can perform, see the following Functions table.

## Data Manipulation Functions
You can insert a data manipulation function into any box that lets you type text. Data manipulation functions must be enclosed in square brackets \('\[' and '\]'\). For example:

`[Upper('this will be inserted in upper case')]`

When the activity runs, the text 'this will be inserted in uppercase' in the example is replaced with 'THIS WILL BE INSERTED IN UPPERCASE'.

## Nested Functions
If you want to use a data manipulation function within another function, you do not have to enclose the nested function in square brackets. For example, to nest the Field function, type:

`[Field(Field('username=jsmith@abcompany.com','=',2),'@',1)]`

## Functions
Functions are case\-sensitive. For example, Upper\('Text'\) will be processed, but upper\('Text'\) will not.

|Function and Definition|Usage|Parameters|Example|
|---------------------------|---------|--------------|-----------|
|Upper \- converts text to uppercase.|Upper\('Text'\)|Text \- the text that is being converted to uppercase.|Upper\('this will be converted to uppercase'\) returns 'THIS WILL BE CONVERTED TO UPPERCASE'|
|Lower \- converts text to lowercase.|Lower\('Text'\)|Text \- the text that is being converted to lowercase.|Lower\('This Will Be Converted To Lowercase'\) returns 'this will be converted to lowercase'|
|Field \- returns text in a specific position.|Field\('Text', 'Delimiter', Field Number\)|Text \- the text that is being searched.<br /><br />Delimiter \- the character that separates each field.<br /><br />Field Number \- the position of the field that is being returned \(starting at 1\).|Field\('John;Smith;9055552211', ';', 2\) returns 'Smith'|
|Sum \- returns the sum of a set of numbers.|Sum\(firstNumber, secondNumber, thirdNumber, ...\)|Number \- the number that is being added. You can put any set of numbers, each separated by a comma \(,\).|Sum\(2,3,4,5\) returns '14'|
|Diff \- returns the difference of two numbers.|Diff\(Number1, Number2, <Precision>\)|Number1 \- the number that will be subtracted from.<br /><br />Number2 \- the number that will be subtracted from Number1.<br /><br />Precision <Optional> \- the number of decimal places that the result will be rounded to.|Diff\(9, 7\) returns '2'<br /><br />Diff\(9.3, 2.1, 2\) returns '7.20'|
|Mult \- returns the product of a set of numbers.|Mult\(firstNumber, secondNumber, thirdNumber, ...\)|Number \- the number being multiplied. You can put any set of numbers, each separated by a comma \(,\).|Mult\(2, 3, 4\) returns '24'|
|Div \- returns the quotient of two numbers.|Div\(Number1, Number2, <Precision>\)|Number1 \- the number that will be divided.<br /><br />Number2 \- the number that will divide Number1.<br /><br />Precision <Optional> \- the number of decimal places that the result will be rounded to.|Div\(8, 4\) returns '2'<br /><br />Div\(9, 2, 2\) returns '4.50'|
|Instr \- returns the position of first occurrence of text within another text.|Instr \('SearchText', 'TextToFind'\)|SearchText \- the text that is being searched.<br /><br />TextToFind \- the text that you are searching for.|Instr\('This is a string that is searched', 'string'\) returns 11|
|Right \- returns a subset of the text from the right side of the full text.|Right\('Text', Length\)|Text \- the full text.<br /><br />Length \- the number of characters from the right side that will be returned.|Right\('Take from the right', 9\) returns 'the right'|
|Left \- returns a subset of the text from the left side of the full text.|Left\('Text', Length\)|Text \- the full text.<br /><br />Length \- the number of characters from the left side that will be returned.|Left\('Take from the left', 4\) returns 'Take'|
|Mid \- returns a subset of the text from the middle of the full text.|Mid\('Text', Start, Length\)|Text \- the full text.<br /><br />Start \- the starting position in the text where you want to begin returning characters.<br /><br />Length \- the number of characters starting from the Start position that will be returned.|Mid\('Take from the middle', 5, 4\) returns 'from'|
|LTrim \- trims leading spaces from text.|LTrim\('Text'\)|Text \- the text that is being trimmed of leading spaces.|LTrim\(' Remove the leading spaces only. '\) returns 'Remove the leading spaces only. '|
|RTrim \- trims the trailing spaces from text.|RTrim\('Text'\)|Text \- the text that is being trimmed of trailing spaces.|RTrim\(' Remove the trailing spaces only. '\) returns ' Remove the trailing spaces only.'|
|Trim \- trims leading and trailing spaces from text.|Trim\('Text'\)|Text \- the text that is being trimmed.|Trim\(' Remove leading and trailing spaces. '\) returns 'Remove leading and trailing spaces.'|
|Len \- returns the length of text.|Len\('Text'\)|Text \- the text that is being measured.|Len\('Measure this text'\) returns 17|

## See Also
[Data Manipulation](./Data-Manipulation.md)


