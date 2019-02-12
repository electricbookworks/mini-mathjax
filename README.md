# Smaller MathJax for offline use

This repo is based on the Gruntfile [here](https://github.com/mathjax/MathJax-grunt-cleaner) and the guidance [here](https://github.com/mathjax/MathJax-docs/wiki/Guide:-reducing-size-of-a-mathjax-installation/1814429ed1e97bfb7675c0fd400804baa9287249). It's a good idea to read those pages before using this tool.

You'd use this repo for quickly generating a customised, stripped-down version of MathJax for offline use. You customise what is going to be left in your offline version, and the Grunt script discards everything else.

## Usage

### Use as is

If you're happy to use the offline version we've created for TeX input with SVG output, unzip `build.zip` and place these contents into your own `mathjax` or similar folder:

- `extensions`
- `jax`
- `MathJax.js`
- `LICENSE`

We've done this in the `build` folder here for demo purposes. You can see that in action [here](https://electricbookworks.github.io/mini-mathjax).

You'll also need to add a MathJax config to your page (as a Javascript object). See `index.html` here for an example. Note that the config script element appears before the link to `MathJax.js`.

### Customise your MathJax package

If you want a different offline package:

1. You must have Grunt installed. If you don't yet, follow the [official instructions](https://gruntjs.com/getting-started). Or:

    start by updating npm:

    ```
    npm update -g npm
    ```

    then run

    ```
    npm install -g grunt-cli
    ```

1. Open this folder in a terminal and run `npm install` to install the necessary `node_modules`.
1. The master version of MathJax is tracked as a [Git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) in this repo. To get the files, run `git submodule init && git submodule update` in this folder. That will clone the latest version of MathJax into the `MathJax-master` folder. In future, to update the MathJax files, `cd MathJax-master && git fetch && git merge`.
1. Copy into the root of this repo *only* these from `MathJax-master`:

    1. all folders
    2. `MathJax.js`
    3. `LICENSE`
    
    (Some of the files in `MathJax-master` have the same names as ones we need in this repo's root, such as `package.json` and `README.md`. Don't overwrite those! This is also why we have edited the list under `notcode` in the Gruntfile, or we'd lose our files, too.)

1. In `Gruntfile.js`, change which lines we've commented out already in the `template` task (lines 324 to 365). You comment out a line to *keep* a component. Anything not commented out gets removed (cleaned) from your offline MathJax.
1. Run `grunt template`.
1. Use the MathJax files that remain in the project root for your website.
