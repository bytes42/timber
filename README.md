# Timber - A Jekyll Theme
In a nutshell Timber is an open-source Jekyll theme. Rather than describing it verbatim it's far simpler to look at an example, [like this one](http://bytes42.github.com/timber "Example of Timber in action").

If you like what you see then read on.

- [Prerequisites](#prereq)
- [Configuration](#config)
- [Content](#content)
- [Styling](#style)
- [Build, Test &amp; Deploy](#btd)
- [Browser Support](#browsers)
- [Issues, Requests &amp; Questions](#irq)
- [Sites Using Timber](#using)

## <a name="prereq">Prerequisites</a>
Timber has the following dependencies:

- `git` - to get the project
- `jekyll` - to build the project

It also has the following optional dependencies:

- `haml` - generate HTML code from HAML definitions (only required if you plan to change the HTML)
- `sass` - generate CSS code from SASS definitions (only required if you plan to change the standard CSS rules)
- `rake` - run provided rake tasks for building, testing and deploying to GitHub

## <a name="config">Configuration</a>
All configuration is handled in `_config.yml`. What follows is a description of each available option:

- `name` - the text to be used in the browser title bar and copyright notice
- `logo` - the text to be used in the logo element (between "blurb" and "journal")
- `author` - value to be place in the author HTML `meta` tag
- `description` - value to be place in the description HTML `meta` tag
- `favicon` - path to favicon `.ico` file; ignored if no value given.
- `share_count` - the number of share options to include at the foot of a post.  
    - Zero or no value will remove the shared block
    - A value of 1 will only shown the aggregated share button
    - A value of 2 to 12 will show the aggregated share button as well as a number of specific site icons (the set adjusts according to the user, showing what [AddThis](http://www.addthis.com) deems most likely for the user to click; see the AddThis documentation on preferred entries).
- `addthis_username` - your [AddThis](http://www.addthis.com) username for collecting share analytics; optional.
- `show_tags` - if `true` show tags section at foot of post, otherwise `false`.
- `related_count` - the number of related posts to show at the foot of a post. _The quality of the related matches can be improved with Jekyll's `--lsi` option, see Jekyll documentation for more information_/
    - Zero or no value will remove the related block
    - A value of 1 or more will show the related block with the defined number of related posts.
- `elsewhere_<service>` - for each supported _elsewhere_ there is a configuration option; an entry here will result in the service being shown in the elsewhere section, no value it will be removed. _Note I have only added a handful of services, if you require more get in touch or you can add yourself, it should be straight forward to do._
    - email
    - dribbble
    - github
    - linkedin
    - meetup
    - spotify
    - twitter
    - rss
- `baseurl` - a Jekyll option used to define site path from root the directory. For GitHub Pages deployment specifically use the following:
    - _User/Organisation Page_ - Leave blank
    - _Project Page_ - requires `baseurl` to use project-name path, i.e.`/<project-name>` such as `/timber`.
- `exclude` - a Jekyll option used to exclude files/directories being copied to `_site`, add to if required.
- `pygments` - a liquid extension for formatting source code.  
- `permalink` - a Jekyll option controlling post permalinks; can be changed freely.
- `safe` - a Jekyll option permitting _plugin use or not. Must be false in order for _plugins to work.

## <a name="content">Content</a>
There are three sections which will definitely require your own content:

- `_includes/about.md` - The text shown in the blurb's about section.
- `_includes/projects` - The text shown in the blurb's about section.
- `_posts/*.md` - The collection of posts which forms your journal.

There is one section which can optionally be edited:

- `_includes/colophon.md` - The text showing thanks to the free resources used in making the site; recommended you leave this intact.

## <a name="style">Styling</a>
All styling is applied with rules set out in three stylesheets, namely:

- `css/stylesheet.[css|sass]` - controls all layout, text, images and links (master stylesheet).
- `css/override.[css|sass]` - empty stylesheet for users of Timber to add overrides to the existing CSS rules; by adding overrides here users can easily pull updates to `css/stylesheet.css` and `css/elsewhere.css`.
- `css/basic.css` - used in cases where it's detected that the site visitor's Internet Explorer can't provide a consistent presenation of the site (see [browser support](#browsers).

## <a name="btd">Build, Test &amp; Deploy</a>
A number of rake tasks are provided to simplify building, testing and deploying Timber. All rake tasks should be run from the root directory this automatically picking up `Rakefile`.

### Build
To build Timber means combining the content and templates into a collection of static files.

`rake build`

This will first generate the HTML files from the HAML definitions and then run the site through Jekyll. The generated site will reside under `_site`.

### Test
Jekyll allows you to serve your site locally in order to test.

`rake preview`

This will first build and then serve up the site. View the site in your browser at `0.0.0.0:4000`. Note if you are using a `baseurl` in `_config.yml` you will need to add this to the URL, e.g. `baseurl: timber` resolves at `0.0.0.0:4000/timber/`.

### Deploy
If you decide to host your site at GitHub Pages you must be aware that committing a Jekyll site to GitHub results in GitHub attempting to parse it with Jekyll. You must also note that GitHub does not support plugins, a feature Timber make use of (see `_plugins` directory). Roughly translated GitHub cannot be relied upon to generate the site, instead an already generated site must be committed.

This is achieved like so:

- Place all source content on one branch
- Place all generated content on a second branch
- Place a `.nojekyll` file in the source branch root to stop Jekyll attempting to parse the site source

I'd highly recommend the following branch names:

- User/Organisation repo - place source on newly created `source` branch, place generated site on `master`
- Project repo - place source on `master` branch, place generated site on a newly created `gh-pages` branch

Once the branches are created - ensuring the branch to which generated content will be committed is empty - the site can be deployed.

`rake deploy[<src>, <dest>]`

The deploy rake task will parse the HAML, parse the site with Jekyll and then commit the resultant site to the destination (generated site) branch. This task **must be run from the source branch**. Here are some examples:

- `rake deploy["source","master"]`
- `rake deploy["master","gh-pages"]`

The first example would be used on a user/organisation page whereas the second would work on a project page.

If the deploy is successful you should receive an email confirming your site has been built. Your site will be available at either `http://<username>.github.com` for user/organisation pages or `http://<username>.github.com/<project-name>` for project pages.


## <a name="browsers">Browser Support</a>
Timber has been built following the principles of [progressive enhancement](http://www.alistapart.com/articles/understandingprogressiveenhancement/ "'Read more about progressive enhancement'"). 

- **HTML5** - for browsers which do not supporting HTML5 the [html5shim](http://code.google.com/p/html5shim/) is used; where JavaScript is turned off basic styling is applied via `css/basic.css`
- **CSS3** - CSS3 has only been used for non-essential styling and therefore lack of support presents no issues
- **jQuery** - jQuery has only been used for non-essential features and therefore lack of support presents no issues

## <a name="irq">Issues, Requests &amp; Questions</a>
If you encounter any issues, have a feature request or have a question about Timber then please post it to the [issue tracker](https://github.com/bytes42/timber/issues "Issue Tracker"). I'll provide a response to every issue as quickly as possible.

## <a name="using">Sites Using Timber</a>
If you do make use of Timber then **please let me know** and I'll add a link to your site here.
