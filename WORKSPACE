# Base libraries required by bazel to install rules
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive") # The second string is a _rule_

http_archive(
    name = "bazel_skylib",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-skylib/releases/download/1.3.0/bazel-skylib-1.3.0.tar.gz",
        "https://github.com/bazelbuild/bazel-skylib/releases/download/1.3.0/bazel-skylib-1.3.0.tar.gz",
    ],
    sha256 = "74d544d96f4a5bb630d465ca8bbcfe231e3594e5aae57e1edbf17a6eb3ca2506",
)
load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")
bazel_skylib_workspace()

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")


# Rules for javascript + typescript

# Rules JS
http_archive(
    name = "aspect_rules_js",
    sha256 = "f58d7be1bb0e4b7edb7a0085f969900345f5914e4e647b4f0d2650d5252aa87d",
    strip_prefix = "rules_js-1.8.0",
    url = "https://github.com/aspect-build/rules_js/archive/refs/tags/v1.8.0.tar.gz",
)

load("@aspect_rules_js//js:repositories.bzl", "rules_js_dependencies")

rules_js_dependencies()

# Rules nodejs
load("@rules_nodejs//nodejs:repositories.bzl", "nodejs_register_toolchains")

nodejs_register_toolchains(
    name = "nodejs",
    node_version = "16.13.0",
)


# Setup/fetch depencencies defined on the pnpm-lock.yaml

load("@aspect_rules_js//npm:npm_import.bzl", "npm_translate_lock")

npm_translate_lock(
    name = "npm",
    pnpm_lock = "//:pnpm-lock.yaml",
    lifecycle_hooks_execution_requirements = {
        "canvas@2.10.2": ["no-sandbox"],
    },
    lifecycle_hooks_envs = {
        "canvas@2.10.2" :[
            'CPATH=/opt/homebrew/include',
            'LIBRARY_PATH=/opt/homebrew/lib',
            'PATH=/opt/homebrew/bin:/usr/bin:/bin',
        ], 
    },
)

load("@npm//:repositories.bzl", "npm_repositories")

npm_repositories()
