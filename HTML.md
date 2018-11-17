# HTML Questions


Yangshun - 23 questions

1. What does a doctype do?
Stands for document type (duh)


It is a declaration, preamble, very first part of an html document
It tells browser what type of document type to expect (HTML5, HTML4.0x), and also
how to translate code

It is a legacy effect from days when main browsers were netscape and internet explorer

Similar to a title in an article, giving reader a set of expectations

#### Provides browser with set of expectations on how to interpret code

ex: 

#### HTML5 uses <!doctype html>
#### HTML4 uses <!DOCTYPE HTML PUBLIC “-//W3C//DTD HTML 4.01//EN” “http://www.w3.org/TR/html4/strict.dtd”> 


if browser recognizes doctype declaration, it will trigger no-quirks mode, with proper method to read document

if browser doesn't recognize, it uses quirks mode, i.e a mode for reading documents without a doctype. As expected, many quirks in quirks mode and site does not render how one expects.

https://medium.freecodecamp.org/web-developer-interview-q-a-what-does-a-doctype-do-146dd757d7d1


2. How do you serve a page with content in multiple languages?


3. What kind of things must you be wary of when design or developing for multilingual sites?


4. What are data- attributes good for?


5. Consider HTML5 as an open web platform. What are the building blocks of HTML5?


6. Describe the difference between a cookie, sessionStorage and localStorage.

7. Describe the difference between <script></script>, <script async></script> and <script defer></script>.



8. Why is it generally a good idea to position CSS <link>s between <head></head> and JS <script></script>s just before <body></body>? Do you know any exceptions?



9. What is progressive rendering?



10. Why you would use a srcset attribute in an image tag? Explain the process the browser uses when evaluating the content of this attribute.


11. Have you used different HTML templating languages before?

templating languages/engine

What are HTML templating languages?

#### A type of language that allows combining of data with own syntax/template/variables to produce HTML

Hello {{name}} => in rendering Hello bob, or Hello Karen

	- . Allows write out template/format. 
	- Add data to fill out format, like a form.
	- Then produce HTML with the template.


examples: pug (jade => pug), handlebars/mustache, php


https://www.quora.com/What-is-the-use-of-template-engine-in-nodeJS



Markup vs MarkDown Languages

html is a markup language, used to format sites
.md files are markdown, actually a type of markup language


Stylesheet Languages

CSS is a stylesheet language, used to affect presentation of a language


