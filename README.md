GitHub Pages requires public repo or a paid plan if you want to use a private repo (GitHub Pro is $4/month):
- https://github.community/t/publish-with-github-pages-keeping-repo-as-private-on-free-plan/10574
- https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/about-github-pages
- https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/faq-about-changes-to-githubs-plans

# How it Works

When the code is committed into the `master` branch, it triggers a Travis-CI build that can be monitored on travis-ci.com.
The output of the build is committed to the `gh-pages` branch which is actually used to serve the site by GitHub Pages.
On [settings](https://github.com/siddjain/siddjain.github.io/settings) page under GitHub Pages
section I have configured Your GitHub Pages site is currently being built from the **gh-pages** branch.

The Travis build looks at the [.travis.yml](.travis.yml) file for instructions on what to do when a build is triggered.
Among other things, the main step is to run following command to build the site:

```
bundle exec rake deploy
```

This command in turn references [Rakefile](Rakefile) for instructions on what it should do. In the [Rakefile](Rakefile)
you can see we have set:

```
t.deploy_branch = 'gh-pages'
```

The main command that builds the site in the [Rakefile](Rakefile) is:

```
bundle exec jekyll build --destination #{dest_dir}
```

And the `dest_dir` is committed to the `gh-pages` branch. This is how it works.
You can run this command yourself if you want to build manually although its nice to automate the work through Travis CI.

How are the posts written in asciidoc converted to HTML? This is done using the [jekyll-asciidoc](https://github.com/asciidoctor/jekyll-asciidoc)
Ruby gem defined in the [Gemfile](Gemfile).

## References

- https://docs.travis-ci.com/user/deployment/pages/

# [Local Setup](https://jekyllrb.com/docs/step-by-step/01-setup/)

Step 0:

If you are using WSL:

```
sudo apt update
sudo apt install make gcc g++ ruby-full graphviz
```

Step 1:

```
gem install jekyll bundler
```

Step 2:

```
bundle install
```

# To Run Locally:

Once you are done with the setup, you can run locally by first building the site:

```
bundle exec jekyll build
```

This is going to generate a `_site` folder that contains the site.

We can then run the web server:

```
bundle exec jekyll serve
```

Open browser and point to `http://127.0.0.1:4000/`