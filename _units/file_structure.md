---
layout: page
title: File Structure

order: 10
duration: 5
tutorial: true
instructors_notes: true
description: |
  Understanding how the files are organized in apprentice helps a lot in using it.
  This unit covers the basic structure of apprentice, describing the function of\
  the most  important files and folders.

---


When you first look at a new apprentice project, the large numbers of files and 
directories can be intimidating. Actually, once you understand it, it makes it a lot 
easier to build workshops and tutorials. Here we will describe the most important and 
commonly edited files and directories. 

The first thing to understand is the use of the underscore *_*. In most cases, files 
that start with an underscore or files in directories that start with an underscore
are safe to edit. Other files can be edited, but it may require more care and 
understanding of what you are doing. 

Each of these will be covered in more detail later, so we'll just touch on them 
quickly here.

<dl>
  <dt>_config.yml and _config_dev.yml</dt>
  <dd>
    These go in the base directory and tell apprentice how to set up your application
  </dd>
  <dt>_data</dt>
  <dd>
    Files in this directory are written as YAML files. They are read when the 
    application starts and available anywhere using the syntax `{ site.data.file_name }`.
    The files provided should be adequate in most cases, so you only need to add the 
    data in each file as needed.
  </dd>
  <dt>_includes</dt>
  <dd>
    This directory provides additional formatting if needed. This will require some 
    knowledge of HTML to creator your own includes but using them is straighforward.
  </dd>
  <dt>_layouts</dt>
  <dd>
    This directory contains layouts for different kinds of pages in apprentice. Like
    `_includes` you likely won't use it much until you are more advanced.
  </dd>
  <dt>_sass</dt>
  <dd>
    This directory contains styling instructions for apprentice. It requires some 
    knowledge of CSS to use but its very safe to work with for the most part.
  </dd>
  <dt>_site</dt>
  <dd>
    This directory is actually automatically created by jekyll and you shouldn't have a 
    reason to edit it.
  </dd>
  <dt>_slides</dt>
  <dd>
    This directory is where you create slides for your workshop. Each file is a slide. 
    If you do not wish to have slides, just delete or empty the directory.
  </dd>
  <dt>_units</dt>
  <dd>
    This directory contains the files for an online tutorial. Each file is a webpage.
    If you don't want any units, just delete or empty the directory.
  </dd>
  
  The rest of the files and directories won't typically need to be edited, although
  you may want to someday. Before you do that, make sure you understand the file first,
  and if you wish submit and issue to see if the changes can be added to the apprentice
  project.
</dl>

