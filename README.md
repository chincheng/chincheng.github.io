[//]: # (# My Blog)

[//]: # (Write some notes on my homepage located on Github.)

## How I create my blog

I use Hugo for designing my blog. I build a hugo image named **chincheng/hugo-builder** and push it to Dockerhub.


Open a terminal on my PC or NB.
Type a command script as shown below:

> alias hugo='docker run --rm -it -v $PWD:/src -u hugo chincheng/hugo-builder hugo'

where $PWD is my sources of blog content

Now, we can use the command, hugo, very easy.
For example, we want to know the usage of hugo.
> hugo help


It will pull the image automatically if it does not exist in your respository.

---
deploy.sh is a bash script which deploys and uploads my blog.
<pre><code>
#!/bin/bash

hugo='docker run --rm -it -v /home/chincheng/myblog:/src -u hugo chincheng/hugo-builder hugo'

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
#hugo # if using a theme, replace with `hugo -t <YOURTHEME>`
$hugo

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back up to the Project Root
cd ..

</pre></code>

