---
layout: page
title: Layouts and Themes

order: 7
duration: 320
tutorial: true
instructors_notes: true

description: |
  You can change layouts, add pages or change the style of your  workshop
  relatively easy with just a little knowledge of CSS and HTML.
  
instructors_note: |

---

This unit may be a bit advanced. You may want to just read it over, to get 
some background information if you don't have plans to really change the look
and feel of your workshops. Jekyll and the Apprentice framework are fairly 
adaptable to your needs. If you have some knowledge of HTML and CSS, or are 
willing to learn, there are few limits as to what you can do.

## Adding Pages

If you add a file to the top level directly, Jekyll will automatically 
make it available to you. For instance if you wanted to add a bibliography,
you can just create a `bibliography.md` file in the top level of your workshop
project. For this tutorial, we have provided a file called `bibliography.md.back`
for you to use, just change the name to `bibliography.md`. After a few moments
(or you may need to restart your server) if you got to `your_base_url/bibliography`
in a web browser you should see the page is available.

## Custom Layouts

Layouts are useful templates that contain all the repetitive content in the 
web pages, and also format and display the specific content on each page. Layouts,
also can call other layouts. This page for instance has the *page* layout 
specified in the front matter.

```yml
    ---
    layout: page
    title: Layouts and Themes
    
    order: 7
    ...
```

This directs Jeklyll to look in `_layouts/page.html` to know how to display 
the content on this page. If you open this page up in a web browser, you'll see
that it has front matter too, and specifies a *default* layout. There is also
a lot of HTML and some stuff in curly braces, such as {% raw %}`{{ content }}` 
 or `{% assign sorted_pages = site.units | where: "tutorial", true | sort:"order" %}`
{% endraw %}. We'll touch briefly on the curly braces in a bit. Going back to 
the *default* layout, that means we need to look in `_layouts/default.html` as 
well. Jekll sees this and applies the *default* layout, then the *page* layout. 

If you want to change something on your page, you typically will change that here.
You could for instance add something like below to `_layouts/page`.

```html

    ---
    layout: default
    ---
    <article class="post">
    
    <!-- Add this line -->
    <P> Look at me, I'm a cowboy! Howdy, howdy howdy!!</P>
    
```

Now it will have this line on everthing that uses the *page* layout.

The curly braces are part of the [Liquid Programming Language](https://help.shopify.com/en/themes/liquid).
You can also find more on the [Jekyll Web Pages](https://jekyllrb.com/docs/home/).
Liquid is a fairly simple programming language that Jekyll uses to
allow you to automate tasks and work with information in your various files.

A full liquid tutorial is beyond our scope here, so very briefly there are two
kinds of curly braces. {% raw %} The double curlies `{{ content }}` echo back
content. If for instance you put in `{{ site.title }]` {% endraw %} right after your last line

```html
    ---
    layout: default
    ---
    <article class="post">
    
    <!-- Add this line -->
    <P> Look at me, I'm a cowboy! Howdy, howdy howd!!</P>
    
    <h1>{{ site.title }}</h1>
```

Your workshop title will be displayed there on every page that uses the page 
layout. 

The curly/percents {% raw %} `{% assign var = 42 %}` {% endraw %} are used for 
doing operations, such as if/then statement, assigning variables or looping 
over data strctures.



## Custom Styles

