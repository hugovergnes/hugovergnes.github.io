---
layout: page
title: XMem under stress
description: Probing a video object segmentation model with synthetic benchmarks
img: assets/img/xmem_occlusion_contact_sheet.jpg
importance: 2
category: vision & video
---

[XMem](https://github.com/hkchengrex/XMem) is a video object segmentation model built
around an explicit memory system. Benchmark numbers tell you it works; they don't tell
you *when* it stops working.

So I built synthetic sequences with controlled failure modes — occlusion, appearance
change, fast motion — and watched the memory behave under each one. Synthetic data
means the ground truth is exact and the difficulty is a dial, not a property of
whatever footage happened to be in the dataset.

<div class="row justify-content-sm-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/xmem_occlusion_contact_sheet.jpg" title="Occlusion sequence contact sheet" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  An occlusion sequence, frame by frame.
</div>

[Read the full write-up]({% post_url 2026-06-15-xmem %}).
