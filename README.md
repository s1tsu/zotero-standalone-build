# Zotero Standalone build utility for FreeBSD
I have modified several scripts to build Zotero standalone on FreeBSD.
I am using the build. It works well for me but not fully tested.

## Environment

  - FreeBSD 11.2-RELEASE

## Prerequisites

### bash

``` example
# ln -s /usr/local/bin/bash /bin/bash
```

### Linux binary compatibility ( `linux_base-c7` )

The PDF tools are bundled with Zotero since Zotero 5.0.36. 
The bundled linux binaries seem to work well via Linux binary compatibility.

### Firefox ESR package ( `firefox-esr-52.9.0` )

We assume that the package `firefox-esr-52.9.0*.txz` is located at `/usr/ports/packages/All/`.

I build the package as follows.

``` example
> svnlite checkout https://svn.freebsd.org/ports/branches/2018Q2/www/firefox-esr SOMEWHERE/ports/www/firefox-esr
> svnlite checkout https://svn.freebsd.org/ports/branches/2018Q2/www/firefox SOMEWHERE/ports/www/firefox
> cd SOMEWHERE/ports/www/firefox-esr
> sudo make build
> sudo make package-noinstall
```

If one use the existing binary package, 
then one may have to take care of versions of some libraries such as libicui18n, libicuuc, and libvpx.

## Building

Follow the instructions on the [Zotero wiki](https://www.zotero.org/support/dev/client_coding/building_the_standalone_client) with the following changes.

### Step 1.

Use this repository instead of `github.com/zotero/zotero-standalone-build`.

``` example
> git clone --recursive https://github.com/s1tsu/zotero-standalone-build.git
```

Ensure that the current branch is `freebsd`.

OR apply the patch ( `freebsd.patch` ) to the original repo.

### Step 3.

In my case, I have to clean up `build/` ( `rm -r build/*` ) before running `npm run build` .

### Step 5.

Use the option `-p f`.

``` example
> ./fetch_xulrunner.sh -p f
```
