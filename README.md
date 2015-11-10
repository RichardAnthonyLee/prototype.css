![CSS Blocks]( http://cloud.quallsbenson.com/uploads/css-blocks.png )

Write fully semantic, dry, and scalable css with CSS Blocks. 

CSS blocks is a BEM based scss library that applies object oriented principles, like abstract classes, inheritance, and multiple inheritance to css development. It was designed to help css developers create component-based css that is less specific, more organized, and extremely reusable.

### Installation ###

Run the following command in the terminal (requires [bower](http://bower.io/) )

```cli

bower install css-blocks

```

Next, import the library into your scss file

```css

@import 'path/to/css-blocks';

```

### Usage ###

**First:** create an Abstract Block for your other blocks to inherit from:

Let's create a `thumbnail` module:


```css

%thumbnail{

	display: block;
	border: 1px solid blue;

	@include block; //here is where we define thumbnail as an abstract block

}

```

Next we'll create elements and modifiers for the thumbnail block:

The following code will create an element called `thumbnail__image`.

```css

%thumbnail__image{

	width: 100%;
	height: auto;
	
	@include block; //defines thumbnail__image as an element to the thumbnail abstract block

}

```

Create modifiers for the `thumbnail` and `thumbnail__image`

```css 

%thumbnail--big{

	@include block; //defines thumbnail--big as a modifier of the thumbnail abstract block

	/*.. attributes of thumbnail--big  ..*/

}

%thumbnail__image--top{

	@include block; //defines thumbnail__image--top as a modifier of the thumbnail__image

	/*.. attributes of thumbnail__image--top   */

}

```

**Second:** Extend that abstract block with a new module.

Let's create a `.video` module

```css 

@include extend-block( '.video-thumbnail', thumbnail ){

	/* overriding styles */

}

```

**Voila:** The Resulting CSS:

```css

.video-thumbnail{

	display: block;
	border: 1px solid blue;
	/*.. other attributes of the thumbnail ..*/
}

.video-thumbnail__image{

	/*... attributes of the thumbnail__image ..*/

}

.video-thumbnail--big{

	   /* attributes of thumbnail--big */

}

.video-thumbnail__image--top{

	   /*.. attributes of thumbnail__image--top   */

}

```

CSS Blocks allows for your modules to inherit all the attributes and properties of abstract blocks as base styles, which you can easily override. 

Create another thumbnail module called `news`:

```css

@include extend-block('.news-thumbnail', thumbnail){

	/* overriding styles */

}

```

Resulting CSS:

```css

.news-thumbnail, .video-thumbnail{

	/* ... */

}

.news-thumbnail__image, .video-thumbnail__image{

	/* ... */

}

```

This CSS is reusable, portable and reduces the need for specificity. For example: I can alter styles of the thumbnails in the news section like this:

```css

.news-thumbnail{

	/* styles */

}
```

Rather than this:

```css
.news-section .thumbnail{

	/* styles */

}
```	


There is no risk of css style clashes with other thumbnail modules; This is especially useful in cases where developers can only alter css, and not the actual html. 

### Multiple Selectors ###


Sometimes it may be desireable to extend an abstract block with multiple selectors rather than just one. This can be done in one of two ways:


**Method One (Separate wit commas)**

```css

@include extend-block( ".news-thumbnail, .video-thumbnail", thumbnail ){
	
	/*..styles..*/

}

```

**Method Two (Nested Selector)**

```css


.news-thumbnail, .video-thumbnail{
	
	/*..styles..*/

	@include extend-block( thumbnail );

}


The latter may be desireable as it looks more cssy than the first.


```

### Multiple Inheritance ###


With CSS blocks, your modules can also inherit the properties of multiple abstract blocks. Using the `thumbnail` example above: let's say we wanted to give the option of using the basic thumbnail abstract block and an extended version, that included more properties and modifiers. The basic version, that we created above, would have only the `thumbnail__image` property, but the extended version would have additional properties like `thumbnail__action` and `thumbnail__date`.

Let's create the scss:

```css

@include abs-block(thumbnail-extended){ //can be any name

	/* extended styles */

} 

@include abs-block-property(thumbnail-extended, action){

	/* attributes for action */

}

@include abs-block-property(thumbnail-extended, date){

	/* attributes for date */

}

```	

We don't want every module we create to inherit all the properties of the extended thumbnail, only a few, but without the pain of writing css attributes for each element/property we want to extend. Just extend both the `thumbnail` and the `thumbnail-extended` abstract blocks to inherit all their properties:


```scss

@include extend-block(`.news-thumbnail`, thumbnail);

@include extend-block(`.news-thumbnail`, thumbnail-extended);


```

You can mix and match module properties easily using multiple inheritance. 

### Class Naming Conventions ###

By default CSS Blocks uses BEM syntax, which uses double underscores to separate elements from blocks, and double hyphens to to separate modifiers from blocks and elements example:

.block__element--modifier{
	/* ..styles.. */
}

.block--modifier{
	/* ..styles.. */
}

To alter this, set the global variables $abstract-block-element-separator, and $abstract-block-modifier-separator to the desired values. For example, some frameworks use single hyphens for both modifiers and elements. Setting $abstract-block-element-separator, $abstract-block-modifier-separator to '-', will result in the following syntax.

.block-element{
	/* ..styles.. */
}

.block-element-modifier{
	/* ..styles.. */
}




### The CSS Blocks Way ###


Coding scss this way naturally makes css more portable, less specific, and more scalable/maintainable. The objective of CSS Blocks is to increase productivity, and preserve semantics. It is designed for projects that scale. 


**Benefits:**


* Use only the css you need, when you need it
* Reuse CSS without increasing specificity
* Create your own framework without imposing class-naming conventions
* Write Fully semantic css without losing productivity
* Add or remove styles from a css block without effecting other blocks
* Object Oriented organization of css.
* Alter all blocks or a single blocks without increasing css specificity. 
* Add a property to all blocks or a single block with a single line of code.
* Keep css specificity maintainable, Write less css


**Limits:**


* Since all abstract blocks create placeholders, nested abstract blocks tend to 
  create very very long selectors after compiled. 


### Bugs/Feature Requests ###

If you notice any bugs, or have a feature request; just create an issue, and we'll address them promptly. 	

### Contributors ###

 [Richard Lee](https://twitter.com/@Richard_A_Lee ) - Creator and Maintianer of CSS Blocks


### License (MIT) ###

Copyright (c) 2015 Quallsbenson

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.