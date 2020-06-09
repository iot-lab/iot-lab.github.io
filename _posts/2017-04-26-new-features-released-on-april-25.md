---
title: New features released on April, 25
---

![]({{ '/assets/images/posts/' | relative_url }}tools.png){: .img-fluid }
{: .text-center}

The whole FIT IoT-LAB testbed was closed on April 25th afternoon for upgrade operations.
{: .lead}

Here is the details of the new features available from today.

### Run Script

We finally release a feature we would like to provide from a long time ago. For sure, it is really convenient to be able to specify a firmware that will be flashed automatically at the experiment starting, as much as to specify a profile for the automatic monitoring setup. But we are quite sure that you may have already say to yourself: “I just miss something to launch my own script automatically after that”.

We finally had some time to integrate this feature in our Open REST API, letting the possibility to specify a script that will be run in background on the SSH frontends. You can launch this script manually at any time during your experiment or you can specify this script at experiment submission. In this last case, it will be launched automatically at experiment starting.

We made this new feature easy to use by providing it to the CLI tools. Follow [this documentation]({{ site.baseurl }}{% link docs/tools/run-script.md %}) to get an introduction of this feature and learn how it works.

### CLI Tools 2.4.0

Version 2.4.0 of our IoT-LAB CLI tools is here, with new interesting features:

* a <tt>script</tt> subcommand, enabling the use of the new Run Script feature explained just above
* an <tt>update-idle</tt> and a <tt>profile-reset</tt> commands, to respectively set firmware and profile to defaults
* a <tt>profile-load</tt> command, to update profiles
* improvement in filtering possibilities in commands

This new version is now available on [PyPI](https://pypi.python.org/pypi/iotlabcli/2.4.0 "iotlabcli on PyPI"), easy to install with this command:

```
pip install iotlabcli --upgrade
```

You will also find on [the module page](https://pypi.python.org/pypi/iotlabcli/2.4.0 "iotlab-cli on PyPI") the complete changelog.
