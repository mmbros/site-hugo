+++
date = "2017-03-03T22:46:54Z"
draft = true
title = "Deploy Hugo site on GitHub"
description = "Description"
tags = ["hugo", "github", "html"]
+++

Links:

- [Hugo - Hosting on GitHub Personal/Organization Pages](http://gohugo.io/tutorials/github-pages-blog/#hosting-personal-organization-pages)
- [Deploy your blog to github pages automatically using Hugo and Travis](http://rcoedo.com/post/hugo-static-site-generator/)

We’ll create two separate repos, one for Hugo’s content, and a git submodule
with the public folder’s content in it.

Step by step:

1. Create on GitHub `<your-project>-hugo` repository (it will host Hugo’s
   content)
2. Create on GitHub `<username>.github.io` repository (it will host the `public`
   folder: the static website)
3. `git clone <<your-project>-hugo-url> && cd <your-project>-hugo`
4. Make your website work locally (`hugo server --watch`)
5. Once you are happy with the results, <kbd>Ctrl+C</kbd> (kill
   server) and `rm -rf public` (don't worry, it can always be regenerated
   with `hugo`)
6. `git submodule add -b master https://github.com/<username>/<username>.github.io public`
7. Almost done: add a `deploy.sh` script to help you (and make it executable:
   `chmod +x deploy.sh`):

	```
	#!/bin/bash
	echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

	# Build the project.
	hugo # if using a theme, replace by `hugo -t <yourtheme>`

	# Go To Public folder
	cd public

	# Add changes to git.
	git add -A

	# Commit changes.
	MSG="rebuilding site `date`"
	if [ $# -eq 1 ]
	  then MSG="$1"
	fi
	git commit -m "$MSG"

	# Push source and build repos.
	git push origin master

	# Come Back
	cd ..
	```

8. `./deploy.sh "Your optional commit message"` to send changes to `<username>.github.io` (careful, you may also want to commit changes on the `<your-project>-hugo` repo).

That's it! Your personal page is running at [http://username.github.io/](http://username.github.io/) (after up to 10 minutes delay).

