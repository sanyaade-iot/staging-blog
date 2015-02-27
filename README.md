# Jekyll Incorporated
Modern Jekyll based blog. Great for companies, products or anything. See live at [blog.sendtoinc.com](http://blog.sendtoinc.com)

## Contributing (Spark Team Flow)

1. Get repo: `git clone ...`
2. Get changes: `git pull`
3. Fork a branch from master: `git checkout master` and `git checkout -b feature/spark-telegraph`
4. Write Markdown Content in `_posts` dir
5. Verify it looks good locally ( see instructions below )
6. Deploy to Staging ( see instructions below)
7. Deploy to production ( see instructions below)

*NOTE*: Please remember to write your blog post on a separate branch; any changes pushed to `master` will be automatically deployed to the blog.

## Installation & Usage
    bundle install
    jekyll serve --watch

_Note: Requires Ruby version 1.9.3 =>. For example use [rbenv](https://github.com/sstephenson/rbenv)_

## Configuration
Edit: _config.yml (general options), main.css (theme colors &amp; fonts)

```
jekyll-incorporated/
├── _config.yml
├── _assets/
    ├── stylesheets/
        ├── main.scss
```

_Note: when editing _config.yml, you need to restart jekyll to see the changes.__

## Publish to staging

Deployment is now done automatically by Travis CI. To publish the blog to staging, simply merge your changes into the `staging` branch.

## Publish to production

To publish the blog to production, simply merge your changes into the `master` branch.

## Authors

Originally build for [sendtoinc.com](https://sendtoinc.com), your workspace for sharing and organizing knowledge

**Karri Saarinen**

+ [http://twitter.com/karrisaarinen](http://twitter.com/karrisaarinen)
+ [http://github.com/ksaa](http://github.com/ksaa)

**Jori Lallo**

+ [http://twitter.com/jorilallo](http://twitter.com/jorilallo)
+ [http://github.com/jorde](http://github.com/jorilallo)

## Todo:

+ Documentation
+ Less config files
+ Better deploy scripts

## Copyright and license

Copyright 2013 Kippt Inc. under [The MIT License ](LICENSE)
