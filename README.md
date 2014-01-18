# Middleman by Lifepillar

This is a [Middleman](http://middlemanapp.com) template I have built for myself.
It has support for:

- [Zurb Foundation 5 or later](http://foundation.zurb.com);
- [Font Awesome 4.0.3](http://fortawesome.github.io/Font-Awesome/);
- blogging (through the [middleman-blog](https://github.com/middleman/middleman-blog) gem);
- syntax highlighting (through the [middleman-syntax](https://github.com/middleman/middleman-syntax) gem);
- [Disqus](http://disqus.com);
- Classic and Universal [Google Analytics](https://developers.google.com/analytics/devguides/collection/analyticsjs/);
- [MathJax](http://www.mathjax.org).

## Requirements

- Git!
- Ruby 1.9+ (tested with Ruby 2.x).
- [Bower](http://bower.io).


## Installation

First, install [Bundler](http://bundler.io) if you haven't done so already:

    gem install bundler

To create a self-contained project (with everything included inside the project directory):

    git clone http://github.com/lifepillar/middleman-by-lifepillar my-project
    cd my-project
    bundle install
    bower install

`bundle install` will update all the gems.
`bower install` will create a directory called `bower_components`, containing Foundation's files.

Then, to build and serve your web site:

    bundle exec middleman build
    bundle exec middleman server

Alternatively, if you already have Middleman installed globally, you may add this template inside `~/.middleman` with:

    git clone http://github.com/lifepillar/middleman-by-lifepillar ~/.middleman/middleman-by-lifepillar

After that, you can create a project with:

    middleman init my-project --template=middleman-by-lifepillar
    cd my-project
    bower install


## Upgrade

To upgrade the installed gems execute this command inside
the project root directory:

    bundle update

To upgrade Foundation:

    bower update


## Usage and Customization

One thing you may want to set in `config.rb` is the `Time.zone`. Then, you should edit the site metadata in the `data` folder. The project contains sample pages adapted from [Zurb Foundation's templates](http://foundation.zurb.com/templates.html) (Workspace and Blog). You may use them as a starting point to develop your site.

Site metadata (site title, slogan, author, etc…) and menu data are kept in YAML files in the `data` folder. For example, to add a link to the main menu, just add a title/link pair to `main_menu.yml`.

In the frontmatter of any page, you may use the variables `head`, `beginbody`, and `endbody`
to load additional partials, just before the `</head>` tag, just after `<body>`, and just before `</body>`, respectively.
For example, for a page that includes MathJax, Disqus comments and Google Analytics, your frontmatter might look like this:

    ---
    title: My Page
    head: [mathjax]
    endbody: [disqus, analytics]
    ---

Each variable takes a list of names of partials, which must exist in the `partials` folder. You may
use your own partials in the same way. Of course, for a bunch of pages having the same structure,
it is better to define a custom layout. See, for instance, the `mathjax.erb` layout in the `layouts` folder.


To create a new post, type

    bundle exec middleman article '<title>'

and edit the generated file. The default author's name for blog posts (as well as the blog's title and slogan) can be set in `blog.yml`. To override the default author for a specific post, add an `author: <name>` key to that post's frontmatter. This information is correctly exported to the XML feed.

If you do not need a blog, comment out or delete the following section in `config.rb`:

    activate :blog do |blog|
    ...
    end

and add the following line instead

    ignore "blog/*"

Then, edit `main.css.scss` and comment out or delete

    @import "blog";
