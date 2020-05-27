---
layout: page
title: Configuration

order: 20
duration: 10
tutorial: true
instructors_notes: true
description: |
  Change the configuration settings for your workshop.
instructors_note: |
  Emphasize that the server needs to be restarted with any change in 
  `_config.yml`.

---


Jekyll websites always use a `_config.yml` file to keep site wide settings such 
as **title** or **description**. The values set here are available from
from within your markdown or html using ` {{ site.setting_name }}`. You
will see and use this often as you work. You can also add your own
settings as needed.

The `_config.yml` is commented with more detailed instructions. To get started
we'll just change the most important ones. Make the changes below.

```yml

    title: <your workshop name>
    
    description: <describe your workshop>
    
    # Multiple authors go on the same line, just format how you like.
    # Same with companyies
    author:
      name: <your name(s)
      # url:  http://example.com/
      company:
          name: < your orgnization(s)
          # url:  http://example.com/
    
    # Any value is ok, Beginner|Intermediate|Advanced are recommended, required 
    level: Beginner
    
    # This needs to be set to your repository name, or it won't work on GitHub.
    # If you are deploying elsewhere it may not be necessary.
    # It is overridden if you are working locally when you start the server
    baseurl: "/repo_name"
```

If you are working locally restart your server to see the changes, which
should be evident on your workshop homepage. If you are working directly 
on GitHub pages, there server restarts automatically and may take a few minutes.

Some of the other settings will be dealt with in future units.


Apprentice also comes with a `config_dev.yml` file. This is useful if you are working
locally (on  your own computer) and want some different settings when you run your 
project locally vs in GitHub. The two most useful changes you can make are the `baseurl`
and `title`. GitHub needs to use your repo name for the baseurl, but your local 
environmoent probably does not. Using a different title is a good way to know you are 
looking at your local development version rather than the version that might be up 
on GitHub. This is especially useful when both applications are running in  your browser.

Below is the version that comes with Apprentice.

```yaml

    # This allows overriding the defult _config.yml file. Use 
    # jekyll serve --host $IP --port $PORT --baseurl '' --config _config.yml,_config_dev.yml to run this 
    # on a local server. Then GitHub will not use the _config.dev.yml file so the settings
    # there will take over. SEe https://github.com/jekyll/jekyll/issues/958 .
    
    supporting_files_path: "supporting_files/"
    
    # Where the bibliography data is comment out or set to blank to disable.
    title: NCSU Apprentice (DEV)
    
    baseurl: ""

```


Then to run your application locally using `config_dev.yml` you would enter something like
this into your command line.

```bash
    # This will run the application using the local host IP addres 127.0.0.1 on
    # the 4000 port. 
    > jekyll serve  --config _config.yml,_config_dev.yml 
    
    # If you need ot use a different IP address or port you can do this. In this example
    # the IP address and port are environmental variables but you could enter them in the
    # command instead.
    > jekyll serve --host $IP --port $PORT --config _config.yml,_config_dev.yml 
    
    # or 
    > jekyll serve --host 127.0.0.1 --port 5000 --config _config.yml,_config_dev.yml 
    
```

The `--config` option specifies the order the configuration files are used. In this case
`config.yml` is read first then `config_dev.yml` is read second and any settings in
`config_dev.yml` override equivalent settings in `config.yml`.










