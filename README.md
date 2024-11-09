# Documentation project

This repo contains a Nextra (Next.js) project for hosting technical documentation and deploying it on GitHub Pages.


## Installation

### From the entire repo

If the documentation project is hosted in a repo (just like this one):

1. In your repo settings:
    1. Activate GitHub Pages
    2. Select `GitHub Actions` as source
2. Download this repo contents
3. Clone your repo
4. Copy this repo contents to your repo 
5. Edit the file `next.config.mjs` and change the variable `basePath` to the URL you want for the docs under your GitHub URL
6. Push the changes to your repo
7. The workflow will publish the contents in your GitHub Pages everytime you do a push to the main branch 

### From a folder in a repo

1. Follow steps 1-5 from the previous install process
2. Edit the file `nextjs.yml` inside the folder `.github/workflows` and change:
    1. In the `Build with Next.js` step, add `cd [YOUR_FOLDER]` (or the name of the folder that hosts the doc project) to navigate to the specific directory before running next build. This tells Next.js to build the content only from that directory. For example:
    ```
    - name: Build with Next.js
            run: |
              cd docs
              ${{ steps.detect-package-manager.outputs.runner }} next build
            working-directory: ./docs
    ```
    2. In the `Upload artifact` step, set the path to `./[YOUR_FOLDER]/out` so that it uploads only the files built in that directory and not the entire repository’s content. For example:
    ```
    - name: Upload artifact
            uses: actions/upload-pages-artifact@v3
            with:
              path: ./docs/out
    ```
3. Follow steps 6-7 from the previous install process

## Usage

All the content is written in Markdown files with the .mdx extension (because they can include React components, though it’s not required). To add new ones:

1. Add or copy the markdown file/s to the pages folder
2. Push the changes to the main branch
3. Wait until the GitHub Action that compile and deploys the project finishes

### To add a subtree to the documentation structure

1. Create a folder inside the pages folder
2. Add or copy the markdown file/s to the new folder
2. Push the changes to the main branch
3. Wait until the GitHub Action that compile and deploys the project finishes

You can control the order of the files, subtrees and the names by using the `_meta.ts` files inside the `pages` folder and subfolders. For a complete info about how to do this please check the [Nextra documentation page](https://nextra.site/docs/docs-theme/page-configuration).