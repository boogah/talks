footer: boogah.org/wcoc17
autoscale: true

# [fit] The Minimal Dev

# WordCamp OC 2017

# @boogah

[.hide-footer]

---

# So...
# dev environments

![](burn-it-all.gif)

^ I hope everyone in here is at least passingly familiar with the concept of a local development environment.

^ If you aren't, local dev environments involve a specialized software stack that runs on your laptop or desktop. This stack allows your computer to emulate a live site while still keeping your work private. Kind of like a staging site, but way less formal.

^ And because dev environments run locally, you don't have to worry about uploading any changes you make. You can dig right into your site's code with your favorite text editor and see your work as soon as you hit save.

^ Dev environments are handy when you want to test something out — such as a new plugin or theme — and can't afford to experiment on your production environment.

---

# [fit] Mamas, don't let your
# [fit] babies grow up to be
# [fit] cowboy coders

![](cowboy.gif)

^ Speaking of experimenting in production...

^ Don't.

^ Nobody can really _afford_ to experiment in production.

^ If your host provides a staging area, use it.

^ If you already use a dev environment, great.

---

# Dev environments

* Vagrant
* Docker
* DesktopServer
* Local
* Chassis
* MAMP
* WAMP

^ Since we just came back from lunch, let's get the blood flowing and move around a little bit.

^ I know I'm speaking to an audience of mostly developers, so I won't ask you to move around too much.

^ Show of hands, who has used at least one of these before?

^ Which one's your favorite?

^ What do you like about it?

^ What do you hate about it?

---

![](the-best.gif)

^ Today we're going to talk about my favorite dev environment...

---

# Valet

![](http://www.reactiongifs.com/wp-content/uploads/2013/10/joy-ride.gif)

^ Valet is a PHP development environment for, as the project site says, "minimalists". Originally developed for the Laravel PHP framework, Valet also supports other PHP projects, like WordPress, through the use of "drivers".

^ While the primary distribution of Valet is for macOS, there are unofficial ports for the Windows and Linux folks in the crowd. With that being said, I'm going to be focusing on the macOS version today. Hope that's not a deal breaker for anyone.

---

# Why Valet?

![](what.gif)

^ If you saw how cluttered the area around my desk is, you'd be pretty hard pressed to call me a minimalist. But when it comes to development environments, I run a pretty tight ship.

^ One of the most appealing things, to me, about Valet is how lightweight it is. The core components — which are installed through Homebrew and the Composer dependency manager — take up no more than a few hundred MB on my laptop. On top of that, Valet uses around 10MB of RAM while idle.

---

# [fit] Installing Valet

![](parking.gif)

---

# [boogah.org/inst-valet](https://boogah.org/inst-valet)

^ While I'd like to say that there's a package that installs all the prerequisites for Valet, the process is still pretty manual.

^ I've written up a list of commands you need to run to install the Homebrew package manager, PHP 7.0 with Xdebug, MySQL, the Composer dependency manager, and Valet.

[.hide-footer]

---

# Installing Valet (Homebrew)

``` [.highlight: 2,5,8,11]
# Install Xcode Command Line Tools
→ xcode-select --install

# Install Homebrew
→ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# Update Homebrew Package Index
→ brew update

# Confirm Homebrew is Installed Correctly
→ brew doctor
```

---

# Installing Valet (PHP 7)

``` [.highlight: 2,3,6,9]
# Install PHP 7.0
→ brew tap homebrew/php
→ brew install php70

# Install Xdebug (optional)
→ brew install php70-xdebug

# Confirm PHP is Installed Correctly
→ php -v
```

---

# Installing Valet (MySQL)

``` [.highlight: 2,5]
# Install MySQL
→ brew install mariadb

# Launch MySQL at Login
→ brew services start mariadb
```

---

# Installing Valet (Composer)

``` [.highlight: 2,5]
# Install Composer
→ brew install composer

# Confirm Composer is Installed Correctly
→ composer -V
```

---

# Installing Valet (Valet)

``` [.highlight: 2,5,8,9,10]
# Install Valet (Part 1)
→ composer global require laravel/valet

# Install Valet (Part 2)
→ valet install

# Create a Directory for Valet Sites
→ mkdir ~/sites/valet/
→ cd ~/sites/valet/
→ valet park
```

---

# [fit] Installing WP-CLI

![](typing.gif)

---

# Install WP-CLI

```
→ curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
→ php wp-cli.phar --info
→ chmod +x wp-cli.phar
→ sudo mv wp-cli.phar /usr/local/bin/wp
```

<sub>**From [wp-cli.org](https://wp-cli.org/)**</sub>

---

# Valet + WP-CLI

![](merge.gif)

---

# WP-CLI Valet commands

```
→ wp package install aaemnnosttv/wp-cli-valet-command
```

---

# [fit] Creating sites

![](hotdog.gif)

---

# Create a site

``` [.highlight: 1]
→ wp valet new modok --admin_user=modok --admin_password=advanced-idea-mechanics
Don't go anywhere, this should only take a second...
Success: modok ready! https://modok.dev
```

---

![inline](modok_dev.jpg)

---

# Destroy a site

``` [.highlight: 1]
→ wp valet destroy modok --yes
Success: modok was destroyed.
```

---

# [fit] Preserving workflows

![](work.gif)

---

# Supported workflows

* [Multisite](https://github.com/Objectivco/WordPressMultisiteSubdirectoryValetDriver)
* [WordPlate](https://github.com/wordplate/valet)
* [Skeleton](https://github.com/Baadier-Sydow/wordpress-skeleton-valet-driver)
* [Bedrock](https://github.com/aaemnnosttv/bedrock-valet-driver)

^ WordPlate = Built around Composer & Packagist

^ Skeleton = Mark Jaquith's simple git skeleton

^ Bedrock = Roots created boilerplate

---

# [fit] Showing off

![](show-off.gif)

---

# Showing off

``` [.highlight: 1,2,10]
→ cd ~/sites/valet/modok
→ valet share
ngrok by @inconshreveable                                       (Ctrl+C to quit)

Session Status                online
Version                       2.2.4
Region                        United States (us)
Web Interface                 http://127.0.0.1:4040
Forwarding                    http://bf40fa0e.ngrok.io -> modok.dev:443
Forwarding                    https://bf40fa0e.ngrok.io -> modok.dev:443

Connections                   ttl     opn     rt1     rt5     p50     p90
                              0       0       0.00    0.00    0.00    0.00
```

---

# [fit] Experimentation

![](science.gif)

---

# Installing Elasticsearch

```
→ brew install elasticsearch
```

---

![inline](modok_elasticpress.jpg)

---

# Maintaining Elasticsearch

```
→ brew pin elasticsearch
```

---

![inline](modok_elasticpress_error.jpg)

---

# [fit] Questions?

![](speechless.gif)
