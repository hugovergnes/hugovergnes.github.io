---
layout: page
title: Path-integral graph convolutions
description: Borrowing from physics to aggregate over molecular graphs
img: assets/img/fig_path_integral_gnn.svg
importance: 5
category: curiosities
---

Most graph neural networks aggregate over a node's immediate neighbours. A
path-integral convolutional kernel instead sums over *every* path between two atoms,
damping each one by its length — an idea lifted from physics.

I implemented it for the molhiv dataset on the Open Graph Benchmark, a drug-discovery
task where the relationship between distant atoms genuinely matters. The
implementation is deliberately lightweight: it trains on CPU, and moves to a GPU
without changes.

<div class="row justify-content-sm-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/fig_path_integral_gnn.svg" title="Weighted paths between two atoms in a molecular graph" class="img-fluid rounded" %}
  </div>
</div>
<div class="caption">
  Every path between two atoms contributes, weighted down by its length.
</div>

[Read the full write-up]({% post_url 2021-03-19-GCN-for-drugs %}).
