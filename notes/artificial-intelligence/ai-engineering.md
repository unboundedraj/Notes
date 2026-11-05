---
title: AI Engineering
date: 2026-11-05
tags: [ai, artificial intelligence]
---

## What is AI Engineering?

**AI engineering is building products on top of a language model that someone else trained. You reach the model through an API, the same way you would call a payments or maps service. Your job is to shape what goes into it, check what comes out, and turn that into something people can rely on.**

## What the work looks like

**Take a realistic task: summarize a meeting transcript into decisions, owners, and action items.**

**The first version is one prompt, and it mostly works. Then the problems show up. Some summaries list an action item with no owner. Some mention a decision that nobody made. As people report issues, the prompt grows into a long list of special cases, and each fix breaks something else.**

**So you split the job. One call pulls out the decisions and action items. A second checks each one against the transcript. A third writes the summary. You add a simple test that every action item has an owner, and a check that each decision appears in the transcript. Then you try smaller, cheaper models and keep the smallest one that still passes your tests.**

**None of that was training. It was writing prompts, writing code around them, reading real outputs, and turning each failure you found into a test. That loop is most of the week:**

- **Shape the input. Instructions, examples, and the right documents for this request.**
- **Check the output. Tests for format, facts, and tone, run on real examples.**
- **Watch cost and speed. Everything the model reads or writes is billed, and longer answers take longer to arrive.**
- **Design around mistakes. Models are sometimes confidently wrong, so good products make an answer easy to verify or correct.**

## What you need to start

**You need solid programming, the habit of reading your own data, and curiosity about why an output went wrong. You do not need the math of neural networks to begin.**

**The math does start to matter as you go further. When an answer is slow, expensive, or strange, knowing what happens inside the model tells you what to try.**
