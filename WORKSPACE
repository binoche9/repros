load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "io_bazel_rules_pkg",
    url = "https://github.com/bazelbuild/rules_pkg/releases/download/0.9.1/rules_pkg-0.9.1.tar.gz",
    sha256 = "8f9ee2dc10c1ae514ee599a8b42ed99fa262b757058f65ad3c384289ff70c4b8",
)

http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "5dd1e5dea1322174c57d3ca7b899da381d516220793d0adef3ba03b9d23baa8e",
    url = "https://github.com/bazelbuild/rules_nodejs/releases/download/5.8.3/rules_nodejs-5.8.3.tar.gz",
)

http_archive(
    name = "aspect_rules_js",
    sha256 = "7b2a4d1d264e105eae49a27e2e78065b23e2e45724df2251eacdd317e95bfdfd",
    strip_prefix = "rules_js-1.31.0",
    # url = "https://github.com/aspect-build/rules_js/releases/download/v1.31.0/rules_js-v1.31.0.tar.gz",
    url = "https://github.com/aspect-build/rules_js/archive/c9791f95c685c78703e1a2b6be8b4e07da05f50e.tar.gz",
)


load("@io_bazel_rules_pkg//:deps.bzl", "rules_pkg_dependencies")
load("@aspect_rules_js//js:repositories.bzl", "rules_js_dependencies")

rules_pkg_dependencies()
rules_js_dependencies()

load("@aspect_rules_js//npm:npm_import.bzl", "npm_translate_lock")
load("@build_bazel_rules_nodejs//:index.bzl", "node_repositories", "yarn_install")
load("@rules_nodejs//nodejs:repositories.bzl", "nodejs_register_toolchains")

NODE_JS_VERSION = "14.21.3"
NODE_REPOSITORIES = {
    "14.21.3-darwin_amd64": ("node-v14.21.3-darwin-x64.tar.gz", "node-v14.21.3-darwin-x64", "a024f0dd5a4c1f951b79959c3e991b30a5919a734ab3e197ae0ef439e5a538b5"),
    "14.21.3-darwin_arm64": ("node-v14.21.3-darwin-arm64.tar.gz", "node-v14.21.3-darwin-arm64", "5370cf87e46cef9b0dfd0e3897a056ed414d5e7f8fe241d56dca81206544ede5"),
    "14.21.3-linux_arm64": ("node-v14.21.3-linux-arm64.tar.xz", "node-v14.21.3-linux-arm64", "f06642bfcf0b8cc50231624629bec58b183954641b638e38ed6f94cd39e8a6ef"),
    "14.21.3-linux_amd64": ("node-v14.21.3-linux-x64.tar.xz", "node-v14.21.3-linux-x64", "05c08a107c50572ab39ce9e8663a2a2d696b5d262d5bd6f98d84b997ce932d9a"),
}
NODE_URLS = ["https://asana-oss-cache.s3.amazonaws.com/node/v{version}/{filename}"]

NODE_20_TOOLCHAIN = select({
    "@bazel_tools//src/conditions:linux_x86_64": "@nodejs20_linux_amd64//:node_toolchain",
    "@bazel_tools//src/conditions:linux_aarch64": "@nodejs20_linux_arm64//:node_toolchain",
    "@bazel_tools//src/conditions:darwin_x86_64": "@nodejs20_darwin_amd64//:node_toolchain",
    "@bazel_tools//src/conditions:darwin_arm64": "@nodejs20_darwin_arm64//:node_toolchain",
})

node_repositories(
    node_version = NODE_JS_VERSION,
    yarn_version = "1.22.19",
    node_repositories = NODE_REPOSITORIES,
    node_urls = NODE_URLS,
)

nodejs_register_toolchains(
    name = "nodejs20",
    node_version = "20.5.0",
    node_repositories = {
        "20.5.0-darwin_arm64": ("node-v20.5.0-darwin-arm64.tar.gz", "node-v20.5.0-darwin-arm64", "56d29a7c620415164e6226804cc1eb8eb7b05ea3123b60c86393fabb551bd5ea"),
        "20.5.0-darwin_amd64": ("node-v20.5.0-darwin-x64.tar.gz", "node-v20.5.0-darwin-x64", "3da7e64ac76309cbbb25524bae75cd335fed2795fcbd4f55e3162bcbcec18176"),
        "20.5.0-linux_arm64": ("node-v20.5.0-linux-arm64.tar.xz", "node-v20.5.0-linux-arm64", "afddd830662bdc71f37d39d6cd74104acc663ecd6bbe0fd9264c581ee4f2559b"),
        "20.5.0-linux_amd64": ("node-v20.5.0-linux-x64.tar.xz", "node-v20.5.0-linux-x64", "c12ee9efe21f3ff9909fbf5d7d3780f16c86fad411f13d715016646c766e8213"),
    },
)

npm_translate_lock(
    name = "npm_rulesjs",
    npmrc = "//:.npmrc",
    pnpm_lock = "//:pnpm-lock.yaml",
    pnpm_version = "7.25.0",
)

load("@npm_rulesjs//:repositories.bzl", "npm_repositories")

npm_repositories()

