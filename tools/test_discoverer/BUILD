load(
    "//swift:swift_binary.bzl",
    "swift_binary",
)

swift_binary(
    name = "test_discoverer",
    srcs = [
        "DiscoveredTests.swift",
        "SymbolCollector.swift",
        "SymbolGraphTestPrinter.swift",
        "SymbolKitExtensions.swift",
        "TestDiscoverer.swift",
        "TestPrinterCommon.swift",
    ],
    visibility = ["//visibility:public"],
    deps = [
        "@com_github_apple_swift_argument_parser//:ArgumentParser",
        "@com_github_apple_swift_docc_symbolkit//:SymbolKit",
    ],
)
