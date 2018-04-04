# Practices Style Guide

## Standard Page Template
The following template can be used as a starting point for your new pages.
```
# {Page Title}
## Contents
{Table of Contents - for long documents}
  * [Anchor link](#anchor-target)
  
## Sub-head
{Sub-head content}
```

## New Content
  1. Create a new branch in this repository
  1. New content should be added to the practices library in Github-compatible markdown format.
  1. New pages must be created in a branch, and then submitted via pull request
  1. Add a link to your new content in the [Practices `readme.md`](../readme.md) file
  1. Create a pull request to merge your changes into the `Master` branch

## Embedded Images
If your images are stored remotely, you can link to them directly from your page. However, if the image needs to be stored/versioned with your page, you can add it to the [[../img/]] directory and then link to it from there.

## Relative Hyperlinks
All hyperlinks to content in this repository should use relative links, so that your links point to content in the the same branch. Links to pages and material in other branches should use absolute (full) links.
