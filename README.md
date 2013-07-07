# Middleman by Lifepillar

This is a [Middleman](http://middlemanapp.com) template I have built for myself. It includes:

- [Zurb Foundation](http://foundation.zurb.com);
- [Font Awesome](http://fortawesome.github.io/Font-Awesome/).

It has support for:

- blogging (through the [middleman-blog](https://github.com/middleman/middleman-blog) gem);
- [Disqus](http://disqus.com) comments (disabled by default);
- [Google Analytics](https://accounts.google.com) (disabled by default);
- [MathJax](http://www.mathjax.org) (optional);
- Syntax highlighting (through the [middleman-syntax](https://github.com/middleman/middleman-syntax) gem).

## Installation and Upgrade

You need [Bundler](http://bundler.io) before installing this template. To install Bundler:

    gem install bundler

With Bundler installed, you can create a new project as follows:

    git clone http://github.com/lifepillar/middleman-by-lifepillar
    cd middleman-by-lifepillar
    bundle install --path .bundle
    bundle exec middleman build
    bundle exec middleman server
    
Then, visit http://127.0.0.1:4567 to see your new web site!

You may also clone into `~/.middleman` and use as a Middleman template. For this you first need to install Middleman itself:

    gem install middleman

Then:

    git clone http://github.com/lifepillar/middleman-by-lifepillar ~/.middleman

From now on, new projects can be created with

    middleman init <project> --template=middleman-by-lifepillar
    cd <project>
    bundle install --path .bundle

One thing that bothered me with the other templates I have
seen around is that it was not trivial to update the external
components (basically, it has to be done manually). In this template I have added a Rakefile for the
purpose. After creating a project, you may type

    bundle exec rake update

to get the latest version of all the gems and components (there are other tasks to update components individually). In particular, the command above will update the content of the `lib` folder and will copy the necessary files from the `lib` folder into the `source` folder, at the appropriate locations.

I recommend that you keep your project under version control, so you can see exactly what is updated and you can easily revert if something goes wrong.

## Usage and Customization

One thing you may want to set in `config.rb` is the `Time.zone`. Then, you should edit the site metadata in the `data` folder. The project contains sample pages adapted from [Zurb Foundation's templates](http://foundation.zurb.com/templates.php) (Workspace and Blog, in particular). You may use them as a starting point to develop your site.

The code is organized as follows:

- Site metadata (site title, slogan, author, etc…) and menu data are kept in YAML files in the `data` folder. For example, to add a link to the main menu, just add a title/link pair to `main_menu.yml`.

- To use Disqus comments and Google Analytics, edit the corresponding partials (in the `partials` folder) with your account information. Then, include the partials in some template or layout. For example, to enable comments in blog posts, edit `blog/_article.erb`.

- To enable MathJax in a page, add

        layout: mathjax

  to the frontmatter. To configure MathJax, edit the corresponding partial in the `partials` folder.

- To create a new post, type

        bundle exec middleman article '<title>'

  and edit the generated file.

- The default author's name for blog posts (as well as the blog's title and slogan) can be set in `blog.yml`. To override the default author for a specific post, add an `author: <name>` key to that post's frontmatter. This information is correctly exported to the XML feed.

- The `lib` folder contains pristine copies of the external components (Foundation and Font Awesome). It is not needed to build a site (the relevant files have been copied into the `source` folder) and can be removed at any time (it is re-created by rake tasks anyway).
