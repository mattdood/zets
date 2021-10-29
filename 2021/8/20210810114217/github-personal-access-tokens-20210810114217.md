---
path: '/2021/8/github-personal-access-tokens-20210810114217'
title: 'github personal access tokens'
date: '20210810114217'
category: 'git'
tags: ['2FA', 'github']
---

# github personal access tokens
I was recently working on a project for a client that did not allow me to `git pull`
out of nowhere. This repository has been something I've interfaced with quite
a bit and it was now suddenly saying that I did not have permission to do the
pull for a specific directory in the project.

When doing a `sudo git pull` I was confronted with a login that wouldn't properly
authenticate my credentials with my correctly input password.

After some searching I found [this StackOverflow article](https://stackoverflow.com/a/34919582/12387496)
that stated if I had either 2FA or a "personal access token" I would have to
input that rather than the password to my account. The CLI wasn't stating this directly.

I actually had both of these set up; however, I found that the "personal access
token" overrides the 2FA and it won't accept one or the other.

