---
layout: post
title:  "Export multiples kubeconfigs"
---

Add all your kubeconfigs in a disarable directory, in my case is: `~/Documents/kubeconfigs/` and add to your `~/.bash_profile`: `export KUBECONFIG=$(/usr/bin/realpath ~/Documents/kubeconfigs/* | tr '\n' ':'| sed 's,\:$,,g')`

Also is highly recommended to use `kubectx` to make the context change easier.
