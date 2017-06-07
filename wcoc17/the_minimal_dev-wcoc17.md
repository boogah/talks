footer: boogah.org/wcoc17

# [fit] The Minimal Dev

# WordCamp OC 2017

# @boogah

[.hide-footer]

---

# [fit] What is Valet?

![](mike-wilson-36140.jpg)

---

# [fit] Why Valet?

![](mike-wilson-36140.jpg)

---

# [fit] Why not Vagrant?

![](martin-sanchez-zekedrone-250745.jpg)

---

# [fit] Why not Docker?

![](chuttersnap-255216.jpg)

---

# [fit] Why not X?

![](wesson-wang-110739.jpg)

---

# [fit] Installing Valet

![](mike-wilson-36140.jpg)

---

# [fit] Installing WP-CLI

![](pete-wright-105201.jpg)

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

# Install WP-CLI Valet commands

```
→ wp package install aaemnnosttv/wp-cli-valet-command
```

---

# [fit] Creating sites

![](marco-djallo-127113.jpg)

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

![](markus-spiske-207946.jpg)

---

# Supported workflows

* [Multisite](https://github.com/Objectivco/WordPressMultisiteSubdirectoryValetDriver)
* [WordPlate](https://github.com/wordplate/valet)
* [Skeleton](https://github.com/Baadier-Sydow/wordpress-skeleton-valet-driver)
* [Bedrock](https://github.com/aaemnnosttv/bedrock-valet-driver)

---

# [fit] Showing off

![](raphael-koh-126192.jpg)

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

# [fit] Exploration

![](himesh-kumar-behera-216019.jpg)

---

# Installing Elasticsearch

``` [.highlight: 1]
→ brew install elasticsearch
```

---

![inline](modok_elasticpress.jpg)

---

# [fit] Questions?

![](edwin-andrade-158050.jpg)
