---
layout: episode
title: Concepts and motivation for using modular coding
teaching: 20
exercises: 0
questions:
  - Know about pure functions (functions without side effects, functions which given same input always return same output)
  - Learn why and how to limit side effects of functions.
  - Discuss why and how to limit side effects of data. Also discuss when mutable data may be preferable.
objectives:
  - Discuss why single-purpose functions are often preferred over multi-purpose functions.
keypoints:
  - Understand the motivation for modular based coding
  - “Global data structures” vs “local data structures”.
---

## Motivation

- You are working in a big project where several persons have contributed at different times in the code development
- Someone has given you access to a repository online, you have developed some new functionalities and would like to contribute to the 'main' code by asking for a pull request or merge with master

- ... and you want to contribute to it.
- It is quite easy to make a copy and send a change back.
- First, we do this a relatively simple way: get repository, make a change
  locally, and send the change directly back.
- Then, we make a "pull request" that allows a review.
- Once we know how code review works, we will be able to propose changes
  to repositories of others and review changes submitted by external
  contributors.

---

## Presentation about modular code development


[Slides](https://cicero.xyz/v3/remark/0.14.0/github.com/coderefinery/modular-code-development/master/talk.md/#1) by Radovan Bast.
