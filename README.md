ost(1)
======

Just an experiment for running daemonized Ost workers.

Usage
-----

Assuming a simple worker:

    require "app"

    Ost[:stuff].each do |item|
      # process item
    end

Place the worker at `./workers/stuff.rb` and then:

    $ ost start stuff

That should load the worker in the foreground.

You can daemonize the process by passing the `-d` flag:

    $ ost start -d stuff

If you daemonize, a file containing the daemonized process ID is written
to `./workers/stuff.pid`.

Given that `start` is the default action for running Ost workers it can
be omitted:

    $ ost -d stuff

You can kill a daemonized worker by issuing the `stop` command:

    $ ost kill stuff

This will send the `TERM` signal to the process.


Optionally, you can specify a different directory for the pid file.

    $ost -d stuff -p tmp
    
Will look for the pid file in `./tmp/` instead of the default `./workers/` directory. This is useful if you're using a deploy tool like Capistrano and need to place the pid files in a symlinked dir.


Support
-------

For now, this experiment is only tested on MRI 1.9.2+.
