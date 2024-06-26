### Local setup 

1. Download and install a Ruby+Devkit version from [RubyInstaller Downloads](https://rubyinstaller.org/downloads/). Use default options for installation.
2. Open a new command prompt window, so that changes to the ``PATH`` environment variable becomes effective. Install Jekyll and Bundler using ``gem install jekyll bundler``.
3. Check if Jekyll has been installed properly ``jekyll -v``.
4. Install all necessary gems ``bundle install``.
5. Build and run the project ``bundle exec jekyll serve``.
    - The website will likely be served at the address ``http://127.0.0.1:4000/blog/``. Try take a look at the output window if it does not work.
    - Auto-regeneration should also be enabled. No need to rerun the command after making changes.


### Local dev cheatsheet
1. Show the gem's local path `bundle show <gem name>`
    ```
    D:\Src\dgtvan.github.io>bundle show minima
    C:/Ruby32-x64/lib/ruby/gems/3.2.0/gems/minima-2.5.1
    ```