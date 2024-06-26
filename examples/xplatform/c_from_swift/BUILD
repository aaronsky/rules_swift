load(
    "//swift:swift.bzl",
    "swift_binary",
    "swift_interop_hint",
    "swift_library",
)

licenses(["notice"])

# 1. This library has some C++ code that you want to interact with from Swift...
cc_library(
    name = "counter",
    srcs = ["counter.cc"],
    hdrs = ["counter.h"],
    linkstatic = True,
)

# 2. ...but Swift can't import C++ yet, so we implement a wrapper API in C. Use
# the `swift_interop_hint` rule to enable module map generation and provide the
# module name for these headers, since `cc_library` doesn't do enable this by
# default.
cc_library(
    name = "c_counter",
    srcs = ["c_counter.cc"],
    hdrs = ["c_counter.h"],
    aspect_hints = [":c_counter_swift_hint"],
    linkstatic = True,
    deps = [":counter"],
)

swift_interop_hint(
    name = "c_counter_swift_hint",
    module_name = "CCounter",
)

# 3. The Swift library then depends on the `cc_library`. This causes a
# Swift-compatible module map to be created for the `cc_library` so that the
# Swift code can import it.
swift_library(
    name = "swift_counter",
    srcs = ["Counter.swift"],
    module_name = "Counter",
    deps = [":c_counter"],
)

# 4. Finally, this binary is a straightforward target with no surprises. It just
# imports the Swift `Counter` module above.
swift_binary(
    name = "c_from_swift",
    srcs = ["main.swift"],
    module_name = "main",
    deps = [":swift_counter"],
)
