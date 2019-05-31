xfce_datetime_sources = [
  'datetime-dialog.c',
  'main.c',
]

xfce_datetime_c_args = [
  '-DHAVE_CONFIG_H',
]

xfce_datetime_deps = [
  libxfce4ui_dep,
]

xfce_datetime_exe = executable(
  'xfce4-datetime-settings',
  xfce_datetime_sources,
  dependencies: xfce_datetime_deps,
  include_directories: top_inc,
  c_args: xfce_datetime_c_args,
  install: true,
  install_dir: datetime_setter_bindir,
)
