---
title: Regular Expressions
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e179b9b5-89aa-4ed0-b1fe-0edf8475ecc0
author: cfreemanwa
ms.author: cfreeman
ms.date: 2016-10-12
manager: cfreeman
---
# Regular Expressions

> Apples To: System Center 2016 - Orchestrator

In System Center 2016 - Orchestrator, regular expressions let you match a string to a pattern. The regular expression can contain a number of different elements that define the pattern. [Smart Link Properties](http://technet.microsoft.com/en-us/library/hh403779.aspx) use regular expressions to perform pattern matching.  

## Advanced Regular Expressions  
To build regular expressions, you must create an expression that contains the text that you are searching for and special characters that create a pattern, which describes how the text that you are searching for appears.  

|Character|Meaning|  
|-------------|-----------|  
|.|Matches any character except a newline.|  
|\*|Matches the preceding item 0 or more times. For example, the "a\*" pattern matches any string of a's in a row "a", "aaa", "aaaaaaaaaaaa", and an empty string "". To match any string of any character, use a dot followed by an asterisk. For example "a.\*" matches any text that begins with the letter "a" and ends with any string of characters such as "abbb", "abcdef", or "automatic restart".|  
|\+|Matches the preceding item 1 or more times. This is like \* but you must have a least 1 of the preceding item to make a match. For example, the "ab\+" pattern matches "abbbbb", "ab", but does not match "a". To contrast, the "ab\*" pattern matches "a".|  
|?|Matches the preceding item 0 or 1 time. For example, the "ab?" pattern matches "a" or "ab" but does not match "abbb".|  
|&#124;|Matches either the preceding expression or the following expression. Logical OR operator.|  
|$|Matches the expression at the end of the input or line. For example, "ab$" matches "I took a cab" or "drab" but does not match "absolutely not".|  
|^|Matches the expression at the beginning of the input or line. For example, "^ab" matches "absolutely not" or "abacuses are great\!" but does not match "I took a cab" or "drab".|  
|\\|For characters that are usually treated as special. This indicates that the next character is literal and is not to be treated as a special character. For example, "\\." means match the "." character and not just any character.|  
|\[ \]|A character set. Matches any one of the enclosed characters. You can specify a range of characters by using a hyphen. For example, \[a\-zA\-Z\] matches any letter of the alphabet.|  
|\[^ \]|An excluded character set. This is the opposite of \[\]. If any of the characters inside the brackets exist, the regular expression match fails. You can specify a range of characters by using a hyphen. For example, \[^a\-zA\-Z\] ensures that none of the letters in the alphabet are present.|  
|\( \)|A group expression. This groups an expression into an item that you can apply special characters to. For example, "a\*\(ba\)\+" matches "ba" "aba" or "ababa" but does not match "abbba" or "abaa"|  

### Examples  

|Expression|Meaning|  
|--------------|-----------|  
|\[a\-zA\-Z\]\+|The text contains only letters of the alphabet.|  
|^\\\*|The text begins with an asterisk.|  
|\(abc&#124;def\)$|The end of the text is either "abc" or "def".|  
|Ha..y|The text begins with "Ha" followed by any two characters followed by a "y".|  
|Help.\*|The text is "Help" followed by any number of other characters.|  

## See Also  
[Data Manipulation](../manage/data-manipulation.md)  
