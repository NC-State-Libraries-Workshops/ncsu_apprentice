---
layout: page
title: Presentation Slides

order: 6
duration: 30
tutorial: true
instructors_notes: true

description: |
  Often a workshop will require some presentation slides. This describes
  how to create a slide deck.
  
instructors_note: |

---

The Apprentice framework also allows you to create HTML slide presentations
using the [Reveal.js framework](). **NOTE:** Because GitHub pages restricts
what plug-ins can be used, some of the Reveal functions don't work there, 
namely **fragments** and **background transitions**.

We won't get into the pros and cons of HTML presentations over something like
PowerPoint. They can both make great and awful presentations. The main 
reason for HTML slides is that they are on the web, so they get indexed by 
search engines, don't require proprietary software, and are often mobile 
friendly. HTML presentations do have a learning curve, but in Apprentice
its no different than creating a unit.

Like units, slides live in the `_slides` directory, and each slide gets its 
own file structued like below.

```markdown

    ---
    order: 2
    ---
    
    ## My Slide
    
    This is the content
    
    <h3><em>Some HTML</em></h3>

```

This should look familiar. The order defines the order of the slide in the 
slide deck and works the same as units. Likewise, the content can be Markdown,
HTML or both. 


