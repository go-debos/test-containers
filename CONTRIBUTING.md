<!--
SPDX-FileCopyrightText: Qualcomm Technologies, Inc. and/or its subsidiaries.
SPDX-License-Identifier: Apache-2.0
-->

# Contributing to debos-test-containers

:+1::tada: Firstly, thank you for taking the time to contribute! :tada::+1:

The following is a set of guidelines for contributing to debos-test-containers, which is hosted on [GitHub](https://github.com/go-debos/test-containers).

These are mostly guidelines and not rules. Use your best judgement and feel free to propose changes to this document in a pull request.


## Get in touch!

💬 Join us on Matrix at [#debos:matrix.debian.social](https://matrix.to/#/#debos:matrix.debian.social)
to chat about usage or development of debos.

🪲 To report a bug, issue or feature request, create a new
[GitHub Issue](https://github.com/go-debos/test-containers/issues).


## Maintainers

 - [Sjoerd Simons - @sjoerdsimons](https://github.com/sjoerdsimons)
 - [Christopher Obbard - @obbardc](https://github.com/obbardc)
 - [Dylan Aïssi - @daissi](https://github.com/daissi)


## Code of conduct

Be kind, constructive and respectful.


## Ways to contribute

- **Report bugs** and regressions
- **Improve documentation**
- **Add or bump distribution releases** in the CI matrix
- **Add packages** needed by debos or fakemachine

If you're planning a larger change, please open an issue first so it can be discussed with maintainers before investing a lot of time.


## Reporting bugs

Please create a [GitHub Issue](https://github.com/go-debos/test-containers/issues) and include:

- The image affected (e.g. `debian-forky`, `fedora-45`)
- Steps to reproduce (ideally a minimal command line)
- What you expected to happen
- What actually happened (including **full** error output)

Logs and links to failing CI runs are very welcome.


## Development setup

Prerequisites:

- `podman` (or `docker`)
- Optional but recommended: ability to use `/dev/kvm` on your host, which
  is needed to run the debos and fakemachine tests inside an image

Clone your fork:

```sh
git clone https://github.com/<your-username>/test-containers.git
cd test-containers
```

See the [README](README.md) for how to build an image and run the debos
and fakemachine test suites inside it.

Check the repository is [REUSE](https://reuse.software/) compliant:

```sh
reuse lint
```


## Coding style

* Keep changes **small and focused** where possible
* Prefer clear, simple code over clever one-liners
* Keep the Containerfiles consistent with each other
* Give every new file an SPDX copyright and license header

If you touch existing code, try to follow the style of the surrounding code.


## Submitting changes (Pull Requests)

1. Fork the repository and create a feature branch:

```sh
git checkout -b wip/my-username/my-feature
```

2. Make your changes and keep the commit history reasonably clean
   (small, logical commits are easier to review).

3. Ensure the images you changed build and pass the debos and fakemachine
   tests locally, as described in the [README](README.md).

4. Ensure the REUSE check passes locally:

```sh
reuse lint
```

5. Push your branch and open a **Pull Request** against `main`:

   * Use a clear PR title (e.g. `Containerfile.fedora: install foo`)
   * Describe *what* you changed and *why*
   * Mention any relevant issue numbers (e.g. `Fixes: #123`)
   * Call out any changes to image names, as debos and fakemachine CI
     pull the images by name

Reviewers may ask for adjustments - this is a normal part of the process.

Ensure your pull request is always rebased on top the latest debos-test-containers main branch.


## License and copyright

debos-test-containers is licensed under the **Apache-2.0** License.
By submitting a pull request, you agree that your contributions will be licensed under the same terms.


Thanks again for helping improve debos-test-containers!
