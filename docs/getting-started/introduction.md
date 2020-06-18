---
title: Introduction
group: getting-started
description: IoT-LAB documentation brings detailed information about the testbed, its usage and its tools to make the most of this experimentation platform and give you the best user experience.
---

## Quickstart

The testbed enables access to hundreds of boards for experimenting, deployed across different sites. This deployment makes IoT-LAB:

- **multi-platform**, in that it offers various different experimentation boards;
- **multi-radio**, in that boards don’t all have the same radio chips, and some have more than one;
- **multi-topology**, in that the physical deployments are all different (in grids, in several corridors, dense, scattered, over several levels, etc.);
- **multi-OS**, in that the different boards have one or more embedded OS support.

The main server serves the open API that allows all interactions. Of course, an easy access is provided through a web portal and command line interface (CLI) tools.

In addition, the testbed offers an hosted environment on SSH frontends (one per IoT-LAB site), featuring:
- pre-installed command line interface (CLI) tools,
- cross-compiler toolchains for target architectures,
- access to devices serial link, debuger and radio sniffer.
- and experiments results,

[Several workspaces]({% link docs/getting-started/workspaces.md %}) are available to facilitate the setup of the
development environment for users and the interaction with the testbed.

### Run an experiment

<div class="row my-3 d-flex justify-content-center">
    <div class="col-lg-5">
        <div class="mb-2 p-3 bg-info text-light text-center rounded">
            <h6 class="card-title m-0">1. Build your application</h6>
        </div>
        <div class="mb-2 p-3 bg-info text-light text-center rounded">
            <h6 class="card-title m-0">2. Select Resources</h6>
        </div>
        <div class="mb-2 p-3 bg-info text-light text-center rounded">
            <h6 class="card-title m-0">3. Configure nodes</h6>
        </div>
        <div class="mb-2 p-3 bg-info text-light text-center rounded">
            <h6 class="card-title m-0">4. Submit</h6>
        </div>
    </div>
</div>

Upload your firmware(s). Select the nodes that you want to use, regarding their characteristics and/or their physical topology. Associate them with a firmware, and  optionally configure some monitoring or sniffing. Submit your experimentation. The scheduler will run it at the right time.

## Learn

The documentation here will bring you a lot of information regarding the features and possibilities of the testbed. But we also added more practical examples. Visit the [Learn]({{ site.baseurl }}{% link learn/index.html %}) page.
