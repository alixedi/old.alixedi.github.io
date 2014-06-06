---
layout: post
title: Kill the rat
date: '2014-06-05T01:08:14+05:00'
tags:
- vim
- linux
tumblr_url: http://alixedi.tumblr.com/post/87807743131/kill-the-rat
---
To replace a text with another for every file in a directory:

grep -rl ''ST2'' ./ | xargs sed -i ''s/ST2/Vim/g''
