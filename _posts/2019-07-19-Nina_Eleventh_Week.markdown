---
layout: post
author: nm
title: "Cells and clusters"
date: 2019-07-19 10:15:00 +0200
categories: jekyll update
comments: true

---
<p>This week I have been working on cell and cluster layout.</p>

### Cell layout
<p>It is pretty easy to imagin this layout. Based on number of elements and their sizes, the drawing space is devided into invisible cells. Each of those is ocupied by a vertex, which are than connected with edges.</p>

- <https://github.com/medicka/PharoGSoC/commit/9a3e002308dfed4ff2109020bdb2222f40cf546b>
- <https://github.com/medicka/PharoGSoC/commit/b3fde85b177a3edb29894e6a62c01c0756ad187e>
- <https://github.com/medicka/PharoGSoC/commit/4fcbd1bb261eb3e6a20fd19c11ea07d7adb8d228>
- <https://github.com/medicka/PharoGSoC/commit/27c3f01cbacc1a61798ade4e3a6d9046358f7504>

### Cluster layout
<p>In this type of layout we position vertices in such postions that they forma a cluster, which repesents a group of objects that are position close together. Lets put it in other perspective. In context of servers, cluster is a group of computers that are connected with each other and operate closely, as if they were one computer.</p>
In order to implement this layouts, firstly I needed to add some methods into the root class os all layouts:

- <https://github.com/medicka/PharoGSoC/commit/a3c1cd5cc1c20066afc3ecd5350a0bab44a2c2bd>

Than I implemented necessary classes and methods for the layout itself:

- <https://github.com/medicka/PharoGSoC/commit/c38906af415768cc6ff93152e726e29f82a05360>
- <https://github.com/medicka/PharoGSoC/commit/f82ce65d2b25ae31da7e8e009f899536de53bd09>
- <https://github.com/medicka/PharoGSoC/commit/f97d9684b959159ed3a636be0f2016d4d0a39711>
- <https://github.com/medicka/PharoGSoC/commit/728cb8864493c13e0cfa4966b053b45fccbe7b94>
- <https://github.com/medicka/PharoGSoC/commit/e9027cf9a1ee519b870775dc277001e63c730314>

<p>Beside the layouts, I added better explanations to some methods, changed some methosd classifications and addopted some expected results.</p>

- <https://github.com/medicka/PharoGSoC/commit/79f7f99e1eef1f61c429569ef27369028a4f0d39>
- <https://github.com/medicka/PharoGSoC/commit/fd381eec03c09cc6c6189d788ece99754588b99a>
- <https://github.com/medicka/PharoGSoC/commit/a8691883a428544998709f28e1bcfbae351b1e6c>
