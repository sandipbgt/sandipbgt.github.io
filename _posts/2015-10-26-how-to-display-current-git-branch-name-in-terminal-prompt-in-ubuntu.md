---
layout:     post
post_id : 14
title:      "How To Display Current Git Branch Name In Terminal Prompt In Ubuntu?"
date:       2015-10-26 13:08 +0545
author:     "Sandip Bhagat"
thumbnail: "https://farm6.staticflickr.com/5734/22459069076_e69af8100f_z_d.jpg"
---

Git and GitHub is one of the most imortant tool for software development.
One of its great feature is branching/merging. Whenever I am inside a git directory, I have to run `git status` to see which branch I am currently working on. Contstantly switching branches is always confusing to me.

The solution to this is to have the terminal prompt display the current branch name.

![My terminal prompt](https://farm6.staticflickr.com/5734/22459069076_e69af8100f_z_d.jpg)

## Installation

First create a `.bash` directory in your home directory and clone the project to it:

{% highlight bash %}
$ mkdir ~/.bash
$ cd ~/.bash
$ git clone https://github.com/jimeh/git-aware-prompt.git
{% endhighlight %}

Edit your `~/.bashrc` and add the following to the bottom:

{% highlight bash %}
export GITAWAREPROMPT=~/.bash/git-aware-prompt
source "${GITAWAREPROMPT}/main.sh"
export PS1="\${debian_chroot:+(\$debian_chroot)}\u@\h:\w \[$txtcyn\]\$git_branch\[$txtred\]\$git_dirty\[$txtrst\]\$ "
{% endhighlight %}

Now `cd` into any git directory, current branch name will be shown in the terminal prompt.