# Silent Asset Compilation Failure

## Stack
- rails 5.2.3
- webpacker 4.0.7
- tailwindcss 1.0.4
- yarn 1.15.2
- node 8.12.0
- heroku

## Bug
During the first deployment of a Rails app to Heroku, a build failure occurred. The Heroku logs show `precompiling assets failed`. The failure is silent with no useful error message in the stacktrace.

    # Heroku build logs
    Preparing app for Rails asset pipeline
       Running: rake assets:precompile
       yarn install v1.12.3
       [1/4] Resolving packages...
       [2/4] Fetching packages...
       info fsevents@1.2.9: The platform "linux" is incompatible with this module.
       info "fsevents@1.2.9" is an optional dependency and failed compatibility check. Excluding it from installation.
       [3/4] Linking dependencies...
       warning "@rails/webpacker > pnp-webpack-plugin > ts-pnp@1.1.2" has unmet peer dependency "typescript@*".
       warning " > webpack-dev-server@3.7.1" has unmet peer dependency "webpack@^4.0.0".
       warning "webpack-dev-server > webpack-dev-middleware@3.7.0" has unmet peer dependency "webpack@^4.0.0".
       [4/4] Building fresh packages...
       Done in 26.82s.
       I, [2019-06-14T22:11:47.419600 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/hero-5b1fbcba90f70d511e65b954c46caabe9c18034c54436def3b8e905a8b0e4dc9.png
       I, [2019-06-14T22:11:50.077551 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/application-d25752b9ab667418e852ef42e1f03f47bd57a7d382318572379f2740fd4b6c95.js
       I, [2019-06-14T22:11:50.078466 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/application-d25752b9ab667418e852ef42e1f03f47bd57a7d382318572379f2740fd4b6c95.js.gz
       I, [2019-06-14T22:11:50.086553 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/application-e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855.css
       I, [2019-06-14T22:11:50.086770 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/application-e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855.css.gz
       I, [2019-06-14T22:11:56.203802 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/administrate/application-6a75fccf481841c324aa19339808666fe7b4accb3b3a49b1d78d4bd627141d85.js
       I, [2019-06-14T22:11:56.204077 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/administrate/application-6a75fccf481841c324aa19339808666fe7b4accb3b3a49b1d78d4bd627141d85.js.gz
       I, [2019-06-14T22:11:57.662101 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/administrate/application-a6f492d359a755552cc0b49e91d9c3d81da0931205a8e258db9baccf87530492.css
       I, [2019-06-14T22:11:57.662402 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/administrate/application-a6f492d359a755552cc0b49e91d9c3d81da0931205a8e258db9baccf87530492.css.gz
       I, [2019-06-14T22:11:57.662974 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/bootstrap/glyphicons-halflings-regular-f495f34e4f177cf0115af995bbbfeb3fcabc88502876e76fc51a4ab439bc8431.eot
       I, [2019-06-14T22:11:57.663459 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/bootstrap/glyphicons-halflings-regular-f495f34e4f177cf0115af995bbbfeb3fcabc88502876e76fc51a4ab439bc8431.eot.gz
       I, [2019-06-14T22:11:57.664581 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/bootstrap/glyphicons-halflings-regular-fc969dc1c6ff531abcf368089dcbaf5775133b0626ff56b52301a059fc0f9e1e.woff
       I, [2019-06-14T22:11:57.666790 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/bootstrap/glyphicons-halflings-regular-bd18efd3efd70fec8ad09611a20cdbf99440b2c1d40085c29be036f891d65358.ttf
       I, [2019-06-14T22:11:57.668160 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/bootstrap/glyphicons-halflings-regular-bd18efd3efd70fec8ad09611a20cdbf99440b2c1d40085c29be036f891d65358.ttf.gz
       I, [2019-06-14T22:11:57.669051 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/bootstrap/glyphicons-halflings-regular-d168d50a88c730b4e6830dc0da2a2b51dae4658a77d9619943c27b8ecfc19d1a.svg
       I, [2019-06-14T22:11:57.670751 #1442]  INFO -- : Writing /tmp/build_046481fee6a2bae4dd86efcd4a00ec22/public/assets/bootstrap/glyphicons-halflings-regular-d168d50a88c730b4e6830dc0da2a2b51dae4658a77d9619943c27b8ecfc19d1a.svg.gz
       Compiling…
       Compilation failed:
       
    !
    !     Precompiling assets failed.
    !
    !     Push rejected, failed to compile Ruby app.
    !     Push failed

Adding `config.assets.initialize_on_precompile = false` to `config/application.rb ` as recommended by [Heroku upload precompiling assets failed](https://stackoverflow.com/questions/19650621/heroku-upload-precompiling-assets-failed) did not solve the issue on Heroku.

Running `RAILS_ENV=production bundle exec rails webpacker:compile` to reproduce the bug locally also fails silently:

    yarn install v1.15.2
    [1/4] 🔍  Resolving packages...
    [2/4] 🚚  Fetching packages...
    [3/4] 🔗  Linking dependencies...
    warning " > webpack-dev-server@3.7.1" has unmet peer dependency "webpack@^4.0.0".
    warning "webpack-dev-server > webpack-dev-middleware@3.7.0" has unmet peer dependency "webpack@^4.0.0".
    [4/4] 🔨  Building fresh packages...
    ✨  Done in 2.77s.
    Compiling…
    Compilation failed:

Same problem when appending `--trace` for better visibility:

    RAILS_ENV=production bundle exec rake assets:precompile --trace

    ** Invoke assets:precompile (first_time)
    ** Invoke assets:environment (first_time)
    ** Execute assets:environment
    ** Invoke environment (first_time)
    ** Execute environment
    ** Invoke yarn:install (first_time)
    ** Execute yarn:install
    yarn install v1.15.2
    [1/4] 🔍  Resolving packages...
    success Already up-to-date.
    ✨  Done in 0.50s.
    ** Execute assets:precompile
    ** Invoke webpacker:compile (first_time)
    ** Invoke webpacker:verify_install (first_time)
    ** Invoke webpacker:check_node (first_time)
    ** Execute webpacker:check_node
    ** Invoke webpacker:check_yarn (first_time)
    ** Execute webpacker:check_yarn
    ** Invoke webpacker:check_binstubs (first_time)
    ** Execute webpacker:check_binstubs
    ** Execute webpacker:verify_install
    ** Invoke environment
    ** Execute webpacker:compile
    Compiling…
    Compilation failed:
    
Running this command sourced from a relevant Github [issue](https://github.com/rails/webpacker/issues/1824#issue-386603091) produces a useful stacktrace:
    
    NODE_ENV=production ./bin/webpack --progress --config config/webpack/production.js

Using the webpack binary produces verbose logs with errors:

    [0] Hash: 186ea18409c2ab12c66a186ea18409c2ab12c66a                                0 Version: webpack 4.33.0
    Child
    Hash: 186ea18409c2ab12c66a
    Time: 977ms
    Built at: 2019-06-15 00:57:10
     2 assets
    Entrypoint application = js/application-c9bf0cd458366c9b9f7c.js js/application-c9bf0cd458366c9b9f7c.js.map
    [0] ./app/javascript/packs/application.js 834 bytes {0} [built]
    [1] ./app/javascript/css/application.css 1.32 KiB {0} [built]
    [2] ./node_modules/css-loader/dist/cjs.js??ref--6-1!./node_modules/postcss-loader/src??ref--6-2!./app/javascript/css/application.css 1.47 KiB {0} [built] [failed] [1 error]
        + 2 hidden modules

    ERROR in ./app/javascript/css/application.css (./node_modules/css-loader/dist/cjs.js??ref--6-1!./node_modules/postcss-loader/src??ref--6-2!./app/javascript/css/application.css)
    Module build failed (from ./node_modules/postcss-loader/src/index.js):
    Error: Cannot find module 'tailwindcss'
        at Function.Module._resolveFilename (module.js:548:15)
        at Function.Module._load (module.js:475:25)
        at Module.require (module.js:597:17)
        ...

Webpacker can't find the `tailwindcss` module during asset pre-compilation.

## Cause
TailwindCSS was improperly configured. `package.json` did not contain tailwind as a dependency. It was only listed in `devDependencies`. This explains why the error wasn't being throw while developing locally.

    # package.json

    "dependencies": {
        "@rails/webpacker": "^4.0.7"
    },
    "devDependencies": {
        "tailwindcss": "^1.0.4",
        "webpack-dev-server": "^3.7.1"
    }
    
This bug may have been caused by mixing package managers (`npm` and then moving to `yarn`) at the instantiation of the project. 

## Solution
After removing and reinstalling `tailwindcss`, the assets compiled successfully locally and on Heroku.

1. Remove tailwindcss from `devDependencies`
        
        # package.json

        "dependencies": {
            "@rails/webpacker": "^4.0.7"
        },
        "devDependencies": {
            "tailwindcss": "^1.0.4", # Remove this line
            "webpack-dev-server": "^3.7.1"
        }
    
2. Add tailwindcss using yarn

        yarn add tailwindcss --save-dev

3. Verify tailwindcss is a dependency in `package.json`

    ```
    # package.json

    "dependencies": {
        "@rails/webpacker": "^4.0.7",
        "tailwindcss": "^1.0.4" # add to dependencies
    },
    "devDependencies": {
        "webpack-dev-server": "^3.7.1"
    }
    ```

4. Install dependencies

        yarn install

5. Verify assets precompile successfully
        
        RAILS_ENV=production bundle exec rake assets:precompile --trace

## Stack Overflow
- [Heroku Upload Precompiling Assets Failed](https://stackoverflow.com/questions/19650621/heroku-upload-precompiling-assets-failed)

## Github Issues
- [Compilation Failed without error message](https://github.com/rails/webpacker/issues/955)
- [Compiling in production fails silently and isn't verbose enough](https://github.com/rails/webpacker/issues/1824#issue-386603091)
