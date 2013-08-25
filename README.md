# Middleman by Lifepillar

This is a [Middleman](http://middlemanapp.com) template I have built for myself. It includes:

- [Zurb Foundation](http://foundation.zurb.com);
- [Font Awesome](http://fortawesome.github.io/Font-Awesome/).

It has support for:

- updating the included libraries to the latest version;
- blogging (through the [middleman-blog](https://github.com/middleman/middleman-blog) gem);
- [Disqus](http://disqus.com) comments (disabled by default);
- Classic and Universal [Google Analytics](https://developers.google.com/analytics/devguides/collection/analyticsjs/) (disabled by default);
- [MathJax](http://www.mathjax.org) (optional);
- Syntax highlighting (through the [middleman-syntax](https://github.com/middleman/middleman-syntax) gem).

## Installation

First, install [Bundler](http://bundler.io) if you haven't done so already:

    gem install bundler

To create a self-contained project (with all the required gems included in the project directory):

    git clone http://github.com/lifepillar/middleman-by-lifepillar my-project
    cd my-project
    bundle install

Then, to build and serve your web site:

    bundle exec middleman build
    bundle exec middleman server

Alternatively, if you already have Middleman installed globally, you may add this template inside `~/.middleman` with:

    git clone http://github.com/lifepillar/middleman-by-lifepillar ~/.middleman/middleman-by-lifepillar

After that, you can create a project with:

    middleman init my-project --template=middleman-by-lifepillar


## Upgrade

Assuming that you have created a self-contained project, you may type

    bundle exec rake update

to get the latest version of all the gems and the external components (if you have used `middleman init` to create the project, use `rake update` to update it). In particular, the command above will update the content of the `lib` folder (creating the folder if it doesn't exist) and will copy the necessary files from the `lib` folder into the `source` folder, at the appropriate locations.

I recommend that you keep your project under version control, so you can see exactly what is updated and you can easily revert if something goes wrong.


## Usage and Customization

One thing you may want to set in `config.rb` is the `Time.zone`. Then, you should edit the site metadata in the `data` folder. The project contains sample pages adapted from [Zurb Foundation's templates](http://foundation.zurb.com/templates.php) (Workspace and Blog, in particular). You may use them as a starting point to develop your site.

The code is organized as follows:

- Site metadata (site title, slogan, author, etc…) and menu data are kept in YAML files in the `data` folder. For example, to add a link to the main menu, just add a title/link pair to `main_menu.yml`.

- To use Disqus comments or Google Analytics, edit the corresponding partials (in the `partials` folder) with your account information. Then, include the partials in some template or layout. For example, to enable comments in blog posts, edit `blog/_article.erb`.

- To enable MathJax in a page, add

        layout: mathjax

  to the frontmatter. To configure MathJax, edit the corresponding partial in the `partials` folder.

- To create a new post, type

        bundle exec middleman article '<title>'

  and edit the generated file.

- The default author's name for blog posts (as well as the blog's title and slogan) can be set in `blog.yml`. To override the default author for a specific post, add an `author: <name>` key to that post's frontmatter. This information is correctly exported to the XML feed.

- If you do not need a blog, comment out or delete the

        activate :blog do |blog|
        ...
        end

  section in `config.rb` and add the following line instead

      ignore "blog/*"

  Then, edit `main.css.scss` and comment out or delete

      @import "blog";

- The `lib` folder contains pristine copies of the external components (Foundation and Font Awesome). It is not needed to build a site (the relevant files are copied into the `source` folder) and can be removed at any time (it is re-created by rake tasks anyway).
