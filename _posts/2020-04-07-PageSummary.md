---
layout: post
title: What is the best way to learn Pytorch?
subtitle: ...made with include files and liquid tags
excerpt: "This post shows how to create simple page summaries for those who just need the facts!"
image: "/img/image/jekyll_post.jpg"
show-avatar: true
category: Jekyll
tags: ["PageSummary", "Jekyll"]
comments: true
googlefonts: ["Share+Tech+Mono"]
---

I often start writing a post or page and end up with much more content than I thought at the beginning.
So I started adding a little summary section like this:

```python
def gen_pose(kpts, valid_frames, width, height, model_pos, pad, causal_shift=0):
    assert len(kpts.shape) == 4, 'The shape of kpts: {}'.format(kpts.shape)
    assert kpts.shape[0] == len(valid_frames)

    norm_seqs = []
    for index, frames in enumerate(valid_frames):
        seq_kps = kpts[index, frames]
        norm_seq_kps = normalize_screen_coordinates(seq_kps, w=width, h=height)
        norm_seqs.append(norm_seq_kps)

    gen = UnchunkedGenerator(None, None, norm_seqs, pad=pad, causal_shift=causal_shift, augment=True,
                             kps_left=kps_left, kps_right=kps_right, joints_left=joints_left, joints_right=joints_right)
    prediction = evaluate(gen, model_pos)
```

```css
.text-muted {
    color: #808080;
    font-size: 14px;
}
```

This works perfect but now it's time to create something more pleasant.

So I started working with include files and ended with this:

{% include about.html caption="About_FooBar" content="Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet." %}


It's done by a simple `include` statement which uses the given file in the `_includes` folder and parses the
content. You can use it on every page or post you want a content summary.

The about.html include takes to optional parameters:

- **caption**: You can specify a custom caption. If you don't define it uses the page title. If the title has more
  than 35 chars it gets truncated.
- **content**: Define your content with this if you don't want to use the `page.excerpt` value.

{% raw %}
```powershell
{% include about.html caption="About_Foobar" content="Some awesome content summary goes in here...." %}
```
{% endraw %}

Detailed features in `about.html`:

- Uses page title and adds it as about page name
- Static tooltip
- Expands content on click at header.
- Container position is absolute and doesn't move the content down below.
- Blinking cursor at the end of the content string. *(CSS source by [Artem Gordinsky](https://codepen.io/ArtemGordinsky/pen/GnLBq))*

## Sources


{% gist OCram85/e9715be8a3e351a2c620a65b0d799f14 %}
