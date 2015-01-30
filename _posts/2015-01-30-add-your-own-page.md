---
layout: post
title: How to Add Your Own Page to Our Website
author: Paul Wilson
category: upcoming
tags: meeting github jekyll
---

This guide assumes that you already have a [Github](http://github.com)
account, and that you have setup `git` previously on your local machine.

## Get your own copy of the repository to start making changes.

1. Go to the [repository][thw-wi-repo] on Github.

2. Click on the fork button on the top right.  If you have multiple
   organizations, select which one will be the owner of this fork.

3. At the command line of your local machine: `git clone
   git@github.com:my_user_name/wisconsin.git` (be sure to use your own Github
   username in place of `my_user_name`)

4. Change directories into the repo: `cd wisconsin`

5. In order to practice good habits with `git`, let's make a branch for these
   changes: `git checkout -b my_new_topic`

## Copy the Template to Start Your New Post

1. The `_drafts` directory has a useful template from which to start: `cp _drafts/YYYY-MM-DD-subject.md _posts/<YYYY-MM-DD-topic>.md`

2. Be sure to replace `<YYYY-MM-DD-topic>` with the year, month, date and title
  of your topic.  For example, this page is `2015-01-30-add-your-own-page`.

## Write Your Content

**This is where the fun begins!**

This standard template is using a flavor of *markdown* to apply
formatting. *Markdown* is intended to be a very natural and concise way to apply
very simple formatting to text.

### Metadata

Our website is being processed and formatted by the `jekyll` processing
tool. This means that some metadata is available for each page.  This metadata
is available to use in your page by placing it inside double curly braces like this:
`{{ "{{ some.metadata " }}}}`.

Some of this metadata comes from the configuration for the whole site.  For
example, you can access `{{ "{{ site.url " }}}}` as the base URL for the site: {{ site.url }}

There is also metadata that you can set for this page by changing the entries
that you see at the top of the template:

```
---
layout: post
title: Insert your title here
author: Paul Wilson
category: upcoming
tags: choose some keywords as tags
---
```

These metadata do the following:

- `layout`: determines which template will be used to format the page. `post`
  is almost always the right choice.

- `title`: is your choice and may automatically be used in other places like
  lists of posts/topics.

- `author`: is the name(s) of the person/people who wrote the page.

- `category`: this should be `upcoming` until after the presentation at which
  it can be changed to `posts`

- `tags`: is a list of keywords that will be used to categorize your post.
  You can choose any keywords you like, although you may want to check the
  list of [existing tags](tags.html) to categorize your post with other posts
  in a reasonable way.

### Formatting

In addition to this metadata, you can format the text using some very simple
command.  Here are some basics:

- `#` or `##` or `###`, etc: This will indicate a heading of level 1, level 2,
  level 3, and so on.

- `**this text is bold**` will produce **this text is bold**

- `*this text is italics*` will produce *this text is italcs*

- `***this text is bold-italics***` will produce ***this text is bold-italcs***

- `[link text](link url)` will create a link from that "link text" to that "link url"

- quoting your text with single back ticks will create an inline code-block

- `---` on a line by itself will create a horizontal rule like this:

---

Feel free to consult previous posts to get some clues for other useful markdown.


## Add and Commit Your Changes

You can do this frequently as you make changes.

- Stage your file in preparation for committing the changes: `git add _posts/<YYYY-MM-DD-topic>.md`

- Commit your file with an appropriate commit message: `git commit -m "Here is a great addition"`

## Testing Your Changes

You can test your changes locally if you have installed jekyll locally.  This
means you won't have to push the changes to Github to see how they look.  I'll
leave many of the details to the
[jekyll documentation](http://jekyllrb.com/docs/home/).  Once you have jekyll
installed, it is very useful to use it in server mode (`serve`) and have it
constantly watch (`-w`) for changing files.  In addition, we have provided a
special config file (`_config_dev.yml`) that will set some site metadata to be
good choices for local testing.

`jekyll serve --config _config_dev.yml -w`

## Push Your Branch and Create a Pull Request

1. When your page is ready to be published, you can push it to your clone of
   the repository: `git push origin my_new_topic`.

2. Go to your clone of the repository on Github

3. Initiate a pull request agains the `gh-pages` branch of the [upstream repository]({{ site.github.repository_url }}).

4. Wait for it to be approved!

## Presenter: Paul Wilson

[Paul Wilson](http://cnerg.engr.wisc.edu/people/pphw.html) is a nuclear
engineering professor in the Engineering Physics department and has long been
inspiring students to awaken the hacker within.

### Attending

- Paul Wilson

## 
<+ notes +>


## Lightning Talks 

## <+ person +> : <+ topic +>

## <+ person +> : <+ topic +>


[thw-wi-repo]: {{ site.github.repository_url }}
[code]: {{ site.github.repository_url }}/tree/master/topic
