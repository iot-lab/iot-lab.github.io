---
title: New SSH CLI Tools
---

![]({{ '/assets/images/posts/' | relative_url }}tools.png){: .img-fluid }
{: .text-center}

After the release of a new version of the CLI Tools a few weeks ago, we are happy to announce the new **SSH CLI Tools** are now available on the testbed.
{: .lead}

The IoT-LAB team has specially designed these tools to remotely control the A8 nodes from the SSH frontends or from a local machine. With the SSH CLI Tools, you’ll find interesting features such as:

* **flashing/resetting the M3** behind the A8
* **waiting for the system boot** of all A8 of an experiment
* **running commands** on the frontend or on the A8
* **running a script** in background on the A8

You can read the documentation [here]({{ site.baseurl }}{% link docs/tools/ssh-cli.md %}).

The SSH CLI Tools source code is [available on GitHub](https://github.com/iot-lab/ssh-cli-tools) so if you find bugs or potential improvements, feel free to propose a Pull Request or open an issue.

Finally, since the SSH CLI Tools are available on PYPI, you can use them from your computer. In this case, they can be installed using pip:

```
sudo pip install iotlabsshcli
```