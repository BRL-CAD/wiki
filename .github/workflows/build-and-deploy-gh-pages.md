# This action rebuilds the docs whenever there is a change (push),
# and deplys it automatically on GitHub pages (the branch gh-pages).
#
name: Build and Deploy GitHub Pages
on:
  push:
    branches:
      - main
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2.3.1
      - run: pip3 install mkdocs
      - run: mkdocs build
	  - run: mkdocs gh-deploy

      - name: Deploy to GitHub Pages
        uses: JamesIves/github-pages-deploy-action@4.1.4
        with:
          branch: gh-pages # The branch the action should deploy to.
          folder: html # The folder the action should deploy.