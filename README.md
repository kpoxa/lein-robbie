# lein-robbie

> Robbie nodded his head - a small parallelepiped with rounded edges and
> corners attached to a similar but much larger parallelepiped that
> served as a torso by means of a short, flexible stalk - and obediently
> faced the tree. A thin metal film descended over his glowing eyes, and
> from within his body came a steady, resonant ticking.
> "Don't peek now - and don't skip any numbers," warned Gloria, and
> scurried for cover.

> With unvarying regularity seconds were ticked off, and at the
> hundredth, up went the eyelids and the glowing red of Robbie's eyes
> swept the prospect.

> --From Robbie, by Isaac Asimov. 
> Published by Fictioneers, Inc. in 1940

`lein-robbie` is a
[leiningen][1] plugin for
creating Android apps built using phonegap and clojurescript.

## Usage

Put `[lein-robbie "0.1.0-SNAPSHOT"]` into the `:plugins` vector of your
`:user` profile, or if you are on Leiningen 1.x do `lein plugin install
lein-robbie 0.1.0-SNAPSHOT`.

Before using Robbie, you need to have the Android SDK installed and
you will probably want to create an AVD (Android Virtual Device, like
a VM image for the emulator) using the `android` tool.

Once you've got all the prerequisites installed, here's the basic workflow:

    $ lein new robbie my-app
    Copying ...
    Generating ...
    
    $ lein cljsbuild once
    ...
    
    $ android &
    # create your AVD if neccesary
    # start the AVD
    
    $ ant debug install
    ...
    
    # verify you can see 'my_app' in the apps screen in the emulator
    # launch your app
    
    # hack, hack, hack
    
    $ lein cljsbuild once && ant debug install
    
    # goto 'launch your app'
    
It's also possible to specify which version of Android you wish to
target:

    $ lein new robbie myapp target android-10
    
You can always change this later in the generated AndroidManifest.xml
file in your project.

You can also tell robbie you'd like to include a javascript framework
with the project. Currently only [jQuery Mobile 1.0][2] and
[jQuery Mobile 1.1 RC1][3] are supported:

    $ lein new robbie myapp target android-10 framework jquery-mobile-1.0

or

    $ lein new robbie myapp target android-10 framework jquery-mobile-1.1

## TODO

* I'd like to override `lein install` to compile cljs and do `ant
  debug install`. My understanding is that I can just make a new
  `leiningen/install` function and it will override the default one as
  long
  [as it's newer than the leiningen built-in install task][4].
* Maybe it would be better to use a hook? (as in, robert)
* Add some subtasks for other android stuff, like release compiles,
  catting/tailing the adb log, so I don't have to remember how to use
  the android tools to do this and so the cljsbuild happens whenever
  it needs to, instead of having a separate step.
* Add example apps
* Longer term: make an iOS and possibly other platform version if
  this.

## License

Copyright © 2012 Chris Bilson

Distributed under the Eclipse Public License, the same as Clojure.

The phonegap portions are distributed under the Apache 2.0 license, as
described in `LICENSE.phonegap`.

[1]: https://github.com/technomancy/leiningen "Leiningen on Github"
[2]: http://jquerymobile.com/demos/1.0.1/ "jQuery Mobile 1.0 Docs"
[3]: http://jquerymobile.com/demos/1.1.0-rc.1/ "jQuery Mobile 1.1 RC1 Docs"
[4]: https://github.com/technomancy/leiningen/issues/415
