# Regular Expression Tutorial

This tutorial is meant to be a foundational reference guide for anyone learning regular expressions.
We'll be referencing one specific regex throughout this tutorial that can be used to search for an email address such as "bob@gmail.com" and return a match if the structure of that email matches the criteria specified in the regex. We'll break down each component of our email regex and learning about the functionality of each part.
By the end of this tutorial you will know what a regular expression is, when to use them and how to utilize each component.

Bonus: You can click <span><a href="https://regexr.com/" target="_blank">here</a></span> to navigate to an online regex editor so you can practice your regex scripting as you learn!

## Summary

A regular expression or "regex" is a statement that describes a specific pattern of characters that can be searched for in a file or directory, matched and then returned to be utilized by a user or program to serve various use cases. The goal of each regex is to return a match for a continuous series of characters. The type of characters, number characters and order of characters can all be specified and modified inside the regex statement. 

## Table of Contents

- [Regular Expression Tutorial](#regular-expression-tutorial)
  - [Summary](#summary)
  - [Table of Contents](#table-of-contents)
  - [Regex for an email address](#regex-for-an-email-address)
  - [Regex Components](#regex-components)
    - [Anchors](#anchors)
    - [Quantifiers](#quantifiers)
    - [Character Classes](#character-classes)
    - [Grouping and Capturing](#grouping-and-capturing)
  - [About the Author](#about-the-author)

## Regex for an email address
```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

- Structure of an email address: <br>
  > The structure of a basic email address is split up into 3 main parts: the "user-name" and "domain-name" separated by an `@` "At sign", then a `.` "dot" followed by the "domain-extension". The final address structure will look like this: `(user-name)@(domain-name).(domain-extension)` We'll reference these 3 parts throughout this tutorial.


## Regex Components

### Anchors

- Description: <br>
  > Anchors are used for matching a character or phrase at the beginning and end of a line. RegEx recognizes the end of a line as a series of characters that is terminated by a return. The `^` "carrot" character is used to reference the start of a line and the `$` "dollar-sign" character is used to reference the end of a line.
 
- Use in our email address regex:
  > Our email address regex utilizes both the `^` "start-of-line" anchor and the `$` "end-of-line" anchor. These anchors appear at the start and end of our expression like this: `/^(regex)$/` This means that if a string is to be matched by our regex, it must be located at both the start and the end of a line. In other words, any email address that's matched by our regex must be on it's own line.

- Example:
  > Given the phrase below, let's say we want to use the `^` and `$` anchors to match a character of any kind at the beginning and end of the line. In our regex, we'll use the `.` period character to match any character at the start or end of the line.

  Phrase: 
  ```
  "I wanted to eat, so I ate a cheeseburger at McDonald's"
  ```

  <br>

  - Demo: Using the `^` "start-of-line" anchor

    Regex: 
    
    ``` 
    /^./
    ```

    Match: <br>
    > ![Start (single line)](https://user-images.githubusercontent.com/87861603/143735449-e50525b3-b05b-430d-968d-60ace53dd30b.png)
    
    Explanation: <br>
    > The regex `/^./` is basically saying, "Find an instance of `.` any character located at the `^` beginning of a line." The "I" is matched since it's a character and it's located at the beginning of a line.

  <br>

  - Demo: Using the `$` "end-of-line" anchor

    Regex: 
    
    ``` 
    /.$/
    ```

    Match: <br>
    > ![end (single line)](https://user-images.githubusercontent.com/87861603/143735469-2f10f7f3-f31f-4de0-a210-18cb8ec87213.png)
    
    Explanation: <br>
    > The regex `/.$/` is basically saying, "Find an instance of `.` any character located at the `$` end of a line." The "s" is matched since it's a character and it's located at the end of a line.

<br>

### Quantifiers

- Description: <br>
  > Quantifiers are used to return a match for a specific number of a characters. Using quantifiers, we can be very specific in how many instances a certain character should exist in a given criteria, or we can be very broad. Either way, quantifiers are very important in finding the characters or phrase we're searching for.

- All regex quantifiers:

  ```
    *     -> 0 or More
    +     -> 1 or More
    ?     -> 0 or One
    {x}   -> Exact Number
    {x,y} -> Min and Max range of numbers
  ```

- Use of quantifiers in our email address regex:

  > Our email address regex utilizes the `+` "1 or more" and `{x,y}` "min-max range" quantifiers. 
  These quantifiers are utilized in our regex in the user-name, domain-name and domain-extension parts. 
  In the user-name part, we see `[a-z0-9_\.-]+`. The `+` "plus sign" character at the end of the character class signifies the regex will match any character in the character class if it appears 1 or more times.
  In the domain-name part, we see `[\da-z\.-]+`. Here we see the `+` "plus sign" used in the same way as in the user-name part which means the regex will match any character in the character class if it appears 1 or more times.
  In the domain-extension part, we see `[a-z\.]{2,6}`. The `{2,6}` "min-max range" signifies the regex will match any character in the character class if it appears between 2-6 times. 
  If an email address is to be matched by this regex, it must satisfy all 3 of these criteria, else the whole email address will not be matched.
  
- Example:
  > Let's take a closer look at how quantifiers work but using all the different quantifier characters to return specific matches from the phrase below.

  Phrase:
  ```
  I am very veryy veryyy veryyyy hungry
  ```

  <br>

  - Demo #1) Using the `*` "0 or more" quantifier: <br>
    
    Regex: 
    
    ``` 
    /very */
    ```

    Match: <br>
    ![*](https://user-images.githubusercontent.com/87861603/144788009-0d86371b-b88e-4274-9b8d-314ae096892b.png)
    
    Explanation: <br>
    > The regex `/very */` is basically saying, "Find all instances of 'very' that are followed by 0 or more " " space characters."

  <br>

  - Demo #2) Using the `+` "1 or more" quantifier: <br>

    Regex: 
    
    ``` 
    /very +/
    ```

    Match: <br>
    ![+](https://user-images.githubusercontent.com/87861603/144787988-2ab92b5d-cbcb-42b3-ace6-1812f70aa4f5.png)
    
    Explanation: <br>
    > The regex `/very +/` is basically saying, "Find all instances of 'very' that are followed by one or more " " space characters."

  <br>

  - Demo #3) Using the `?` "0 or one" quantifier: <br>

    Regex: 
    
    ``` 
    /very?/
    ```

    Match: <br>
    ![?](https://user-images.githubusercontent.com/87861603/144788034-500446ad-a2d5-4ca8-bcc9-03bf2901eec4.png)
    
    Explanation: <br>
    > The regex `/very?/` is basically saying, "Find all instances of 'ver' that are followed by 0 or 1 "y" characters."

  <br>

  - Demo #4) Using the `{x}` "Exact Number" quantifier: <br>

    Regex: 
    
    ``` 
    /very{3}/
    ```

    Match: <br>
    ![{3}](https://user-images.githubusercontent.com/87861603/144788073-a1ee954f-2a81-4391-92b7-4924d4a46ddd.png)
    
    Explanation: <br>
    > The regex `/very{3}/` is basically saying, "Find all instances of 'ver' that are followed by exactly 3 "y" characters."

  <br>

  - Demo #5) Using the `{x,y}` "Min-Max range" quantifier: <br>

    Regex: 
    
    ``` 
    /very{2,4}/
    ```
    
    Match: <br>
    ![{2,4}](https://user-images.githubusercontent.com/87861603/144788880-71e7960a-e8c0-4539-8b24-088681149f7e.png)

    
    Explanation: <br>
    > The regex `/very{2,4}/` is basically saying, "Find all instances of 'ver' that are followed by 2-4 "y" characters."

<br>

### Character Classes

- Description <br>
  > Character classes are used to find matches of a specific character set and are invoked with the `[]` brackets. You can also join multiple character sets together by simply adding the next set immediately after the previous set.

- Use in our email address regex:
  > Our email address regex utilizes character classes in the user-name, domain-name and domain-extension parts. 
  In the user-name part, we see `[a-z0-9_\.-]`. This is saying the character in the user-name position of the email address must be either a `a-z` lowercase letter, a `0-9` numeric character from 0-9, an `_` underscore, a `\.` period or a `-` dash.
  In the domain-name part, we see `[\da-z\.-]`. This is saying the character in the domain-name position of the email address must be either a `\d` digit, a `a-z` lowercase letter, a `\.` period or a `-` dash.
  In the domain-extension part, we see `[a-z\.]`. This is saying the character in the user-name position of the email address must be either a `a-z` lowercase letter or a `\.` period,

- Example:
  > Given the list of user data below, let's say we only wanted to match and return the phone numbers of each user. We could write a regex to do this for us. All of the users have input their phone numbers in different formats and including different symbols, but we can utilize the `[]` character classes to include different sets of characters in our search and match all of the phone numbers. 

  Data:

  ```
  Sally Johnson:
  Email: sally.johnson@gmail.com
  Phone: 1231231234

  Robert Tyler:
  Email: bobT@aol.com
  Phone: 234-234-2345

  Carter Gonzales
  Email: c-gonzales8765@verizon.net
  Phone: (345)-345-3456

  Sue Parker
  Email: sue.p@sbcglobal.net
  Phone: 1-(456)-456-4567
  ```

  Regex:
  ```
  /(1-)?([0-9()]{3,5})-?([0-9]{3})-?([0-9]{4})/
  ```
  Match: <br>
  ![User data](https://user-images.githubusercontent.com/87861603/144983188-e673d433-2f34-4927-b8e4-fcf91a45ea97.png)  

  Explanation:
  > Here, we utilized the `[]` character classes in all 3 parts of the phone number format. 
  For the area code, we have `[0-9()]` which will return a match for any number from 0-9 and also any `()` parentheses characters.
  For the middle part, we have `[0-9]` which will return a match for any number from 0-9.
  And finally for the last 4 digits, we have `[0-9]` which will once again return a match for any number from 0-9.
  Together with quantifiers and grouping, the character classes we used has made it possible for us to match all the phone numbers in our user data despite their varying format.

<br>

### Grouping and Capturing

- Description: <br>
  > Capture groups are used to separate a series of regex criteria so they can be defined and saved in memory as their own group. These capture groups are defined with the `()` parentheses. Once defined and saved, these groups can be referenced in a find or replace operation or for backreferencing.

- Use in our email address regex: <br>
  > Our email address regex utilizes capture groups in the user-name, domain-name and domain-extension parts.
  In the user-name part, we see `([a-z0-9_\.-]+)`. This is saying that this capture group must have `+` one or more characters that could be a `a-z` lowercase letter, a `0-9` numeric character from 0-9, an `_` underscore, a `\.` period or a `-` dash. 
  In the domain-name part, we see `([\da-z\.-]+)`. This is saying that this capture group must have `+` one or more characters that could be a `\d` digit, a `a-z` lowercase letter, a `\.` period or a `-` dash.
  In the domain-extension part, we see `([a-z\.]{2,6})`. This is saying that this capture group must have `{2,6}` 2-6 characters that could be a `a-z` lowercase letter or a `\.` period

- Example:
  > Let's say we've created an application that gives us the current weather and a 24 hour forecast for the city we select. Since we're not a weather service, we're using an api that gives us our desired information when we request it. Occasionally there's an error that occurs when our application attempts to connect with the api. It gives us a message like the one below with a lot of different information about the error all grouped together into one long string. We can use a regular expression that matches that error message and separates the different bits of information into groups so we can quickly and easily extract the information we want.

  Error message:

  ```
  2021-11-06; 04:01.890; ERROR: The resource you requested was not found; USER: R+H/L)%%R7^V6IN68'2&//1;XB4T'_;
  ```

  Regex:

  ```
  /^(\d{4}-\d{2}-\d{2}); (\d{2}:\d{2}.\d{3}); (ERROR: .+); (USER: [A-Z\d\+/)%^'&;_]+);$/
  ```

  Explanation:
  > With this regex, all the different bits of information in this error message are now organized into capture groups.

  ```
    Group 0 (Entire message)  -> 2021-11-06; 04:01.890; ERROR: The resource you requested was not found; USER: R+H/L)%%R7^V6IN68'2&//1;XB4T'_;
    Group 1 (Date)            -> 2021-11-06
    Group 2 (Time)            -> 04:01.890
    Group 3 (Error message)   -> ERROR: The resource you requested was not found
    Group 4 (User ID)         -> USER: R+H/L)%%R7^V6IN68'2&//1;XB4T'_
  ```

  > Now that we have all the information separated, we can write a function that returns only the groups of information we want. We do this by referencing the group with the `$` dollar sign followed by the group number. For instance, if we wanted to only display the the Date and Error message, we can write a function that references those groups as `$1` and `$3`.

<br>

## About the Author

My name is Liz and I look forward to always learning in full stack! 
- [Liz Washington's GitHub](https://github.com/lizwashington)

