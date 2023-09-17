load("@aspect_rules_ts//ts:proto.bzl", "ts_proto_library")
load("@rules_proto//proto:defs.bzl", "proto_library")
load("@npm_rulesjs//:defs.bzl", "npm_link_all_packages")


proto_library(
    name = "settings_proto",
    srcs = ["settings.proto"],
)

ts_proto_library(
    name = "settings_ts",
    proto = ":settings_proto",
    node_modules = "//:node_modules",
    copy_files = False,
    has_services = False,
)

npm_link_all_packages(name = "node_modules")
