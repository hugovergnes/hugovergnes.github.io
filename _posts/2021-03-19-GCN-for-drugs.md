---
title:  "Path Integral Based Convolution Graph Neural Network to solve the molhiv dataset"
layout: post
---

Graph Neural Networks (GNNs) have shown significant promise in tackling molecular data problems, especially for tasks like drug discovery. In my latest project, I implemented a Path Integral-Based Convolutional Kernel to solve the molhiv dataset on the Open Graph Benchmark (OGB). This approach borrows concepts from physics, particularly path integrals, to improve the way GNNs aggregate information across molecular graphs, offering an innovative method to process edge and node relationships.




The implementation was designed to be lightweight and adaptable. While I initially ran the training on a CPU, the model can easily be transferred to a GPU using Google Colab for faster results. If you’re interested in experimenting with it, I’ve also included a ready-to-go Colab notebook that automates the setup. Special thanks to the authors of the original paper on Path Integral-based GNNs and the guidance from CS224W.