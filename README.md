### Local setup 

1. Download and install a Ruby+Devkit version from [RubyInstaller Downloads](https://rubyinstaller.org/downloads/). Use default options for installation.
2. Run the `ridk install` step on the last stage of the installation wizard. From the options choose `MSYS2 and MINGW development tool chain`.
3. Open a new command prompt window, so that changes to the ``PATH`` environment variable becomes effective. Install Jekyll and Bundler using ``gem install jekyll bundler``.
4. Check if Jekyll has been installed properly ``jekyll -v``.
5. Install all necessary gems ``bundle install``.
6. Build and run the project ``bundle exec jekyll serve``.
    1. The website will likely be served at the address ``http://127.0.0.1:4000/blog/``. Try take a look at the output window if it does not work.
    2. Auto-regeneration should also be enabled. No need to rerun the command after making changes.


### Github action
Check out the file `.github/workflows/jekyll.yml`.