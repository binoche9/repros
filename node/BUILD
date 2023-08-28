load("@aspect_rules_js//js:defs.bzl", "js_binary", "js_image_layer")
load("@io_bazel_rules_pkg//:pkg.bzl", "pkg_tar")

js_binary(
    name = "node_modules",
    data = [
        "//:node_modules/iconv-lite",
    ],
    entry_point = "fake.js",
)

js_image_layer(
    name = "node_modules_layer",
    binary = ":node_modules",
)

filegroup(
    name = "node_modules_tar",
    srcs = [":node_modules_layer"],
    output_group = "node_modules",
)
