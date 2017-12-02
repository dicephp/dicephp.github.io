# How to use this site

## Installation
The primary requirement is to have this repo downloaded on your machine. Assuming that you are in `/Users/onepercent/code`, you can run:

```bash
# Clone the repo
git clone git@github.com:vaibhav-kaushal/programming.onepercent.xyz.git
# Make the site directory
mkdir site.programming.onepercent.xyz
# Change directory to the cloned repo
cd programming.onepercent.xyz
# Copy the site deployment script to the git hooks folder
cp git_hooks/pre-push .git/hooks
# Make the hook executable
chmod +x .git/hooks/pre-push
```

Now, the repo is ready to be published as a site. However, to generate the site and actually publish it, you would need the following: 

#### Ruby
Use [rvm](http://rvm.io) to install Ruby 2.4. 
```bash
rvm install "ruby-2.4"
```

#### Some ruby gems
```bash
gem install jekyll bundler
```

#### NOTE
If you want to test how the theme looks, you can run `bundle exec jekyll serve` and navigate to `http://localhost:4000` and see how the site looks like.

### Install all the necessary tools for generation and hosting of the site
Once you have ruby and bundler, run the following: 

```bash
bundle install
```

Bundler will automatically download and install all the necessary gems.

## Deployment
Deployment logic is written in the hook that you had copied in the first step. The steps it takes are: 

1. It runs the jekyll build and puts the generated site inside the `site.programming.onepercent.xyz` folder. 
2. It `cd`s to that directory and removes the `git_hooks` folder if it exists (to ensure that the generated site does not contain the instructions for deployment).
3. If the directory is not a git repository, the script will initialize a new one.
4. If the *origin* remote is not configured, it will configure the remote to the appropriate repository. 
5. It sets the CNAME file to ensure that it can be served from the 
6. It will add all the content in the directory (`site.programming.onepercent.xyz`) to git repo and commit the repo. 
7. It will push the generated site's repository to github.

To deploy, all you have to do is to modify contents in this repo's directory (`programming.onepercent.xyz`) and push it to `origin`. Thus, running the following set of commands (assuming you are in the programming.onepercent.xyz directory) will update the site:

```bash
git add . 
git commit -m "Added more content to site"
git push origin master
```

#### NOTE
Remember that remote theme is fetched everytime you build the site. Depending on the speed of your network connection, it might take time. 

