+++
title = "Test"
description = "foo"

# The date of the post.
# 2 formats are allowed: YYYY-MM-DD (2012-10-02) and RFC3339 (2002-10-02T15:00:00Z)
# Do not wrap dates in quotes, the line below only indicates that there is no default date
date = 2018-04-10

# A draft page will not be present in prev/next pagination
draft = false

# If filled, it will use that slug instead of the filename to make up the URL
# It will still use the section path though
# slug = ""

# The path the content will appear at
# If set, it cannot be an empty string and will override both `slug` and the filename.
# The sections' path won't be used.
# It should not start with a `/` and the slash will be removed if it does
# path = ""

# An array of strings allowing you to group pages with them
# tags = []

# An overarching category name for that page, allowing you to group pages with it
# category = ""

# The order as defined in the Section page
order = 0

# The weight as defined in the Section page
weight = 0

# Use aliases if you are moving content but want to redirect previous URLs to the 
# current one. This takes an array of path, not URLs.
aliases = []

# Whether the page should be in the search index. This is only used if
# `build_search_index` is set to true in the config and the parent section 
# hasn't set `in_search_index` to false in its front-matter
in_search_index = true

# Template to use to render this page
template = "page.html"

# Your own data
[extra]
+++

Some content
