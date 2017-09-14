text: #333333
code: Fira Code Retina, #111111
background-color: #FFA3D7

# [fit] The
# [fit] Minimal
# [fit] Dev

^ Okay. Let's talk about development environments.

---

# [fit] Who should
# [fit] use a development
# [fit] environment?

---

# [fit] A brief history
# [fit] of PHP development
# [fit] environments

---

# [fit] MAMP
# [fit] and/or
# [fit] WAMP

^ Some people may have been doing local PHP development before this, but MAMP and WAMP is where a lot of folks cut their teeth. MAMP and WAMP gives you just what you need to do WordPress development — Apache, MySQL, and PHP — and wraps it up in a no frills user interface.

^ Over the past few years these tools have added Nginx, Python, and Perl to their package. Which is nice, but two out of three of those things probably don't matter to most of you.

^ Besides, if you use either of these tools to do local development, you have to spin up each new WordPress site you work on manually. If you're used to doing that already, that's probably not a big deal. But if you've only used one-click installers to get WordPress set up, you may be in for a bit of a learning experience.

---

# [fit] Vagrant

^ A few years ago, Vagrant took over as the default way for serious developers to work. The appeal here was that Vagrant allowed you to emulate the server that you were deploying to.

^ Despite everyone excitedly saying "I can develop on a local copy of my production server", many people didn't actually do that. But that didn't stop Vagrant from becoming a popular developer tool.

^ If I had to think of Vagrant solutions built specifically for WordPress off the top of my head, I'd say: VVV, Chassis, VCCW, HGV, and Primary Vagrant. And I know I'm missing at least half a dozen others.

^ The problem with Vagrant is that it has a tendency to fall apart at the worst possible times.

---

# [fit] Docker

^ Docker is currently the new hotness. Like Vagrant, you can emulate the server you're deploying to. Better yet, if your production server is running Docker, you can run the exact same containers locally as you do in production as Docker containers are built to run on any infrastructure.

^ And, since it was written to be a lightweight, Docker uses *way* less RAM and CPU than Vagrant. Which is always nice.

^ Unlike Vagrant, and MAMP / WAMP however Docker can be a fairly advanced concept for even seasoned developers to wrap their heads around. While you can use stuff like Elasticsearch by adding the appropriate container to your config, actually adding and troubleshooting containers can be a pain if you're not already familiar with Docker.

---

# [fit] Local

^ Local, by Flywheel, is basically a nice GUI on top of Docker. But that nice GUI makes a massive difference. You're never more than a few mouse clicks away from a brand new WordPress install. And with "Blueprints", you can have ready made sites with your favorite plugins and themes already in place.

^ Local can be configured to use any version of PHP from 5.2.x to 7.1.x, which is nice if you've inherited a legacy environment or need to troubleshoot how something will perform on newer (or older) PHP.

---

# [fit] Valet

^ Valet is a PHP development environment for, as the project site says, "minimalists". It's also what I'm going to be spending most of my time on.

^ Originally developed for the Laravel PHP framework, Valet also supports other PHP projects, like WordPress, through the use of "drivers".

^ While the primary distribution of Valet is for macOS, there are unofficial ports for the Windows and Linux folks in the crowd.

^ If you saw how cluttered the area around my desk is, you'd be pretty hard pressed to call me a minimalist. But when it comes to development environments, I run a pretty tight ship.

---

# [fit] Valet
# [fit] is bae

^ So why do I love Valet so much?

^ One of the most appealing things, to me, about Valet is how lightweight it is. The core components — which are installed through Homebrew and the Composer dependency manager — take up no more than a couple hundred MB on my laptop. On top of that, Valet uses around 10MB of RAM while idle.

^ Even though Docker (and, in turn, Local) was created to be lightweight, the fact that Valet is leaner — and always running — means I can have a scratchpad site up inside of 15 seconds with one WP-CLI command.

---

```
→ wp valet new tacos --admin_user=boogah
    --admin_password=queso-pastor-harina
```

![inline](taco.png)

---

# [fit] Installing Valet

## `https://goo.gl/VtBKPq`

![right inline](install-valet-qr.png)

^ If you're comfortable with the command line, installing Valet is easy_ish_. Just 23 quick commands and you're all set.

^ Okay. By no stretch of the imagination should 23 commands ever be considered "quick".

^ Honestly, I wish I could find the time to make an installer for Homebrew, PHP, MySQL, Composer, Valet, and WP-CLI that doesn't stomp on stuff like Homebrew and Composer if they're already installed. It's not hard, I just have other priorities.

^ If someone who has some spare cycles wants to whip up a shell script (or Electron app) based on what I've linked above, I'll gladly share it.

---

# [fit] Fun
# [fit] with
# [fit] Valet

^ Now that you've got Valet installed, here's some useful stuff you can do with it...

---

# [fit] Share Your Site

```
→ cd ~/sites/valet/tacos
→ valet share
```

^ Typing `valet share` from your site's root directory tunnels your local site through an application called *ngrok*. ngrok allows anyone with the automagically generated URL to visit the site as long as its service is running.

^ This is handy if you want to show a client something you've been working on. Or if you need to run a web based application against your site.

^ I found ngrok to be helpful while I was working through some site optimizations for a client. They couldn't get me access to staging in their corporate environment, but still needed help badly. Using a local copy of their site, I was able to repeatedly run WebPagetest against my changes and get an idea of how they'd help before having to get their web team involved.

---

# [fit] Play with Elasticsearch

```
→ brew tap caskroom/cask
→ brew cask install java
→ brew install elasticsearch
→ brew pin elasticsearch
```

## `http://localhost:9200`

^ Remember how I said that installing Elasticsearch in Docker was kind of a hassle? Installing it under Valet is a relative breeze.

^ Elasticsearch with the ElasticPress plugin is a performant replacement for WordPress search as well as WP_Query. Additionally, there are extensions for ElasticPress that can help speed up WooCommerce, provide related posts with minimal overhead, and index DOC & PDF files.

^ If your host doesn't offer Elasticsearch, there's 3rd party services like Bonsai that sell affordable Elasticsearch server access. But if you'd like to try before you buy, here's your chance.

^ Unfortunately, using Elasticsearch means installing Java on your machine. Because of the number of security issues that target Java, it's a good idea to either keep on top of Java updates religiously or uninstall Java and Elasticsearch as soon as you're done with it.

---

# [fit] Play with Redis

```
→ brew install redis
→ brew services start redis
→ brew install php70-redis
```

## `tcp://localhost:6379`

^ Let's go one level deeper and mess around with Redis.

^ Redis is a "key value store" that, in the case of WordPress, can act as a more performant caching layer for dynamic content. Redis, when coupled with a plugin like WP Redis from Pantheon, holds onto WordPress database queries in its store temporarily, which decreases the amount of queries your WordPress install needs to make to the normally much slower MySQL service.

^ A number of Managed WordPress hosts already offer Redis for their customers, and its adoption rate is only growing. So why not see what it can do for you locally before trying it in production?

^ Under Valet, all you need to do is install one service and the appropriate PHP extension to get the service running locally.

---

# [fit] If all of this
# [fit] command line stuff
# [fit] freaks you out...

^ By all means, use Local instead of Valet. I've been using Local on my work machine since I started at Liquid Web — about 2.5 months ago — and it's actually really nice.

^ Occasionally, it can be a drag when I have to wait a minute for the Docker host machine that Local uses to start up. But being able to pick the PHP version I want to target has been worth the trade off there.

^ Now, just because I use Local at work doesn't mean that I use it full time. I wouldn't spend 30 minutes trying to sell you on Valet if I didn't still use it. I mean, Valet is still what I use on my personal machine. Different tools for different situations, you know?

---

# [fit] But
# [fit] what
# [fit] about...

^ DesktopServer? XAMPP? Some other tool that is amazing and I managed to completely ignore?

^ If you're wondering why I didn't talk about your favorite tool, you're probably already using it. And if you're already using something you like, I'm going to tell you something that might seem counterintuitive to my goal of selling you on Valet... Keep using what you like.

^ There's no need to upset your proverbial apple cart to try something you heard a guy on a stage nerd out about. But if you're fed up with what you're using, or you aren't using anything at all, consider giving Valet (or Local) a try.

---

# [fit] Questions?
