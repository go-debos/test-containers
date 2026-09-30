# debos-test-containers

These images carry everything needed to build and run
[debos](https://github.com/go-debos/debos) and
[fakemachine](https://github.com/go-debos/fakemachine) and are used by
their CI. They are rebuilt weekly and published to
`ghcr.io/go-debos/test-containers/<image>`.

## Images

| Image             | Containerfile          | Base image             |
| ----------------- | ---------------------- | ---------------------- |
| `arch`            | `Containerfile.arch`   | `archlinux:base-devel` |
| `debian-trixie`   | `Containerfile.debian` | `debian:trixie`        |
| `debian-forky`    | `Containerfile.debian` | `debian:forky`         |
| `ubuntu-stonking` | `Containerfile.debian` | `ubuntu:stonking`      |
| `fedora-44`       | `Containerfile.fedora` | `fedora:44`            |

Each image is named after the release it is built on: the codename for
Debian and Ubuntu, and the release number for Fedora, which has no
codenames. The releases are pinned, so the matrix has to be bumped by
hand when a distribution makes a new release. Arch is a rolling release
and so has no codename.

## Building

Every Containerfile takes a `BASE_IMAGE` build-arg holding the complete
reference of the image to build on top of:

```sh
$ podman build -f Containerfile.debian -t debos-test-container-debian-forky \
    --build-arg BASE_IMAGE=debian:forky .
```

Omit `--build-arg` to build the default base image listed above.
`Containerfile.debian` covers both Debian and Ubuntu and picks the kernel
package to install from the base image's `/etc/os-release`.

## Testing

An image is tested by running the debos and fakemachine unit tests inside
it, which is what CI does after every build. The tests need nested
virtualisation, so the host must have `/dev/kvm`:

```sh
$ git clone https://github.com/go-debos/fakemachine.git
$ podman run \
      --rm \
      --cgroupns=private \
      --tmpfs /scratch:exec \
      --tmpfs /run \
      --device /dev/kvm \
      --privileged \
      -e TMP=/scratch \
      -e SYSTEMD_NSPAWN_UNIFIED_HIERARCHY=1 \
      --workdir /mnt \
      --mount "type=bind,source=$(pwd)/fakemachine,destination=/mnt" \
      debos-test-container-debian-forky \
      go test -v ./...
```

Repeat with `https://github.com/go-debos/debos.git` to run the debos test
suite. Replace `debos-test-container-debian-forky` with any locally built
image or with a published one such as
`ghcr.io/go-debos/test-containers/debian-forky:main`.
