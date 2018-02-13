# Smaller MathJax for offline use

This repo is based on the Gruntfile [here](https://github.com/mathjax/MathJax-grunt-cleaner) and the guidance [here](https://github.com/mathjax/MathJax-docs/wiki/Guide:-reducing-size-of-a-mathjax-installation/1814429ed1e97bfb7675c0fd400804baa9287249). It's a good idea to read those pages before using this tool.

You'd use this repo for quickly generating a customised, stripped-down version of Mathjax for offline use. You customise what is going to be left in your offline version, and the Grunt script discards everything else.

## Usage

### Use as is

If you're happy to use the offline version we've created for TeX input with SVG output, unzip `mini-mathjax.zip` and place these contents into your own `mathjax` or similar folder:

    - `extensions`
    - `jax`
    - `MathJax.js`
    - `LICENSE`

### Customise your MathJax package

If you want a different offline package:

1. You must have Grunt installed. To do this, start by updating npm:

    ```
    npm update -g npm
    ```

    then run

    ```
    npm install -g grunt-cli
    ```

    Even better, follow the [official instructions](https://gruntjs.com/getting-started).

2. Open this folder in a terminal and run `npm install` to install the necessary `node_modules`.
1. The `MathJax-master` folder contains a full copy of MathJax for convenience. You may want to update it from `https://github.com/mathjax/MathJax/archive/master.zip`, in case there have been changes to the original MathJax repo.
1. Copy *only* the folders in `MathJax-master` and the `MathJax.js` and `LICENSE` files into the root of this repo. (Some of the files have the same names as ones we need here, such as `package.json` and `README.md`. Don't overwrite those! This is also why we have edited the list under `notcode` in the Gruntfile, or we'd lose our files, too.)
1. In `Gruntfile.js`, change which lines we've commented out already in the `template` task (lines 324 to 365). You comment out a line to *keep* a component. Anything not commented out gets removed (cleaned) from your offline MathJax.
1. Run `grunt template`.
