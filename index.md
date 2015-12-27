---
layout: default
title: VCCW - A WordPress development environment.
og_url: http://vccw.cc/
og_image: http://vccw.cc/images/ogp.png
description: VCCW is a Vagrant based development environment for WordPress plugins, themes, or websites.
---

# Vagrant + Chef + WordPress

This is a [Vagrant](http://www.vagrantup.com/) configuration designed for development of WordPress plugins, themes, or websites.

VCCW includes customizable variables for setting the WordPress version (or beta release), language, hostname, subdirectory, admin credentials, default plugins, default theme, multisite, SSL and other options. These variables give you a lot of flexibility in tailoring your development environment to your specific needs.

<ul id="navmenu"></ul>

## What's Installed

* CentOS 6.5
    * Subversion
    * Git
    * jq
* WordPress latest
    * [WP-CLI](http://wp-cli.org/)
    * [WordPress i18n Tools](https://codex.wordpress.org/I18n_for_WordPress_Developers)
    * [WordPress Coding Standards for PHP_CodeSniffer](https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards)
* PHP 5.4
    * [PHPUnit](https://phpunit.de/)
    * [Composer](https://getcomposer.org/)
    * [phpenv](https://github.com/CHH/phpenv)
    * [php-build](https://github.com/php-build/php-build)
* MySQL 5.5
* Apache
* Node.js
    * [grunt, grunt-cli, grunt-init](http://gruntjs.com/)
    * [gulp](http://gulpjs.com/)
* Ruby 2.1
    * [Bundler](http://bundler.io/)
    * [Wordmove](https://github.com/welaika/wordmove)
    * [Sass](http://sass-lang.com/)
    * [MailCatcher](http://mailcatcher.me/)

<ul id="navmenu"></ul>

## Requires

* Vagrant 1.5 or later
* VirtualBox 4.3 or later

{{ site.scroll_to_top }}

## Getting Started

### 1. Install VirtualBox.

[https://www.virtualbox.org/](https://www.virtualbox.org/)

### 2. Install Vagrant.

[http://www.vagrantup.com/](http://www.vagrantup.com/)

### 3. Install the vagrant-hostsupdater plugin. (Optional)

```
$ vagrant plugin install vagrant-hostsupdater
```

Windows does not allow to change `hosts` files. Please add `vccw.dev 192.168.33.10` by yourself!

### 4. Download vagrant box

```
$ vagrant box add miya0001/vccw
```

### 5. Please download <a class="latest-zipball">.zip</a> or <a class="latest-tarball">.tar.gz</a>.

<p><a class="button latest-zipball"><small>Download</small>.zip</a></p>

### 6. Change into a new directory.

```
$ cd vccw-x.x.x
```

### 7. Start a Vagrant environment.

```
$ vagrant up
```

### 8. Visit WordPress on the Vagrant in your browser

Visit [http://vccw.dev/](http://vccw.dev/) or [http://192.168.33.10/](http://192.168.33.10/)

{{ site.scroll_to_top }}

## Environments

### WordPress

This tool installs a WordPress environment with these settings by default.

* Default user
     * Username: `admin`
     * Password: `admin`

### Database

* MySQL Host: `127.0.0.1`
* Username: `wordpress` or `root`
* Password: `wordpress`
* Port: `3306`

### SSH

 * Host: 127.0.0.1
 * Username: vagrant
 * Password: vagrant
 * Port: 2222

{{ site.scroll_to_top }}

## Customizing

VCCW is configured for those developing WordPress plugins, themes or websites. It includes many customizable variables for setting the WordPress version (or beta release), language, hostname, subdirectory, admin credentials, default plugins, default theme, multisite, SSL and other options. These variables give you a lot of flexibility in tailoring your development environment to your specific needs.

Copy `provision/default.yml` to `site.yml` like following.

```
$ cp provision/default.yml site.yml
```

Then edit the `site.yml` and run `vagrant up`.

Or place the `site.yml` and put variables like following.

```
hostname: example.com
lang: ja
plugins:
  - contact-form-7
  - jetpack
```

Then just run `vagrant up`.

### Change PHP version

Put php version to `site.yml` like following.

```
php_version: 5.6.9
```

Then run `vagrant up` or `vagrant provision`.

See [https://github.com/php-build/php-build/tree/master/share/php-build/definitions](https://github.com/php-build/php-build/tree/master/share/php-build/definitions).

### Global configuration

VCCW has a series of global parameters which work with all virtual machines.

They can be specified `~/.vccw/config.yml` like following.

```
memory: 1024
cpus: 2
lang: ja
theme_unit_test: true
```

### Customizable variables

See [provision/default.yml](https://github.com/vccw-team/vccw/blob/master/provision/default.yml).

{{ site.scroll_to_top }}

## Run pre/post provisioning scripts

You can place shell scripts, so it will run at pre/post provisioning.

* `provision-pre.sh` - Run before chef provisioning.
* `provision-post.sh` - Run after chef provisioning.

### Example shell script.

`provision-post.sh` - It will run after provisioning.

```
#!/usr/bin/env bash

set -ex

/usr/local/bin/wp --path=/var/www/wordpress plugin install contact-form-7 --activate
```

This example script will install and activate plugin "Contact Form 7" by WP-CLI.

{{ site.scroll_to_top }}

## Checking Email with MailCatcher

[MailCathcer](http://mailcatcher.me/) re-routes all WordPress emails to Mailcatcher.

### How to use

Run following command.

```
$ curl -L https://raw.githubusercontent.com/vccw-team/activate-mailcatcher/master/setup.sh | bash
```

Then visit [http://vccw.dev:1080/](http://vccw.dev:1080/).

![](https://www.evernote.com/l/ABUEyE7-DsdNU7Dt80RiWHxyRXyd_8JZ6zEB/image.png)

{{ site.scroll_to_top }}

## Changelog

[https://github.com/vccw-team/vccw/releases](https://github.com/vccw-team/vccw/releases)

{{ site.scroll_to_top }}
