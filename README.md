# README

GitHub Pages requires public repo or a paid plan if you want to use a private repo (GitHub Pro is $4/month):
- https://github.community/t/publish-with-github-pages-keeping-repo-as-private-on-free-plan/10574
- https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/about-github-pages
- https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/faq-about-changes-to-githubs-plans

## How it Works

https://docs.travis-ci.com/user/deployment/pages/

When the code is committed into the `master` branch, it triggers a Travis-CI build that can be monitored on travis-ci.com.
The output of the build is committed to the `gh-pages` branch which is actually used to serve the site by GitHub Pages.
On [settings](https://github.com/siddjain/siddjain.github.io/settings/pages) page under GitHub Pages
section I have configured Your GitHub Pages site is currently being built from the **gh-pages** branch.
On [this](https://github.com/settings/installations/17792330) page I have given access to Travis-CI to this repo.

The Travis build looks at the [.travis.yml](.travis.yml) file for instructions on what to do when a build is triggered.
Among other things, the main step is to run following command to build the site:

```
bundle exec rake deploy
```

This command in turn references [Rakefile](Rakefile) for instructions on what it should do. The [Rakefile](Rakefile)
tells to execute the `GitDeployTask` in the plugin `rake-jekyll`. The source code of this task can be found 
[here](https://github.com/jirutka/rake-jekyll/blob/master/lib/rake-jekyll/git_deploy_task.rb). In the [Rakefile](Rakefile)
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

## Troubleshooting the build

Here is the sequence - the callstack if you will:

```
.travis.yml -> bundle exec rake deploy -> Rakefile -> GitDeployTask
```

The `GitDeployTask` is defined in the `rake-jekyll` plugin and source code is [here](https://github.com/jirutka/rake-jekyll/blob/master/lib/rake-jekyll/git_deploy_task.rb). 

## Manual deployment

In below `$TMP` is a bash variable that holds path to a temporary directory we will create and `$MAIN` is main directory synced to the master branch where you have your latest code that you want to deploy.

```
$ mkdir $TMP
$ cd $TMP
$ git clone git@github.com:siddjain/siddjain.github.io.git .
$ git checkout --track origin/gh-pages
$ cd $MAIN
$ bundle exec jekyll build --destination $TMP
$ cd $TMP
$ git push -q gh-pages:gh-pages
```

This is what the [GitDeployTask](https://github.com/jirutka/rake-jekyll/blob/master/lib/rake-jekyll/git_deploy_task.rb) does.

## References

- https://docs.travis-ci.com/user/deployment/pages/

## [Local Setup](https://jekyllrb.com/docs/step-by-step/01-setup/)

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

## To Run Locally:

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

## More Notes

[master][~/siddjain.github.io]$ git config user.email "758321+siddjain@users.noreply.github.com"
[master][~/siddjain.github.io]$ git push git@github.com-siddjain:siddjain/siddjain.github.io.git

~/.ssh/config:

```
# https://gist.github.com/rahularity/86da20fe3858e6b311de068201d279e3
#rahul-office account
Host github.com-siddhsql
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519

#rahul-personal account
Host github.com-siddjain
     HostName github.com
     User git
     IdentityFile ~/.ssh/siddjain.key
```

## Installing Graphviz

https://gist.github.com/siddjain/e3fa7fa8d52b1f61972eb439c7ff84d5
https://gist.github.com/siddjain/ee75716f971e7ed2f369baacb3c69728
https://gist.github.com/siddjain/3b980a1fa71b3a7cefe7ab384f86883f
https://gitlab.com/graphviz/graphviz/-/blob/main/ci/macos-install-runtime-dependencies.sh
https://forum.graphviz.org/t/failed-to-generate-image-dot-failed-format-png-not-recognized/2334
https://stackoverflow.com/questions/35688320/graphviz-seems-doesnt-support-png-and-map
https://gist.github.com/siddjain/3f47bdd90f9c9f188ed6932045eaaea0
https://gist.github.com/siddjain/016f121f9433ab44712b8021e1080502