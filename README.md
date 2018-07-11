# Apprentice

A lightweight framework for creating workshops using jekyll and markdown (mostly).
The concept is a good workshop will consist of 

- A strong hands on component
- Good online material to refer to both before and after the workshop
- A brief presentation to orient attendees
- Be organized 

The Apprentice framework is composed of 4 primary components.

1. A home page 
2. Online tutorial composed of _units_
3. A slide deck for presentations
4. Instructors notes


## Getting Started

### Installing Jekyll

Follow the appropriate instructions at https://jekyllrb.com/docs/installation/.
If you already have the Ruby programming language installed then it should
be as easy as doing the following on your terminal or command line.
well.

```ruby
    > gem install jekyll bundler
```

If you are running Jekyll locally on windows, refer to
[Jekyll on Windows](https://jekyllrb.com/docs/windows/) as

### Configuration

Edit the _config.yml with the correct information for your workshop, following
the instructions in the comments.

### Running Jekyll Locally

For full documentation on running and deploying Jekyll websites, 
see https://jekyllrb.com/docs/usage/. If you want to be optimistic,
you can just run your website locally as follows.

``` bash
    > jekyll serve --host 0.0.0.0 --port 8080 --baseurl ''`
```

The default port is 4000 so you can use that and omit that option. 
The  `--baseurl ''` option overrides the value from the `_config.yml` allowing 
you to run it locally and then on Github pages as well. More info 
at https://jekyllrb.com/docs/usage/. The HTML is generated when you run the 
server.

Alternatively, you can generate the HTML and run your site from that.

```
  > jekyll build
  # => The current folder will be generated into ./_site
  
  > jekyll build --destination <destination>
  # => The current folder will be generated into <destination>
  
  > jekyll build --source <source> --destination <destination>
  # => The <source> folder will be generated into <destination>
  
  > jekyll build --watch
  # => The current folder will be generated into ./_site,
  #    watched for changes, and regenerated automatically.
```

The default Apprentice Template should give you some filler content, but
be otherwise functional.


### Deploying to Github

The easiest way to deploy to GitHub pages is to make a new branch 
called `gh-pages` and push it up to GitHub. Go to the settings of your
repository to get the URL and you should be able to see the website in 
a few minutes.








### Licensing

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/">
    <img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" />
</a>
<br />
This work is licensed under a 
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/">
Creative Commons Attribution 4.0 International License</a>.

All content in this repository are licensed under the Creative Commons 4.0 - 
Attribution License or where applicable, as with software code, an Apache 2.0
Software License.


### Contributing

Contributions are welcome. You can contribute to this workshop by 

1. Submitting issues
2. Forking the repository, editing it and submitting your proposed changes as a pull request.

### Contributors

Rob Olendorf




