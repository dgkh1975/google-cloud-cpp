# Contributor Guides

Thank you for contributing to `google-cloud-cpp`. We receive contributions from
folks with very different backgrounds. Some of you are experienced C++
developers, but this might be your first contribution to a GitHub hosted
project. Some of you may be experienced GitHub contributors, but this might be
the first time contributing to a C++ library project. Some of you may be
experienced with both, but `google-cloud-cpp` has special requirements to
support multiple platforms, compilers, and even multiple build tools.

To help you navigate the project we have prepared (over time) a number of
documents. You do not need to read each one, specially if they address areas
you are already familiar with, but you may want to browse them in case something
is surprising (or wrong! We need to improve these documents too).

## Key Documents

* [Forks and Pull Requests](howto-guide-forks-and-pull-requests.md): the basic
  workflows for GitHub projects.
* [Running CI builds locally](howto-guide-running-ci-builds-locally.md): how to
  reproduce CI results locally, for faster edit -> build -> test cycles.
* [Setup a development workstation](howto-guide-setup-development-workstation.md):
  how to setup a Linux or Windows (workstation or VM) for `google-cloud-cpp`
  development.
* [Setup CMake Dependencies](howto-guide-setup-cmake-environment.md): how to
  install the dependencies of `google-cloud-cpp` in `$HOME` for easier and
  faster development with CMake.
* [Working with Bazel and CMake](working-with-bazel-and-cmake.md): this project
  can be compiled with CMake or Bazel. Always update the CMake project files
  first, as these files are used to generate `*.bzl` files loaded by Bazel.
  More details in the linked document.

## Style

This repository follows the [Google C++ Style Guide](
https://google.github.io/styleguide/cppguide.html), with some additional
constraints specified in the [style guide](/doc/cpp-style-guide.md).
Please make sure your contributions adhere to the style guide.

Many of these rules (but not all of them) are enforced using `clang-tidy(1)`.

## Formatting

The code in this project is formatted with `clang-format(1)`, and our CI builds
will check that the code matches the format generated by this tool before
accepting a pull request. Please configure your editor or IDE to use the Google
style for indentation and other whitespace. If you need to reformat one or more
files, you can simply run our formatting script:

```console
# Set NCPU to how many threads you wish to use
$ env NCPU=4 CHECK_STYLE=yes ./ci/check-style.sh
```

Please be  advised that `clang-format` has been known to generate slightly
different formatting in different versions. We update this version from time to
time, it is clang-tidy-11 as-of 2021-02-09, but this could be out of date. If
you need to confirm this look at the
[Dockerfile](/ci/kokoro/docker/Dockerfile.fedora-install) used in the
`clang-tidy` build, find out which version of Fedora is in use, and then find
out what is the `clang` version included in that distro: search on pkgs.org,
repology.org, or Google; or just ask around.

To run exactly the same formatting programs that the CI builds will run first
setup your workstation to
[run CI builds locally](howto-guide-running-ci-builds-locally.md). And then
run the right build:

```console
# Run from google-cloud-cpp:
$ ./ci/kokoro/docker/build.sh clang-tidy
```

Or if you just want to reformat the code, without compiling the code or running
any tests:

```console
./ci/kokoro/docker/build.sh clang-tidy ./ci/check-style.sh
```

## Upload generated documentation to personal github pages

If you are using your personal fork as the git origin, there is an easy way to
upload generated doxygen documentation to your personal github pages. The
following command will generate the documentation and upload it to the
`my-fancy-feature` subdirectory in the gh-pages branch of your personal fork.
That is, the documentation will be publicly available at:
`http://<username>.github.io/google-cloud-cpp/my-fancy-feature`.

```console
$ DOCS_SUBDIR=my-fancy-feature ./ci/kokoro/docker/build.sh clang-tidy
```
