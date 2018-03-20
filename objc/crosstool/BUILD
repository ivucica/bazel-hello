# for clang
filegroup(
    name = "toolchain",
    srcs = ["//external:cc_toolchain"],
)

filegroup(
    name = "empty",
    srcs = [],
)

cc_toolchain_suite(
    name = "default-toolchain",
    toolchains = {
        # TODO: this should be local|clang instead of k8|clang. unknown why it
        # has to be k8.
        "k8|clang": ":cc-compiler-local-clang",
        # TODO: this should not be needed, but it's needed for this to work:
        # --apple_crosstool_top=//objc/crosstool:default-toolchain
        # --ios_multi_cpus=x86_64
        # There is no way to override compiler name; it has to be 'compiler'.
        # This CPU also needs to be x86_64 otherwise there is no 'apple'
        # platform definition.
        "ios_x86_64|compiler": ":cc-compiler-local-clang-fake-ios",
    },
)

cc_toolchain(
    name = "cc-compiler-local-clang",
    all_files = ":empty",
    compiler_files = ":empty",
    cpu = "k8", #"local",
    dwp_files = ":empty",
    dynamic_runtime_libs = [":empty"],
    linker_files = ":empty",
    objcopy_files = ":empty",
    static_runtime_libs = [":empty"],
    strip_files = ":empty",
    supports_param_files = 1,
    visibility = ["//visibility:public"],
)

cc_toolchain(
    name = "cc-compiler-local-clang-fake-ios",
    all_files = ":empty",
    compiler_files = ":empty",
    cpu = "ios_x86_64", #"local",
    dwp_files = ":empty",
    dynamic_runtime_libs = [":empty"],
    linker_files = ":empty",
    objcopy_files = ":empty",
    static_runtime_libs = [":empty"],
    strip_files = ":empty",
    supports_param_files = 1,
    visibility = ["//visibility:public"],
)
