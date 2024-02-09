load("@aspect_rules_ts//ts:defs.bzl", "ts_project")

ts_project(
    name = "intermediate",
    srcs = ["intermdiate.ts"],
)

ts_project(
    name = "toplevel",
    srcs = ["toplevel.ts"],
    deps = ":intermediate",
)
