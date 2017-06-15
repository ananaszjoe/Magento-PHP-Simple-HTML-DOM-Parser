# Magento-PHP-Simple-HTML-DOM-Parser
A Magento 1.X extension made to host S.C. Chen's parser [(http://simplehtmldom.sourceforge.net/)](http://simplehtmldom.sourceforge.net/) in a Magento 1.X environment

## DISCLAIMER
This extension is entirely based on the HTML parser made by S.C Chen (me578022@gmail.com) which is available [here](http://simplehtmldom.sourceforge.net/) with its original documentation.

###### I won't actively support this and it is as it is. So if you find any issues or want to mix things up, that's up to you.
---

# Overview

### Installation
Copy the app folder into your Magento 1.X installation's root folder. Empty the cache, recompile.

### Basic usage:
**Note the difference** compared to Chen's original parser at `Mage::helper('htmldom')`
```php
<?php
    // Create DOM from string
    $html = Mage::helper('htmldom')->str_get_html('<div id="hello">Hello</div><div id="world">World</div>');

    $html->find('div', 1)->class = 'bar';

    $html->find('div[id=hello]', 0)->innertext = 'foo';

    echo $html; // Output: <div id="hello">foo</div><div id="world" class="bar">World</div>

?>
```

# The original documentation:

## Quick Start

**Get HTML elements**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Create DOM from URL or file
$html = file_get_html('http://www.google.com/');

// Find all images 
foreach($html->find('img') as $element) 
       echo $element->src . '<br>';

// Find all links 
foreach($html->find('a') as $element) 
		echo $element->href . '<br>';
```

**Modify HTML elements**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Create DOM from string
$html = str_get_html('<div id="hello">Hello</div><div id="world">World</div>');

$html->find('div', 1)->class = 'bar';

$html->find('div[id=hello]', 0)->innertext = 'foo';

echo $html; // Output: <div id="hello">foo</div><div id="world" class="bar">World</div>
```

**Extract contents from HTML**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php

// Dump contents (without tags) from HTML
echo file_get_html('http://www.google.com/')->plaintext; 
```

**Srcaping Slashdot!**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Create DOM from URL
$html = file_get_html('http://slashdot.org/');

// Find all article blocks
foreach($html->find('div.article') as $article) {
    $item['title']     = $article->find('div.title', 0)->plaintext;
    $item['intro']    = $article->find('div.intro', 0)->plaintext;
    $item['details'] = $article->find('div.details', 0)->plaintext;
    $articles[] = $item;
}

print_r($articles);
```

## How to create HTML DOM object?

**Quick way**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Create a DOM object from a string
$html = str_get_html('<html><body>Hello!</body></html>');

// Create a DOM object from a URL
$html = file_get_html('http://www.google.com/');

// Create a DOM object from a HTML file
$html = file_get_html('test.htm');
```

**Object-oriented way**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Create a DOM object
$html = new simple_html_dom();

// Load HTML from a string
$html->load('<html><body>Hello!</body></html>');

// Load HTML from a URL 
$html->load_file('http://www.google.com/');

// Load HTML from a HTML file 
$html->load_file('test.htm');
```


## How to find HTML elements?

**Basics**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Find all anchors, returns a array of element objects
$ret = $html->find('a');

// Find (N)th anchor, returns element object or null if not found (zero based)
$ret = $html->find('a', 0);

// Find lastest anchor, returns element object or null if not found (zero based)
$ret = $html->find('a', -1); 

// Find all <div> with the id attribute
$ret = $html->find('div[id]');

// Find all <div> which attribute id=foo
$ret = $html->find('div[id=foo]'); 
```

**Advanced**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Find all element which id=foo
$ret = $html->find('#foo');

// Find all element which class=foo
$ret = $html->find('.foo');

// Find all element has attribute id
$ret = $html->find('*[id]'); 

// Find all anchors and images 
$ret = $html->find('a, img'); 

// Find all anchors and images with the "title" attribute
$ret = $html->find('a[title], img[title]');
```

**Descendant selectors**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Find all <li> in <ul> 
$es = $html->find('ul li');

// Find Nested <div> tags
$es = $html->find('div div div'); 

// Find all <td> in <table> which class=hello 
$es = $html->find('table.hello td');

// Find all td tags with attribite align=center in table tags 
$es = $html->find(''table td[align=center]');
```

**Nested selectors**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Find all <li> in <ul> 
foreach($html->find('ul') as $ul) 
{
       foreach($ul->find('li') as $li) 
       {
             // do something...
       }
}

// Find first <li> in first <ul> 
$e = $html->find('ul', 0)->find('li', 0);
```

**Attribute filters**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

Supports these operators in attribute selectors:

| filter 				| Description 																			|
| ------------- 		| ------------------------------------------------------------------------------------- |
| [attribute]			| Matches elements that **have** the specified attribute. 									|
| [!attribute] 			| Matches elements that **don't have** the specified attribute. 							|
| [attribute=value]		| Matches elements that have the specified attribute with a **certain value**. 				|
| [attribute!=value] 	| Matches elements that **don't have** the specified attribute with a certain value. 		|
| [attribute^=value] 	| Matches elements that have the specified attribute and it **starts** with a certain value.|
| [attribute$=value] 	| Matches elements that have the specified attribute and it **ends** with a certain value. 	|
| [attribute*=value] 	| Matches elements that have the specified attribute and it **contains** a certain value. 	|


**Text & Comments**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Find all text blocks 
$es = $html->find('text');

// Find all comment (<!--...-->) blocks 
$es = $html->find('comment');
```


## How to access the HTML element's attributes?

**Get, Set and Remove attributes**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Get a attribute ( If the attribute is non-value attribute (eg. checked, selected...), it will returns true or false)
$value = $e->href;

// Set a attribute(If the attribute is non-value attribute (eg. checked, selected...), set it's value as true or false)
$e->href = 'my link';

// Remove a attribute, set it's value as null! 
$e->href = null;

// Determine whether a attribute exist? 
if(isset($e->href)) 
        echo 'href exist!';
```

**Magic attributes**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Example
$html = str_get_html("<div>foo <b>bar</b></div>"); 
$e = $html->find("div", 0);

echo $e->tag; // Returns: " div"
echo $e->outertext; // Returns: " <div>foo <b>bar</b></div>"
echo $e->innertext; // Returns: " foo <b>bar</b>"
echo $e->plaintext; // Returns: " foo bar"
```

| Attribute Name		| Usage														|
| --------------------- | ------------------------------------------------- 		|
| $e->**tag**				| Read or write the **tag name** of element. 			|
| $e->**outertext**	 		| Read or write the **outer HTML text** of element. 	|
| $e->**innertext**	 		| Read or write the **inner HTML text** of element. 	|
| $e->**plaintext** 		| Read or write the **plain text** of element. 			|

**Tips**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Extract contents from HTML 
echo $html->plaintext;

// Wrap a element
$e->outertext = '<div class="wrap">' . $e->outertext . '<div>';

// Remove a element, set it's outertext as an empty string 
$e->outertext = '';

// Append a element
$e->outertext = $e->outertext . '<div>foo<div>';

// Insert a element
$e->outertext = '<div>foo<div>' . $e->outertext;
```


## How to traverse the DOM tree?

**Background knowledge**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// If you are not so familiar with HTML DOM, check this link to learn more... 

// Example
echo $html->find("#div1", 0)->children(1)->children(1)->children(2)->id;
// or 
echo $html->getElementById("div1")->childNodes(1)->childNodes(1)->childNodes(2)->getAttribute('id');
```

**Traverse the DOM tree**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

You can also call methods with [**Camel naming convertions**](http://simplehtmldom.sourceforge.net/manual_api.htm#camel).

| method 								| Description																								|
| ------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| mixed $e->**children** ( [int $index] ) 	| Returns the Nth **child object** if **index** is set, otherwise return an **array of children**. 		|
| element $e->**parent** () 				| Returns the **parent** of element. 																	|
| element $e->**first_child** () 			| Returns the **first child** of element, or **null** if not found. 									|
| element $e->**last_child** () 			| Returns the **last child** of element, or **null** if not found. 										|
| element $e->**next_sibling** () 			| Returns the **next sibling** of element, or **null** if not found. 									|
| element $e->**prev_sibling** () 			| Returns the **previous sibling** of element, or **null** if not found. 								|



## How to dump contents of DOM object?

**Quik way**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Dumps the internal DOM tree back into string 
$str = $html;

// Print it!
echo $html; 
```

**Object-oriented way**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Dumps the internal DOM tree back into string 
$str = $html->save();

// Dumps the internal DOM tree back into a file 
$html->save('result.htm');
```


## How to customize the parsing behavior?

**Callback function**

**Remember** to call the methods on the Magento helper object: `Mage::helper('htmldom')` e.g.: `Mage::helper('htmldom')->file_get_html('foo.bar')`!

```php
// Write a function with parameter "$element"
function my_callback($element) {
        // Hide all <b> tags 
        if ($element->tag=='b')
                $element->outertext = '';
} 

// Register the callback function with it's function name
$html->set_callback('my_callback');

// Callback function will be invoked while dumping
echo $html;
```
