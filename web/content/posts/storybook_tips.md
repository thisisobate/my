---
authors:
  - name: "Uchechukwu Obasi"
date: 2021-03-22
linktitle: "5 Things To Look Out For When Creating Stories Using Storybook"
type:
  - post
  - posts
title: "5 Things To Look Out For When Creating Stories Using Storybook"
weight: 1
categories:
  - Storybook
  - Technical
images:
  - "/images/blog/storybook_logo.png"
featuredImage: "/images/blog/storybook_logo.png"
---

In this blogpost, I will be sharing some things you should know about Storybook, how to avoid some of the mistakes I made while creating stories, and of course, my solutions to these problems.

According to the [Storybook documentation](https://storybook.js.org/) website, Storybook is an open source tool for developing UI components in isolation for React, Vue, Angular, and more. It makes building stunning UIs organized and efficient. For me, I think Storybook is basically a tool that is used mainly by organizations to create a design system alongside with documentation. It allows teams to play around with the component UI without thinking about the business logic.

In my own case, I have only used Storybook for React and Typescript components and so, this article will only reference React Storybook.

# Storybook knobs are going into extinction.

If you or your team is already using Knobs, I would recommend migrating to Controls instead. Storybook Controls is an addon introduced in storybook v6.0. They are similar to knobs but have alot more capabilites such as: automatic Control generation, No dependency on Storybook-specific APIs, live edit components, and a host of others. From my experience, using Controls has made me write less code which has greatly improved the readability of my component stories.

# ReactNode types doesn't correspond to text.

In Storybook, component props that are set to React.ReactNode correspond to a textbox in the Controls pane. The weird thing I always notice is that text input must be enclosed in quotation marks. This is not good because users would tend to forget about the quotation marks which often lead to errors. My approach towards solving this problem is to always explicitly set these props argtype to text.

# Some component props doesn't enable full control of the component Story.

Oftentimes, component props are assigned types that are not strings, numbers, or booleans. In scenarios where a prop is assigned a different type like object or function types, it's a bit tricky to play around with such Control. It makes no sense to have an object or function as a Control type becasue it's going to be difficult for non-engineers to interact with that Control. My solution is basically creating a new interface while extending from the original component interface. This gives me the opportunity to create new props with my desired types, and alot more flexibility to tweak and play around with the component story.

# Component props are automatically generated as Controls on Storybook.

This could lead to unwanted Controls cluttered on the Control pane on Storybook. You can solve this by completely disabling these unwanted Controls. You can learn more about Controls on the [Storybook documentation](https://storybook.js.org/docs/react/essentials/controls/) website.

# Using the Select argtype without providing it's options might break your story.

Recently, I tried setting the argtype of a specific Control that has a list of options to the Select Control type. I forgot to provide the Select argtype with an array of options and as a result, Storybook broke down. Always remember to provide options to both Select and Radio argtypes.

Thanks for Reading!
