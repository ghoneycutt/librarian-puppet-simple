# librarian-puppet-simple

This project was created out of my frustration with dependency management in librarian-puppet, some people need external dependencies, I just need to be able to pin revisions for a collection of modules, and I found the dependency managment features of librarian-puppet too heavy for my simple use case.

This project just has fewer commands, but they should be compatible with the original librarian-puppet:

### Clean
Remove the directory where the modules will be installed, by default it will use `./modules` but you can override it by passing a `--path` option.
```
  librarian-puppet clean [--verbose] [--path]
```

### Install
Iterates through your Puppetfile and installs git sources. Use the `--clean` option to remove the directory and the `--path` option to override the default `./modules`.
```
  librarian-puppet install [--verbose] [--clean] [--path]
```

## Puppetfile
The processed Puppetfile may contain two different types of modules, `git` and `tarball`. The `git` option accepts an optional `ref` parameter.

The module names can be namespaced, but the created directory will only contain the last part of the name. For example, a module named `puppetlabs/ntp` will generate a directory `ntp`, and so will a module simply named `ntp`.

Here's an example of a valid Puppetfile showcasing all valid options:

```
mod "puppetlabs/ntp",
    :git => "git://github.com/puppetlabs/puppetlabs-ntp.git",
    :ref => "99bae40f225db0dd052efbf1d4078a21f0333331"

mod "apache",
    :tarball => "http://apache.mirror.iweb.ca//httpd/httpd-2.4.4.tar.gz"
```

## License

See [LICENSE](/LICENSE)

## Credits
The untar and ungzip methods came from https://gist.github.com/sinisterchipmunk/1335041