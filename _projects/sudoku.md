---
layout: page
title: Solving Sudoku like a human
description: A heuristic solver that never backtracks
img: assets/img/fig_sudoku_candidates.svg
importance: 6
category: side projects
---

The standard computer-science answer to Sudoku is backtracking: pick a branch, and if
it contradicts, unwind. It works, and it is nothing like how a person solves a puzzle.
I like to solve mine in one pass.

So this solver does what a human does. Every cell tracks its own candidate set, and a
digit goes down only when it is the sole option for that cell, or that cell is the sole
option for the digit. No branching, no unwinding — the constraints propagate until the
grid falls out.

It's built around a single `Cell` class holding a position, a value, and a candidate
set. Once that exists and the candidate sets stay honest, the puzzle mostly solves
itself. Written on a long flight, as an excuse to apply decent software engineering to
a puzzle I've liked since I was a kid.

<div class="row justify-content-sm-center">
  <div class="col-sm-10 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/fig_sudoku_candidates.svg" title="A grid with one cell's candidate set pencilled in" class="img-fluid rounded" %}
  </div>
</div>
<div class="caption">
  The highlighted cell has three candidates left. Eliminate two more and it resolves itself.
</div>

[Read the full write-up]({% post_url 2024-08-02-sudokus %}).
