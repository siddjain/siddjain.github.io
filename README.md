GitHub Pages requires public repo or a paid plan (GitHub Pro is $4/month):
- https://github.community/t/publish-with-github-pages-keeping-repo-as-private-on-free-plan/10574
- https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/about-github-pages
- https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/faq-about-changes-to-githubs-plans

On [settings](https://github.com/siddjain/siddjain.github.io/settings) page under GitHub Pages
section I have configured Your GitHub Pages site is currently being built from the **gh-pages** branch

# [Local Setup](https://jekyllrb.com/docs/step-by-step/01-setup/)

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