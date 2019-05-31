# NO-AUTO-UPGRADE

common_inc = include_directories('.')

common_sources = []

sources = files(
  'list-box-helper.c',
)

libwidgets = static_library(
  'widgets',
  sources: sources,
  include_directories: top_inc,
  dependencies: common_deps
)
libwidgets_dep = declare_dependency(
  include_directories: common_inc,
  link_with: libwidgets
)

sources = common_sources + files(
  'cc-util.c'
)

deps = common_deps + [
  dependency('fontconfig')
]

deps = common_deps

libdevice = static_library(
  'device',
  sources: sources,
  include_directories: top_inc,
  dependencies: deps
)

libdevice_dep = declare_dependency(
  include_directories: common_inc,
  link_with: libdevice
)

