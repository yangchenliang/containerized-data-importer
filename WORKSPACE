register_toolchains("//:python_toolchain")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive", "http_file")
load(
    "@bazel_tools//tools/build_defs/repo:http.bzl",
    "http_archive",
    "http_file",
)
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

http_archive(
    name = "rules_python",
    sha256 = "778197e26c5fbeb07ac2a2c5ae405b30f6cb7ad1f5510ea6fdac03bded96cc6f",
    urls = [
        "https://github.com/bazelbuild/rules_python/releases/download/0.2.0/rules_python-0.2.0.tar.gz",
        "https://storage.googleapis.com/builddeps/778197e26c5fbeb07ac2a2c5ae405b30f6cb7ad1f5510ea6fdac03bded96cc6f",
    ],
)

load("//third_party:deps.bzl", "deps")

deps()

# register crosscompiler toolchains
load("//bazel/toolchain:toolchain.bzl", "register_all_toolchains")

register_all_toolchains()

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive", "http_file")

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "69de5c704a05ff37862f7e0f5534d4f479418afc21806c887db544a316f3cb6b",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.27.0/rules_go-v0.27.0.tar.gz",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.27.0/rules_go-v0.27.0.tar.gz",
        "https://storage.googleapis.com/builddeps/69de5c704a05ff37862f7e0f5534d4f479418afc21806c887db544a316f3cb6b",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_rules_dependencies", "go_register_toolchains")

go_rules_dependencies()

go_register_toolchains(
    go_version = "1.16.1",
)

http_archive(
    name = "com_google_protobuf",
    sha256 = "cd218dc003eacc167e51e3ce856f6c2e607857225ef86b938d95650fcbb2f8e4",
    strip_prefix = "protobuf-6d4e7fd7966c989e38024a8ea693db83758944f1",
    # version 3.10.0
    urls = [
        "https://github.com/google/protobuf/archive/6d4e7fd7966c989e38024a8ea693db83758944f1.zip",
        "https://storage.googleapis.com/builddeps/cd218dc003eacc167e51e3ce856f6c2e607857225ef86b938d95650fcbb2f8e4",
    ],
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()

# gazelle rules
http_archive(
    name = "bazel_gazelle",
    sha256 = "62ca106be173579c0a167deb23358fdfe71ffa1e4cfdddf5582af26520f1c66f",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.23.0/bazel-gazelle-v0.23.0.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.23.0/bazel-gazelle-v0.23.0.tar.gz",
        "https://storage.googleapis.com/builddeps/62ca106be173579c0a167deb23358fdfe71ffa1e4cfdddf5582af26520f1c66f",
    ],
)

load(
    "@bazel_gazelle//:deps.bzl",
    "gazelle_dependencies",
    "go_repository",
)

gazelle_dependencies()

#load("@com_github_bazelbuild_buildtools//buildifier:deps.bzl", "buildifier_dependencies")

#buildifier_dependencies()

# bazel docker rules
http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "95d39fd84ff4474babaf190450ee034d958202043e366b9fc38f438c9e6c3334",
    strip_prefix = "rules_docker-0.16.0",
    urls = [
        "https://github.com/bazelbuild/rules_docker/releases/download/v0.16.0/rules_docker-v0.16.0.tar.gz",
        "https://storage.googleapis.com/builddeps/95d39fd84ff4474babaf190450ee034d958202043e366b9fc38f438c9e6c3334",
    ],
)

load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_image",
    "container_pull",
)
load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)

container_repositories()

# This is NOT needed when going through the language lang_image
# "repositories" function(s).
load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")

container_deps()

# override rules_docker issue with this dependency
# rules_docker 0.16 uses 0.1.4, bit since there the checksum changed, which is very weird, going with 0.1.4.1 to
go_repository(
    name = "com_github_google_go_containerregistry",
    importpath = "github.com/google/go-containerregistry",
    sha256 = "bc0136a33f9c1e4578a700f7afcdaa1241cfff997d6bba695c710d24c5ae26bd",
    strip_prefix = "google-go-containerregistry-efb2d62",
    type = "tar.gz",
    urls = ["https://api.github.com/repos/google/go-containerregistry/tarball/efb2d62d93a7705315b841d0544cb5b13565ff2a"],  # v0.1.4.1
)

# RPM rules
http_archive(
    name = "io_bazel_rules_container_rpm",
    sha256 = "151261f1b81649de6e36f027c945722bff31176f1340682679cade2839e4b1e1",
    strip_prefix = "rules_container_rpm-0.0.5",
    urls = [
        "https://github.com/rmohr/rules_container_rpm/archive/v0.0.5.tar.gz",
        "https://storage.googleapis.com/builddeps/151261f1b81649de6e36f027c945722bff31176f1340682679cade2839e4b1e1",
    ],
)

# Pull base image fedora33
container_pull(
    name = "fedora",
    digest = "sha256:bfcc10d2d2a3a52fe997daba311c3a5298b426b524ab2b012fa24730dd0eb763",
    registry = "quay.io",
    repository = "fedora/fedora",
    tag = "33-x86_64",
)

#No need to update this one until we re-enable the cinder lane, as only the lvm pod uses this.
container_pull(
    name = "fedora-aarch64",
    registry = "quay.io",
    repository = "fedora/fedora",
    tag = "33-aarch64",
)

container_pull(
    name = "fedora-docker",
    digest = "sha256:fdf235fa167d2aa5d820fba274ec1d2edeb0534bd32d28d602a19b31bad79b80",
    registry = "index.docker.io",
    repository = "fedora",
    tag = "33",
)

# Pull base image container registry
container_pull(
    name = "registry",
    digest = "sha256:b1165286043f2745f45ea637873d61939bff6d9a59f76539d6228abf79f87774",
    registry = "index.docker.io",
    repository = "library/registry",
    tag = "2",
)

# RPMS
http_file(
    name = "qemu-img",
    sha256 = "7128a6513323264b21e1572764fa2d2ea11753a1c1c3933a4bc1c4843f165633",
    urls = ["https://storage.googleapis.com/builddeps/7128a6513323264b21e1572764fa2d2ea11753a1c1c3933a4bc1c4843f165633"],
)

http_file(
    name = "qemu-img-aarch64",
    sha256 = "715523961ee6c0b1617b067ae3e0e0f5a9818626f69dd29d11b66d3cfd37cfad",
    urls = [
        "http://download.fedoraproject.org/pub/fedora/linux/updates/33/Everything/aarch64/Packages/q/qemu-img-5.1.0-9.fc33.aarch64.rpm",
        "https://storage.googleapis.com/builddeps/715523961ee6c0b1617b067ae3e0e0f5a9818626f69dd29d11b66d3cfd37cfad",
    ],
)

http_file(
    name = "nginx",
    sha256 = "e98ab45cb7f616ac99d5dde14d318c0374c060816b02a0d6360a1ac6e6f0c5c4",
    urls = ["https://storage.googleapis.com/builddeps/e98ab45cb7f616ac99d5dde14d318c0374c060816b02a0d6360a1ac6e6f0c5c4"],
)

http_file(
    name = "xen-libs",
    sha256 = "b5a460dceb4f9feff4701088f6421bbf380f9eb285b56fac1409e236a9d6877b",
    urls = ["https://storage.googleapis.com/builddeps/b5a460dceb4f9feff4701088f6421bbf380f9eb285b56fac1409e236a9d6877b"],
)

http_file(
    name = "xen-libs-aarch64",
    sha256 = "cda623f50ec363b1dc8a27ac969973198d6853ec373dc5d26dcdf14978c0415e",
    urls = [
        "http://download.fedoraproject.org/pub/fedora/linux/updates/33/Everything/aarch64/Packages/x/xen-libs-4.14.2-2.fc33.aarch64.rpm",
        "https://storage.googleapis.com/builddeps/cda623f50ec363b1dc8a27ac969973198d6853ec373dc5d26dcdf14978c0415e",
    ],
)

http_file(
    name = "libaio",
    sha256 = "51ae3b86c7a6fd64ed187574b3a0a7e3a58f533a6db80e3bf44be99f5fd72f50",
    urls = ["https://storage.googleapis.com/builddeps/51ae3b86c7a6fd64ed187574b3a0a7e3a58f533a6db80e3bf44be99f5fd72f50"],
)

http_file(
    name = "libaio-aarch64",
    sha256 = "a2f2ee3465c4495e1b4f10c9dad5dacc9e9679cc8d1153cf8155066ae56303db",
    urls = [
        "http://download.fedoraproject.org/pub/fedora/linux/releases/33/Everything/aarch64/os/Packages/l/libaio-0.3.111-10.fc33.aarch64.rpm",
        "https://storage.googleapis.com/builddeps/a2f2ee3465c4495e1b4f10c9dad5dacc9e9679cc8d1153cf8155066ae56303db",
    ],
)

http_file(
    name = "capstone",
    sha256 = "1ee04e337c7ba1d8f3d17510b4b86d5a2090f31244a4d9cef3f6f5eb83ec93a9",
    urls = ["https://storage.googleapis.com/builddeps/1ee04e337c7ba1d8f3d17510b4b86d5a2090f31244a4d9cef3f6f5eb83ec93a9"],
)

http_file(
    name = "capstone-aarch64",
    sha256 = "89b37a5cbc4bd0ae3b36ab3887edaa8b4ecb7db5f7f02d461f4ced10f17e311d",
    urls = [
        "http://download.fedoraproject.org/pub/fedora/linux/releases/33/Everything/aarch64/os/Packages/c/capstone-4.0.2-3.fc33.aarch64.rpm",
        "https://storage.googleapis.com/builddeps/89b37a5cbc4bd0ae3b36ab3887edaa8b4ecb7db5f7f02d461f4ced10f17e311d",
    ],
)

http_file(
    name = "gperftools-lib",
    sha256 = "4013a64942bbb4644f433e38ff3a2cb0db19978d5aff44461efb42b4edfd0993",
    urls = ["https://storage.googleapis.com/builddeps/4013a64942bbb4644f433e38ff3a2cb0db19978d5aff44461efb42b4edfd0993"],
)

http_file(
    name = "libunwind",
    sha256 = "01957e4ebfb63766b22fb9d865d8c8e13b945a4a49cc14af7261e9d1bc6279f2",
    urls = ["https://storage.googleapis.com/builddeps/01957e4ebfb63766b22fb9d865d8c8e13b945a4a49cc14af7261e9d1bc6279f2"],
)

http_file(
    name = "nginx-mimetypes",
    sha256 = "e860501275c9073f199354766d9ccd99afc0b97fff8acae8e8184d4f02799d38",
    urls = ["https://storage.googleapis.com/builddeps/e860501275c9073f199354766d9ccd99afc0b97fff8acae8e8184d4f02799d38"],
)

http_file(
    name = "nginx-filesystem",
    sha256 = "ff48d81762bb83eb5ed5aed829a50515af3b706ec6c7b8645ac1f3ac034eefe0",
    urls = ["https://storage.googleapis.com/builddeps/ff48d81762bb83eb5ed5aed829a50515af3b706ec6c7b8645ac1f3ac034eefe0"],
)

http_file(
    name = "buildah",
    sha256 = "15d9cca0887f78d7c5530b2b65fc90b221b999962dfa6323b42571020ae434e9",
    urls = ["https://storage.googleapis.com/builddeps/15d9cca0887f78d7c5530b2b65fc90b221b999962dfa6323b42571020ae434e9"],
)

http_file(
    name = "containers-common",
    sha256 = "26f573cf377eff79893b17a7e3f2ade9984820bcd1776db5fc24bb8b70587349",
    urls = ["https://storage.googleapis.com/builddeps/26f573cf377eff79893b17a7e3f2ade9984820bcd1776db5fc24bb8b70587349"],
)

http_file(
    name = "containers-common-aarch64",
    sha256 = "2a230e8c2059536ef3377f0094a53db609513187623a4b1d69b9265d4b044bb6",
    urls = [
        "https://storage.googleapis.com/builddeps/2a230e8c2059536ef3377f0094a53db609513187623a4b1d69b9265d4b044bb6",
    ],
)

http_file(
    name = "tar",
    sha256 = "871dc18514b9b64bcff6c4c61fd4c1a9f4c1e46cddd6f6934b4ee93662541aca",
    urls = ["https://storage.googleapis.com/builddeps/871dc18514b9b64bcff6c4c61fd4c1a9f4c1e46cddd6f6934b4ee93662541aca"],
)

http_file(
    name = "ostree-libs",
    sha256 = "2523f8915b724a14312cd4103faa0e6a213b6dab18a89c7bec6e3c70b0acc66d",
    urls = ["https://storage.googleapis.com/builddeps/2523f8915b724a14312cd4103faa0e6a213b6dab18a89c7bec6e3c70b0acc66d"],
)

http_file(
    name = "ostree-libs-aarch64",
    sha256 = "86fbe688a50d119d73af6cd1b70707aa35046e907485eb9020409293c426813a",
    urls = [
        "http://download.fedoraproject.org/pub/fedora/linux/updates/33/Everything/aarch64/Packages/o/ostree-libs-2021.2-2.fc33.aarch64.rpm",
        "https://storage.googleapis.com/builddeps/86fbe688a50d119d73af6cd1b70707aa35046e907485eb9020409293c426813a",
    ],
)

http_file(
    name = "lvm2",
    sha256 = "1d0378ffc0575f8627445aa666533e4558235d830adb61927069e4682eca3104",
    urls = [
        "http://download.fedoraproject.org/pub/fedora/linux/releases/33/Everything/x86_64/os/Packages/l/lvm2-2.03.10-1.fc33.x86_64.rpm",
        "https://storage.googleapis.com/builddeps/1d0378ffc0575f8627445aa666533e4558235d830adb61927069e4682eca3104",
    ],
)

http_file(
    name = "lvm2-libs",
    sha256 = "dbc237320a73c44c38124da66469d199a49c3361d416f9e7354b9e106043938c",
    urls = ["https://storage.googleapis.com/builddeps/dbc237320a73c44c38124da66469d199a49c3361d416f9e7354b9e106043938c"],
)

http_file(
    name = "device-mapper",
    sha256 = "3d0f1d848a92a8401ca6c8778f9a9a329af8a8420ae14a5c8c99ccbcbd97ebb7",
    urls = ["https://storage.googleapis.com/builddeps/3d0f1d848a92a8401ca6c8778f9a9a329af8a8420ae14a5c8c99ccbcbd97ebb7"],
)

http_file(
    name = "device-mapper-libs",
    sha256 = "9539c6e7a76422600939d661382634d7912e0669aa7e273fdf14b1fcde5b0652",
    urls = ["https://storage.googleapis.com/builddeps/9539c6e7a76422600939d661382634d7912e0669aa7e273fdf14b1fcde5b0652"],
)

http_file(
    name = "device-mapper-event",
    sha256 = "68242b0ea47075bd78ef4bbab44520d2061582ad8ebf57fd4027fdac77f256f0",
    urls = [
        "http://download.fedoraproject.org/pub/fedora/linux/releases/33/Everything/x86_64/os/Packages/d/device-mapper-event-1.02.173-1.fc33.x86_64.rpm",
        "https://storage.googleapis.com/builddeps/68242b0ea47075bd78ef4bbab44520d2061582ad8ebf57fd4027fdac77f256f0",
    ],
)

http_file(
    name = "device-mapper-event-libs",
    sha256 = "605a07738477a5a7d9c536f84e7df5b3f7c607125c08223151cab4dae1e8b9cb",
    urls = ["https://storage.googleapis.com/builddeps/605a07738477a5a7d9c536f84e7df5b3f7c607125c08223151cab4dae1e8b9cb"],
)

http_file(
    name = "device-mapper-persistent-data",
    sha256 = "f7e8201cb8e3fb9269c47c1ca758aebcd529a7a1578bd520d74074943e96b3e9",
    urls = [
        "http://download.fedoraproject.org/pub/fedora/linux/releases/33/Everything/x86_64/os/Packages/d/device-mapper-persistent-data-0.8.5-4.fc33.x86_64.rpm",
        "https://storage.googleapis.com/builddeps/f7e8201cb8e3fb9269c47c1ca758aebcd529a7a1578bd520d74074943e96b3e9",
    ],
)

http_file(
    name = "compat-readline5",
    sha256 = "d37fb057cd371d93c2b3903544bbd3d30683242867ebfd7996866494c9b71021",
    urls = ["https://storage.googleapis.com/builddeps/d37fb057cd371d93c2b3903544bbd3d30683242867ebfd7996866494c9b71021"],
)

http_file(
    name = "kmod",
    sha256 = "5d3d98545ad28bd76a8fe11acbebde68897872aeb0c6fb2b63f9b8b495b7383c",
    urls = ["https://storage.googleapis.com/builddeps/5d3d98545ad28bd76a8fe11acbebde68897872aeb0c6fb2b63f9b8b495b7383c"],
)

http_file(
    name = "basesystem",
    sha256 = "f4efaa5bc8382246d8230ece8bacebd3c29eb9fd52b509b1e6575e643953851b",
    urls = ["https://storage.googleapis.com/builddeps/f4efaa5bc8382246d8230ece8bacebd3c29eb9fd52b509b1e6575e643953851b"],
)

http_file(
    name = "bash",
    sha256 = "c59a621f3cdd5e073b3c1ef9cd8fd9d7e02d77d94be05330390eac05f77b5b60",
    urls = ["https://storage.googleapis.com/builddeps/c59a621f3cdd5e073b3c1ef9cd8fd9d7e02d77d94be05330390eac05f77b5b60"],
)

http_file(
    name = "fedora-gpg-keys",
    sha256 = "45565c84ae0c38c2dda5f1d17b398acb1c6be3018e7ab385ce7920cd888e779b",
    urls = ["https://storage.googleapis.com/builddeps/45565c84ae0c38c2dda5f1d17b398acb1c6be3018e7ab385ce7920cd888e779b"],
)

http_file(
    name = "fedora-release",
    sha256 = "5e4cba4a5a21d9f84a364ae3ba129eb26d1b0514c810cf5d116b6e879e8efff5",
    urls = ["https://storage.googleapis.com/builddeps/5e4cba4a5a21d9f84a364ae3ba129eb26d1b0514c810cf5d116b6e879e8efff5"],
)

http_file(
    name = "fedora-release-common",
    sha256 = "a98b94b73e2213e9e53ff3855ac7a306b1965db0518a0e510411b801d9d15d4e",
    urls = ["https://storage.googleapis.com/builddeps/a98b94b73e2213e9e53ff3855ac7a306b1965db0518a0e510411b801d9d15d4e"],
)

http_file(
    name = "fedora-repos",
    sha256 = "7a541cc42342eca39eb487cf0de670ad374006a7a204c0e1f5ff69b6b509ab6f",
    urls = ["https://storage.googleapis.com/builddeps/7a541cc42342eca39eb487cf0de670ad374006a7a204c0e1f5ff69b6b509ab6f"],
)

http_file(
    name = "filesystem",
    sha256 = "2d9ed3be09813ff727751a6db3a839e49630257df9ab5a21204335f4ca49fecc",
    urls = ["https://storage.googleapis.com/builddeps/2d9ed3be09813ff727751a6db3a839e49630257df9ab5a21204335f4ca49fecc"],
)

http_file(
    name = "glibc",
    sha256 = "f3c6365e5f6ad3d6c34eda0ef25faec8bbd6d0a10d0a5ee226725d50ac6b0a47",
    urls = ["https://storage.googleapis.com/builddeps/f3c6365e5f6ad3d6c34eda0ef25faec8bbd6d0a10d0a5ee226725d50ac6b0a47"],
)

http_file(
    name = "glibc-all-langpacks",
    sha256 = "9d3d5441c7c898109519fa33dd51c615d9d2266206cceae1a159549c5aa6fe33",
    urls = ["https://storage.googleapis.com/builddeps/9d3d5441c7c898109519fa33dd51c615d9d2266206cceae1a159549c5aa6fe33"],
)

http_file(
    name = "glibc-common",
    sha256 = "5e272782cc7bdc3e2005d7b01de6c130eaed69c7d4d01d9bb4b7354af675c13a",
    urls = ["https://storage.googleapis.com/builddeps/5e272782cc7bdc3e2005d7b01de6c130eaed69c7d4d01d9bb4b7354af675c13a"],
)

http_file(
    name = "libgcc",
    sha256 = "14a7ad9770c7d20998dd7e57e9d98666da9e2abd61bbf529a3c54cb2af67d567",
    urls = ["https://storage.googleapis.com/builddeps/14a7ad9770c7d20998dd7e57e9d98666da9e2abd61bbf529a3c54cb2af67d567"],
)

http_file(
    name = "libselinux",
    sha256 = "898d9c9911a8e9b6933d3a7e52350f0dbb92e24ba9b00959cfaf451cec43661a",
    urls = ["https://storage.googleapis.com/builddeps/898d9c9911a8e9b6933d3a7e52350f0dbb92e24ba9b00959cfaf451cec43661a"],
)

http_file(
    name = "libsepol",
    sha256 = "3da666241b0c46a3e6d172e028ce657d02bc6b9c7e2c12757ce629bdfee07a97",
    urls = ["https://storage.googleapis.com/builddeps/3da666241b0c46a3e6d172e028ce657d02bc6b9c7e2c12757ce629bdfee07a97"],
)

http_file(
    name = "ncurses-base",
    sha256 = "3ba2028d4649a5f9e6c77785e09dc5d711f5856c5c91c923ff3f46ea4430f4df",
    urls = ["https://storage.googleapis.com/builddeps/3ba2028d4649a5f9e6c77785e09dc5d711f5856c5c91c923ff3f46ea4430f4df"],
)

http_file(
    name = "ncurses-lib",
    sha256 = "6aa5ec2a16eb602969378982f1d7983acb2fad63198042235224a9e3ebe27e06",
    urls = ["https://storage.googleapis.com/builddeps/6aa5ec2a16eb602969378982f1d7983acb2fad63198042235224a9e3ebe27e06"],
)

http_file(
    name = "pcre2",
    sha256 = "afb45cbdb05dc809cefedd44b5ea1bda59b871ce6bd010252445eb43fd6d361f",
    urls = ["https://storage.googleapis.com/builddeps/afb45cbdb05dc809cefedd44b5ea1bda59b871ce6bd010252445eb43fd6d361f"],
)

http_file(
    name = "setup",
    sha256 = "74d8bf336378256d01cbdb40a8972b0c00ea4b7d433a5c9d5dad704ed5188555",
    urls = ["https://storage.googleapis.com/builddeps/74d8bf336378256d01cbdb40a8972b0c00ea4b7d433a5c9d5dad704ed5188555"],
)

http_file(
    name = "tzdata",
    sha256 = "2f162af6cdbbdae95d5981c4859a00895d6abb3709ba0c20c4138aca69fd002a",
    urls = ["https://storage.googleapis.com/builddeps/2f162af6cdbbdae95d5981c4859a00895d6abb3709ba0c20c4138aca69fd002a"],
)

http_file(
    name = "iscsi-initiator-utils",
    sha256 = "62950607db278f9a9c631e528dec6e8bd00a522b9f9fab69ae4d69000654e62f",
    urls = [
        "http://download.fedoraproject.org/pub/fedora/linux/releases/33/Everything/x86_64/os/Packages/i/iscsi-initiator-utils-6.2.1.1-0.gitac87641.fc33.2.x86_64.rpm",
        "https://storage.googleapis.com/builddeps/62950607db278f9a9c631e528dec6e8bd00a522b9f9fab69ae4d69000654e62f",
    ],
)

http_file(
    name = "iscsi-initiator-utils-iscsiuio",
    sha256 = "9b3d8a210752006a15181de2ea860166040f65e5ce307d439e5abbea8be2655b",
    urls = ["https://storage.googleapis.com/builddeps/9b3d8a210752006a15181de2ea860166040f65e5ce307d439e5abbea8be2655b"],
)

http_file(
    name = "isns-utils-libs",
    sha256 = "b892675cbd02dd907ee1c09bfcc0158f040f0e634d6a3969fbab02c8a29896a7",
    urls = ["https://storage.googleapis.com/builddeps/b892675cbd02dd907ee1c09bfcc0158f040f0e634d6a3969fbab02c8a29896a7"],
)

http_file(
    name = "nbdkit-server",
    sha256 = "b22c4949164901295cc84db1d3747fc05b0dc85a9cb0710143005a61919a53de",
    urls = ["https://storage.googleapis.com/builddeps/b22c4949164901295cc84db1d3747fc05b0dc85a9cb0710143005a61919a53de"],
)

http_file(
    name = "nbdkit-server-aarch64",
    sha256 = "28d0872b0aa914859e479c75ecb3fb3061c7c1701495ec5f3bd166f2c6309204",
    urls = ["https://storage.googleapis.com/builddeps/28d0872b0aa914859e479c75ecb3fb3061c7c1701495ec5f3bd166f2c6309204"],
)

http_file(
    name = "nbdkit-basic-filters",
    sha256 = "51ba4e00f0180ea07b4ed46ca2ded198876bfe67cfe533421cafd0978ed2c7bf",
    urls = ["https://storage.googleapis.com/builddeps/51ba4e00f0180ea07b4ed46ca2ded198876bfe67cfe533421cafd0978ed2c7bf"],
)

http_file(
    name = "nbdkit-basic-filters-aarch64",
    sha256 = "21a40e61d1966509fc6a7575c5af36b6ec31cf44106f674121a1e9996399694b",
    urls = ["https://storage.googleapis.com/builddeps/21a40e61d1966509fc6a7575c5af36b6ec31cf44106f674121a1e9996399694b"],
)

http_file(
    name = "nbdkit-vddk-plugin",
    sha256 = "cee8f05ab93a9e43aec0d97fcc47997e13d9c277b4c334e77ce5e0b68ac51efc",
    urls = ["https://storage.googleapis.com/builddeps/cee8f05ab93a9e43aec0d97fcc47997e13d9c277b4c334e77ce5e0b68ac51efc"],
)

http_file(
    name = "nbdkit-xz-filter",
    sha256 = "a77043f110496658d87332b064f34fc10bbf0fdd429c4bbbe9542308ff087007",
    urls = ["https://storage.googleapis.com/builddeps/a77043f110496658d87332b064f34fc10bbf0fdd429c4bbbe9542308ff087007"],
)

http_file(
    name = "nbdkit-xz-filter-aarch64",
    sha256 = "132b5f5185754d18bb45135f3ec2803aa7ad1c5273b9a34c371986796b753825",
    urls = ["https://storage.googleapis.com/builddeps/132b5f5185754d18bb45135f3ec2803aa7ad1c5273b9a34c371986796b753825"],
)

http_file(
    name = "nbdkit-gzip-filter",
    sha256 = "52787fd9aff69599837328b8b8dd76376999e7c5c96bd72669b0c77a1ac31d4f",
    urls = [
        "http://download.fedoraproject.org/pub/fedora/linux/releases/33/Everything/x86_64/os/Packages/n/nbdkit-gzip-filter-1.22.3-2.fc33.x86_64.rpm",
        "https://storage.googleapis.com/builddeps/52787fd9aff69599837328b8b8dd76376999e7c5c96bd72669b0c77a1ac31d4f",
    ],
)

http_file(
    name = "nbdkit-gzip-filter-aarch64",
    sha256 = "63461edfa15ee1d3861a46202fa1494bbd2ff0e9e83b9d5359df369adc59214b",
    urls = ["https://storage.googleapis.com/builddeps/63461edfa15ee1d3861a46202fa1494bbd2ff0e9e83b9d5359df369adc59214b"],
)

http_file(
    name = "nbdkit-curl-plugin",
    sha256 = "53412db6df5e098d2439d456a309e567af75b721178a9f7a5c10fa192ecf5d43",
    urls = ["https://storage.googleapis.com/builddeps/53412db6df5e098d2439d456a309e567af75b721178a9f7a5c10fa192ecf5d43"],
)

http_file(
    name = "nbdkit-curl-plugin-aarch64",
    sha256 = "63461edfa15ee1d3861a46202fa1494bbd2ff0e9e83b9d5359df369adc59214b",
    urls = ["https://storage.googleapis.com/builddeps/63461edfa15ee1d3861a46202fa1494bbd2ff0e9e83b9d5359df369adc59214b"],
)

http_file(
    name = "libxcrypt-compat",
    sha256 = "51d74854365a393393b4457e3d92ba103c08671b4c881a8a1d9fcb8a54a4a737",
    urls = ["https://storage.googleapis.com/builddeps/51d74854365a393393b4457e3d92ba103c08671b4c881a8a1d9fcb8a54a4a737"],
)

http_file(
    name = "libxcrypt-compat-aarch64",
    sha256 = "f36cfd27003bcfc6f5fba9b99414402397f4b57fd503e84514a06d794f313346",
    urls = ["https://storage.googleapis.com/builddeps/f36cfd27003bcfc6f5fba9b99414402397f4b57fd503e84514a06d794f313346"],
)

http_file(
    name = "libxcrypt",
    sha256 = "a4b3e2d0a10721c22d86fe8517b057fb600addd2a6b9f77f64d5c8b57def627f",
    urls = ["https://storage.googleapis.com/builddeps/a4b3e2d0a10721c22d86fe8517b057fb600addd2a6b9f77f64d5c8b57def627f"],
)

http_file(
    name = "mkpasswd",
    sha256 = "6db907dff3ba74017d46db5cd81409971afeebfb9ef529462e8379def5d43cc0",
    urls = ["https://storage.googleapis.com/builddeps/6db907dff3ba74017d46db5cd81409971afeebfb9ef529462e8379def5d43cc0"],
)

http_file(
    name = "whois-nls",
    sha256 = "6b5c7c46f0a177bf9c8b89ae3eb251a5e7315424c326cc62871b004bcaed414d",
    urls = ["https://storage.googleapis.com/builddeps/6b5c7c46f0a177bf9c8b89ae3eb251a5e7315424c326cc62871b004bcaed414d"],
)

http_file(
    name = "golang-github-vmware-govmomi",
    sha256 = "8c58134cdcec8a993c7da827abb4e9ab78d974038d984ff1fee39963d92736c5",
    urls = ["https://storage.googleapis.com/builddeps/8c58134cdcec8a993c7da827abb4e9ab78d974038d984ff1fee39963d92736c5"],
)

http_file(
    name = "libnbd",
    sha256 = "a63602bb9ebc13f31543332164c64e9c5342089e7431fa35b393f0692b6acb97",
    urls = ["https://storage.googleapis.com/builddeps/a63602bb9ebc13f31543332164c64e9c5342089e7431fa35b393f0692b6acb97"],
)

http_file(
    name = "liburing",
    sha256 = "049778a480dd02774934b37c127b345d8748bfbec1e584f9c412a41af34eaf89",
    urls = ["https://storage.googleapis.com/builddeps/049778a480dd02774934b37c127b345d8748bfbec1e584f9c412a41af34eaf89"],
)

http_file(
    name = "liburing-aarch64",
    sha256 = "253d0c1dc3180f44766c298ae4cd3426ec7a60a41ea0dc50d0884928b031c1b7",
    urls = [
        "http://download.fedoraproject.org/pub/fedora/linux/updates/33/Everything/aarch64/Packages/l/liburing-0.7-3.fc33.aarch64.rpm",
        "https://storage.googleapis.com/builddeps/253d0c1dc3180f44766c298ae4cd3426ec7a60a41ea0dc50d0884928b031c1b7",
    ],
)

http_file(
    name = "libseccomp",
    sha256 = "964e39835b59c76b7eb3f78c460bfc6e7acfb0c40b901775c7e8a7204537f8a7",
    urls = ["https://storage.googleapis.com/builddeps/964e39835b59c76b7eb3f78c460bfc6e7acfb0c40b901775c7e8a7204537f8a7"],
)

http_file(
    name = "libnbd-aarch64",
    sha256 = "0e24ffdcda4efc7445834c86d29d7416426bafa9073259cc31bcb1f03fb5eaeb",
    urls = [
        "http://download.fedoraproject.org/pub/fedora/linux/updates/33/Everything/aarch64/Packages/l/libnbd-1.6.5-1.fc33.aarch64.rpm",
        "https://storage.googleapis.com/builddeps/0e24ffdcda4efc7445834c86d29d7416426bafa9073259cc31bcb1f03fb5eaeb",
    ],
)
