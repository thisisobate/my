---
authors:
  - name: "Uchechukwu Obasi"
date: 2021-02-18
linktitle: My Pull Request Checklist.
type:
  - post
  - posts
title: My Pull Request Checklist.
weight: 1
categories:
  - version control
  - technical
  - open source
---

It's one thing to write code, it's another thing to get it merged to upstream. I've been creating a lot of pull request lately and I've beginning to notice some patterns to the code reviews I get all the time. I noticed that I make some mistakes which always comes up during code reviews and repeating them would make it a bad habit for me. Together, I and my manager decided to create a checklist that will allow me craft out a good pull request.

# Test locally and try to break it

The purpose of pull request is to merge local changes to upstream. I try to test my work to see if it actually works as expected in the application. After that, I try to break it to know if I covered the edge cases.

# Compare with similar code within the codebase (specially for syntax purposes)

This section is important most especially when I'm new to the codebase. It gives me an insight into what their coding style looks like and allows me to start contributing right away.

# Remove unnecessary comments or leftover code

I fall victim of this every single time. When creating a pull request, it's important you carefully scan through your changes and see if you have some unnecessary comments/leftover code. I've begin to notice that whenever I do this, it makes life easy for the code reviewer and it gives the impression that I'm attentive to detail which is one of the qualities of an effective software engineer.

# Tests are updated- Make sure they are passing

Always remember to update tests before pushing any changes upstream. This can never be overemphasized.

# Try not to force push once code review started.

I used to force push my changes all the time. I began to notice that force pushing to a branch/PR that has lot's of conversations going on actually rewrites the commit history thus making it difficult for me or anyone else to track the referenced code in the discussion thread. This is never a good thing. Remember, the goal is to make the review process alot more easier for the reviewer which in turn leads to quick PR approvals.

# Double check variables- good naming is key

Naming is hard. Good naming takes alot of time and effort but trust me, it's worth the extra stress.

# Implement the DRY principle- abstract, compose, and reuse code as much as possible

For me, I think this is one of the most important things I try to implement when writing code. It makes my code alot more readable and overall, it improves the look and feel of the codebase. I know for sure making this a daily habit would help me become an efficient software engineer.

Thanks for reading!
