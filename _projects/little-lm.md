---
layout: page
title: little-lm
description: A 3.8B language model pretrained from scratch to 0.384 CORE for $998
img: assets/img/fig_core_vs_loss.svg
importance: 1
category: language models
---

A config-driven framework for pretraining decoder-only language models, and
the 3.8B-parameter model I trained with it: **0.384 CORE on 65B tokens, in 43 hours,
for $998** on rented B200s. That beats GPT-2 1.5B (0.2565) by a wide margin and lands
ahead of nanochat's ~$1000 configuration.

The architecture is Llama-style — RMSNorm, RoPE, GQA, relu² MLPs, QK-norm, logit
softcap, and ResFormer-style value embeddings. Training uses Muon for matrix
parameters and AdamW for everything else, on a trapezoidal LR schedule, in FP8.

Things the project turned up along the way:

- **Value embeddings earn their keep.** 19% more parameters bought 0.46% better loss
  and 3.2% better CORE at identical throughput — they're lookups, so they cost memory
  but essentially no FLOPs.
- **Context length is a measurement decision, not just a quality one.** Three of the
  22 CORE tasks never fit in a 1024-token context. SQuAD decayed monotonically to
  exactly zero — not because the model got worse, but because it got *better* at
  language and stopped accidentally matching short gold answers.
- **Careful dtype handling is underrated.** bf16 master weights cut VRAM 27% and gave
  a 2.2× throughput win, for a CORE cost of roughly 0.01.

<div class="row justify-content-sm-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/fig_core_vs_loss.svg" title="Eval loss and CORE for the 1024 and 2048 context runs" class="img-fluid rounded" %}
  </div>
</div>
<div class="caption">
  At step 20,000 the two runs share an eval loss of 2.016 — and differ by 0.034 on CORE.
</div>

[Read the full write-up]({% post_url 2026-09-04-little-lm-3-8b %}) for the throughput
work, the ablations, and the things that didn't work.
