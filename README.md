# FSEvents Tools

Command-line tools and scripts that use OS X's [FSEvents](http://en.wikipedia.org/wiki/FSEvents) API. Mostly useful for watching a directory and react to changes in it.


## Building

In addition to the typical automake/autoconf/make, you'll need pkg-config. `brew install pkg-config` should do the trick.

Once you have all the dependencies, just run `./autogen.sh` and `make install`.


## Usage examples

Alert if any files in a directory are changed.

    notifywait /path/; echo "\007"

Automatically rsync files to a remote server if any of them are changed.

    auto_rsync . 192.168.1.127:/var/www

Same as above, but don't copy .pyc files.

    notify_loop ~/code/directory rsync -avz --exclude="*.pyc" ~/code/directory/ server.example.com:/stuff/

By default, the process will terminate upon "the event" "transpiring".. Use your preferred looping paradigm to alter this behavior..

    watchout(){ notifywait ~/.thereitis; say "there she went" && watchout; }; watchout > /dev/null

## Related software

* [inotify-tools](https://github.com/rvoicilas/inotify-tools). The original tools that inspired me to make fsevents-tools.
* [Lsyncd](https://github.com/axkibe/lsyncd). A service to keep files synced between a master and one or more slave servers.
