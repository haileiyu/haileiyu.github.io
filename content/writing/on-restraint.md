---
title: "On Restraint"
date: 2026-07-25
---

This is a sample post. Delete it and write your own.

To add a new one, create a file at `content/writing/my-post.md` with the same
front matter block at the top — a title and a date is all that is required.
Everything below the second `---` is [Markdown](https://commonmark.org/help/).

Regular paragraphs, **bold**, *italic*, and [links](https://example.com) all
work as you would expect. Lists too:

- One
- Two
- Three

> Block quotes sit in a slightly grey, slightly indented column.

If a post needs a picture, make it a folder instead of a single file:
`content/writing/my-post/index.md`, with the image sitting next to it. Then
call it by name and Hugo does the resizing at build time:

```
{{</* img src="photo.jpg" caption="Somewhere, 2026" */>}}
```

A post saved with a future date will not be published until that date arrives.
A post with `draft: true` in its front matter stays hidden until you remove it.
