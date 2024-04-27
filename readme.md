<b>JEKYLL + GITHUB PAGES</b>
- <https://jekyllthemes.io/jekyll-documentation-themes>
- <https://github.com/pmarsceill/just-the-docs>
- <https://pmarsceill.github.io/just-the-docs>
- <https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll>
- <https://jekyllrb.com/docs/github-pages>

dev (JEKYLL_ENV=development):
`bundle exec jekyll serve --livereload --force_polling --incremental --config _config.yml,_config_development.yml`

(prod?:)
`JEKYLL_ENV=production PAGES_REPO_NWO=phlppnhllngr/phlppnhllngr.github.io bundle exec jekyll build`

*Some configuration settings [_config.yml] cannot be changed for GitHub Pages sites.*
*GitHub Pages cannot build sites using unsupported plugins. If you want to use unsupported plugins, generate your site locally and then push your site's static files to GitHub.*
<https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#configuring-jekyll-in-your-github-pages-site>
supported plugins: <https://pages.github.com/versions/>


```
# H1
{: .no_toc }

## Inhalt
{: .no_toc }
- TOC
{:toc}

## H2
```
