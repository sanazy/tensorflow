# Description:
# TensorFlow SavedModel.

load("//tensorflow:tensorflow.bzl", "cuda_py_test")

# buildifier: disable=same-origin-load
load("//tensorflow:tensorflow.bzl", "tf_py_test")

package(
    # TODO(drpng): change that to //third_party/tensorflow:internal
    # when we have migrated all users.
    default_visibility = ["//visibility:public"],
    licenses = ["notice"],  # Apache 2.0
)

exports_files(["LICENSE"])

py_library(
    name = "saved_model",
    srcs = ["saved_model.py"],
    srcs_version = "PY2AND3",
    visibility = ["//tensorflow:internal"],
    deps = [
        ":builder",
        ":constants",
        ":load",
        ":loader",
        ":main_op",
        ":method_name_updater",
        ":save",
        ":signature_constants",
        ":signature_def_utils",
        ":simple_save",
        ":tag_constants",
        ":utils",
        "//tensorflow/python:util",
    ],
)

py_library(
    name = "constants",
    srcs = ["constants.py"],
    srcs_version = "PY2AND3",
    deps = ["//tensorflow/python:util"],
)

py_library(
    name = "signature_constants",
    srcs = ["signature_constants.py"],
    srcs_version = "PY2AND3",
    deps = ["//tensorflow/python:util"],
)

py_library(
    name = "tag_constants",
    srcs = ["tag_constants.py"],
    srcs_version = "PY2AND3",
    deps = ["//tensorflow/python:util"],
)

py_library(
    name = "builder",
    srcs = [
        "builder.py",
        "builder_impl.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":constants",
        ":utils",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:lib",
        "//tensorflow/python:platform",
        "//tensorflow/python:saver",
        "//tensorflow/python:util",
        "//tensorflow/python:variables",
    ],
)

py_library(
    name = "loader",
    srcs = [
        "loader.py",
        "loader_impl.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":constants",
        ":signature_def_utils",
        ":utils",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:lib",
        "//tensorflow/python:platform",
        "//tensorflow/python:saver",
        "//tensorflow/python:util",
        "//tensorflow/python:variables",
    ],
)

tf_py_test(
    name = "loader_test",
    size = "small",
    srcs = ["loader_test.py"],
    deps = [
        ":builder",
        ":loader",
        ":signature_def_utils",
        ":utils",
        "//tensorflow/python:client",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:control_flow_ops",
        "//tensorflow/python:errors",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:lib",
        "//tensorflow/python:state_ops",
        "//tensorflow/python:training",
        "//tensorflow/python:variables",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "simple_save",
    srcs = [
        "simple_save.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":builder",
        ":signature_constants",
        ":signature_def_utils",
        ":tag_constants",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:lib",
        "//tensorflow/python:util",
    ],
)

py_library(
    name = "main_op",
    srcs = [
        "main_op.py",
        "main_op_impl.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow/python:control_flow_ops",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:lookup_ops",
        "//tensorflow/python:util",
        "//tensorflow/python:variables",
    ],
)

tf_py_test(
    name = "saved_model_test",
    size = "small",
    srcs = ["saved_model_test.py"],
    data = ["//tensorflow/cc/saved_model:saved_model_half_plus_two"],
    tags = ["no_windows"],
    deps = [
        ":builder",
        ":constants",
        ":loader",
        ":main_op",
        ":signature_def_utils",
        ":tag_constants",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:control_flow_ops",
        "//tensorflow/python:errors",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:lib",
        "//tensorflow/python:math_ops",
        "//tensorflow/python:saver_test_utils",
        "//tensorflow/python:session",
        "//tensorflow/python:state_ops",
        "//tensorflow/python:test_ops",
        "//tensorflow/python:training",
        "//tensorflow/python:util",
        "//tensorflow/python:variables",
    ],
)

py_library(
    name = "utils",
    srcs = [
        "utils.py",
        "utils_impl.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":constants",
        ":nested_structure_coder",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:lib",
        "//tensorflow/python:sparse_tensor",
        "//tensorflow/python:util",
    ],
)

tf_py_test(
    name = "utils_test",
    size = "small",
    srcs = ["utils_test.py"],
    deps = [
        ":utils",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:array_ops",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:sparse_tensor",
    ],
)

py_library(
    name = "signature_def_utils",
    srcs = [
        "signature_def_utils.py",
        "signature_def_utils_impl.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":signature_constants",
        ":utils",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:util",
    ],
)

tf_py_test(
    name = "signature_def_utils_test",
    size = "small",
    srcs = ["signature_def_utils_test.py"],
    deps = [
        ":signature_constants",
        ":signature_def_utils",
        ":utils",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:array_ops",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework_for_generated_wrappers",
    ],
)

tf_py_test(
    name = "simple_save_test",
    size = "small",
    srcs = ["simple_save_test.py"],
    deps = [
        ":loader",
        ":signature_constants",
        ":simple_save",
        ":tag_constants",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:variables",
    ],
)

py_library(
    name = "signature_serialization",
    srcs = [
        "signature_serialization.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":revived_types",
        ":signature_constants",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:tensor_spec",
        "//tensorflow/python:util",
        "//tensorflow/python/eager:def_function",
        "//tensorflow/python/eager:function",
        "//tensorflow/python/training/tracking:base",
    ],
)

py_library(
    name = "save",
    srcs = [
        "save.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":builder",
        ":constants",
        ":function_serialization",
        ":nested_structure_coder",
        ":revived_types",
        ":save_options",
        ":signature_constants",
        ":signature_def_utils",
        ":signature_serialization",
        ":tag_constants",
        ":utils",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:array_ops",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:control_flow_ops",
        "//tensorflow/python:dtypes",
        "//tensorflow/python:framework",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:lib",
        "//tensorflow/python:resource_variable_ops",
        "//tensorflow/python:util",
        "//tensorflow/python/eager:context",
        "//tensorflow/python/eager:def_function",
        "//tensorflow/python/eager:function",
        "//tensorflow/python/training/saving:checkpoint_options",
        "//tensorflow/python/training/saving:functional_saver",
        "//tensorflow/python/training/tracking",
        "//tensorflow/python/training/tracking:base",
        "//tensorflow/python/training/tracking:graph_view",
        "//tensorflow/python/training/tracking:util",
    ],
)

tf_py_test(
    name = "save_test",
    srcs = ["save_test.py"],
    tags = ["no_rocm"],
    deps = [
        ":loader",
        ":save",
        ":save_options",
        ":signature_constants",
        ":tag_constants",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:error_interpolation",
        "//tensorflow/python/eager:def_function",
        "//tensorflow/python/eager:test",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "load",
    srcs = [
        "load.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":constants",
        ":function_deserialization",
        ":load_v1_in_v2",
        ":loader",
        ":nested_structure_coder",
        ":revived_types",
        ":utils",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:init_ops",
        "//tensorflow/python:lib",
        "//tensorflow/python:resource_variable_ops",
        "//tensorflow/python:tensor_util",
        "//tensorflow/python:util",
        "//tensorflow/python:variables",
        "//tensorflow/python/distribute:distribute_lib",
        "//tensorflow/python/distribute:distribute_utils",
        "//tensorflow/python/distribute:values",
        "//tensorflow/python/training/tracking",
        "//tensorflow/python/training/tracking:base",
        "//tensorflow/python/training/tracking:graph_view",
        "//tensorflow/python/training/tracking:util",
    ],
)

py_library(
    name = "load_v1_in_v2",
    srcs = [
        "load_v1_in_v2.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":loader",
        ":signature_serialization",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:saver",
        "//tensorflow/python/eager:wrap_function",
        "//tensorflow/python/training/tracking",
    ],
)

cuda_py_test(
    name = "load_test",
    srcs = ["load_test.py"],
    shard_count = 10,
    tags = [
        "no_gpu",  # TODO(b/136560979): flaky
        "no_mac",  # TODO(b/124822121): Re-enable this test.
    ],
    deps = [
        ":load",
        ":save",
        "//tensorflow/python:cond_v2",  # b/118513001
        "//tensorflow/python:constant_op",
        "//tensorflow/python:control_flow_ops",
        "//tensorflow/python:dtypes",
        "//tensorflow/python:lib",
        "//tensorflow/python:tensor_spec",
        "//tensorflow/python:while_v2",  # b/118513001
        "//tensorflow/python/eager:def_function",
        "//tensorflow/python/eager:test",
        "//tensorflow/python/module",
        "//tensorflow/python/training/tracking",
        "@absl_py//absl/testing:parameterized",
    ],
)

tf_py_test(
    name = "load_v1_in_v2_test",
    srcs = ["load_v1_in_v2_test.py"],
    deps = [
        ":builder",
        ":load",
        ":save",
        ":signature_def_utils",
        ":simple_save",
        ":utils",
        "//tensorflow/python:array_ops",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:dtypes",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:lib",
        "//tensorflow/python:resource_variable_ops",
        "//tensorflow/python:session",
        "//tensorflow/python:tensor_spec",
        "//tensorflow/python:variables",
        "//tensorflow/python/eager:def_function",
        "//tensorflow/python/eager:test",
        "//tensorflow/python/training/tracking",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "revived_types",
    srcs = [
        "revived_types.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow/core:protos_all_py",
    ],
)

tf_py_test(
    name = "revived_types_test",
    srcs = ["revived_types_test.py"],
    deps = [
        ":revived_types",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:client_testlib",
    ],
)

py_library(
    name = "function_serialization",
    srcs = [
        "function_serialization.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":nested_structure_coder",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python/eager:def_function",
        "//tensorflow/python/eager:function",
    ],
)

py_library(
    name = "function_deserialization",
    srcs = [
        "function_deserialization.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":nested_structure_coder",
        "//tensorflow/python/eager:def_function",
    ],
)

py_library(
    name = "nested_structure_coder",
    srcs = ["nested_structure_coder.py"],
    deps = [
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:framework",
        "//tensorflow/python:tensor_array_ops",
        "//tensorflow/python/data/ops:dataset_ops",
        "//tensorflow/python/data/ops:iterator_ops",
        "//tensorflow/python/data/ops:optional_ops",
        "//tensorflow/python/distribute:values",
        "//tensorflow/python/ops/ragged",
        "@six_archive//:six",
    ],
)

tf_py_test(
    name = "nested_structure_coder_test",
    srcs = ["nested_structure_coder_test.py"],
    deps = [
        ":nested_structure_coder",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:framework",
        "//tensorflow/python/eager:test",
    ],
)

py_library(
    name = "save_options",
    srcs = ["save_options.py"],
    deps = [
        "@six_archive//:six",
    ],
)

py_library(
    name = "method_name_updater",
    srcs = ["method_name_updater.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":constants",
        ":loader",
        "//tensorflow/python:lib",
        "//tensorflow/python:platform",
        "//tensorflow/python:util",
    ],
)

tf_py_test(
    name = "method_name_updater_test",
    srcs = ["method_name_updater_test.py"],
    deps = [
        ":method_name_updater",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:framework",
        "//tensorflow/python/eager:test",
    ],
)
