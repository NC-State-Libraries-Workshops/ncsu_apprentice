---
layout: page
title: Pages and Page Layouts

order: 70
duration: 20
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
make it available to you. For instance if you wanted to add an **example**,
you can just create a `example.md` file in the top level of your workshop
project. For this tutorial, we have provided a file called `example.md.back`
for you to use, just change the name to `example.md`. After a few moments go
to `your_base_url/example` in a web browser you should see the page.

You can add this page to your navigation bar by adding some lines to `data/tabs.yml`
as shown below.

```yaml

- path: example
  title: Example
```

If you wish to add the link somewhere in your text just use the path where
you would insert the URL in a link. For instance 

{% raw %}
```html

# path is the path for your page. Don't use the word 'path'
<a href={{ site.base_url }}/path></a>

```
{% endraw %}


## Custom Layouts

Layouts are essentially a mix of HTML and 
[Liquid](https://shopify.dev/docs/themes/liquid/reference) that handle
repetitive aspects of your website, and also help give it a consistent look 
and feel. Liquid is a simple programming language created by shopify, visit their pages
for mor information. Layouts,also 
can call other layouts. This page for instance has the *page* layout specified in the 
front matter.

```yml
    ---
    layout: page  # Layout specified here
    title: Layouts and Themes
    
    order: 7
    ...
```

This directs Jeklyll to look in `_layouts/page.html` to know how to display 
the content on this page. If you open this page up in a web browser, you'll see
that it has front matter too, and specifies a *default* as a layout, which 
can be found at `_layouts/default.html`. Jekll sees this and applies the 
*default* layout, then the *page* layout. 

If you want to change something on your page, you typically will change it in 
a layout as we did above. If we edit `_layouts/page.html` like below...

```html
    ---
    layout: default  # notice this layout calls another layout
    ---
    <article class="post">
    
    <!-- Add this line -->
    <P> Look at me, I'm a cowboy! Howdy, howdy howd!!</P>
    
    <h1>{{ site.title }}</h1>
```


Everthing that uses the *page* layout will have this line on it. In a nutshell,
that is how you can change the layouts to your needs.

You can create your own layouts too. The easiest way to learn how to do that is to 
user existing layouts and the 
[shopify liquid documentation](https://shopify.dev/docs/themes/liquid/reference) to 
create your own layout.




