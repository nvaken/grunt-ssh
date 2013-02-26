# grunt-ssh

> SSH tasks for Grunt.

## Overview

This plugin requires Grunt `~0.4.0`

This library provides two Grunt tasks for ssh:

* _sftp_
* _sshexec_

*This plugin was designed to work with Grunt 0.4.x. If you're still using grunt v0.3.x it's strongly recommended that [you upgrade](http://gruntjs.com/upgrading-from-0.3-to-0.4), but in case you can't please use [v0.1.0](https://github.com/andrewrjones/grunt-ssh/tree/v0.1.0).*

## Synopsys

```js
// don't keep passwords in source control
secret: grunt.file.readJSON('secret.json'),
sftp: {
  test: {
    files: {
      "./": "*json"
    },
    options: {
      path: '/tmp/',
      host: '<%= secret.host %>',
      username: '<%= secret.username %>',
      password: '<%= secret.password %>'
    }
  }
},
sshexec: {
  test: {
    command: 'uptime',
    options: {
      host: '<%= secret.host %>',
      username: '<%= secret.username %>',
      password: '<%= secret.password %>'
    }
  }
}
```

## Description

### sftp

Copies one or more files to a remote server over ssh.

Inside your `grunt.js` file add a section named `sftp`.

#### Parameters

##### files ```object```

The files to copy. Should contain key:value pairs.

##### options ```object```

###### path ```string```

The path on the remote server. Defaults to home.

###### minimatch ```object```

Options for [minimatch](https://github.com/isaacs/minimatch).

###### username ```string```

The username to authenticate as on remote system.

###### password ```string```

The password to authenticate on remote system.

###### host ```string```

The remote host to copy to, set up in your `~/.ssh/config`.

###### port ```number```

The remote port, optional, defaults to `22`.

###### srcBasePath ```string```

Optionally strip off an initial part of the file when performing the SFTP operation. This is a string operation, so trailing slashes are important.

For example:

```js
    /* [...] */
    files: {
      "./": "dist/**"
    },
    options: {
      path: '/tmp/',
      /* [...] */
      srcBasePath: "dist/"
```

Would SFTP the files in dist directly into tmp (eg. ```dist/index.html``` ==> ```/tmp/index.html```)

###### createDirectories ```boolean```

Optionally check whether the directories files will be sftp'd to exist first. This can take a bit of extra time as directories need to be checked, so this option is disabled by default.

See also the ```directoryPermissions``` option.

###### directoryPermissions ```number```

The permissions to apply to directories created with createDirectories.  The default is 0755.  JSHint will probably yell at you unless you set this using ```parseInt```:

```js
directoryPermissions: parseInt(755, 8)
```

### sshexec

Runs a command over ssh.

Inside your `grunt.js` file add a section named `sshexec`.

#### Parameters

##### command ```string```

The command to run.

##### options ```object```

###### username ```string```

The username to authenticate as on remote system.

###### password ```string```

The password to authenticate on remote system.

###### host ```string```

The remote host to copy to, set up in your `~/.ssh/config`.

###### port ```number```

The remote port, optional, defaults to `22`.

### Release History
* 2013/02/20 - v0.2.0 - Update for grunt 0.4.x.
* 2013/02/13 - v0.1.0 - Initial release with _sshexec_ and _sftp_ tasks.

### License
Copyright (c) 2013 Andrew Jones
Licensed under the MIT license.
