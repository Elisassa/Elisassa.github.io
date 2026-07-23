---
title: "Name your SharePoint columns right the first time"
category: sharepoint
lede: SharePoint keeps two names for every column, and one of them is permanent. Knowing this earlier would have saved me real time.
---

Here's something basic that nobody told me when I started building on
SharePoint: every column has **two names**, and one of them is set forever
the moment you create it.

- The **display name** is what you see in the list. You can rename it any
  time.
- The **internal name** is what SharePoint actually uses behind the scenes.
  It's created from whatever you first typed, and it **never changes**, no
  matter how many times you rename the column later.

That sounds harmless until you see what SharePoint does to special
characters.

## What happens to spaces and symbols

The internal name only allows letters and numbers. Everything else gets
encoded. Create a column called `Project - Status`, and the internal name
becomes:

```text
Project_x0020__x002d__x0020_Status
```

A space turns into `_x0020_`, a hyphen into `_x002d_`, and so on for
parentheses, slashes, and most punctuation. The column still *looks* fine in
the list, so you might not notice for weeks.

## Where it comes back to bite you

You'll meet the internal name any time you go one level below the list UI:

- **Power Automate** — OData filter queries use internal names. So instead
  of writing `Status eq 'Active'`, you're writing
  `Project_x0020__x002d__x0020_Status eq 'Active'`. Good luck spotting a
  typo in that.
- **REST API and JSON** — same thing, everywhere.
- Renaming the column later doesn't help. The ugly internal name is
  permanent.

## The two-step trick

The fix is simple once you know it:

1. **Create** the column with a clean name, no spaces or symbols:
   `ProjectStatus`
2. **Rename** it afterwards to whatever reads nicely: `Project - Status`

Now the display name is friendly and the internal name stays `ProjectStatus`
forever. Your filter queries stay readable.

The same idea applies to the **list itself**: the list's URL comes from its
creation name. Create it as `ProjectTracker`, then rename it to
`Project Tracker`, and you get a clean URL instead of `%20` soup.

## How to check an internal name

Go to **List settings**, click the column, and look at the end of the URL in
your browser:

```text
...&Field=Project_x0020_Status
```

Whatever comes after `Field=` is the internal name.

One more quirk: the default **Title** column's internal name is always
`Title`, even if you rename it to something else. If a flow references
`Title` and the list shows a column called "Request Name", that's why.

## Takeaway

Create first with a clean name, rename after. Thirty seconds of habit, and
you never have to type `_x0020_` in a filter query again.
