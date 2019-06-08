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

resource_data = files(
  'datetime-dialog.ui',
)

resources = gnome.compile_resources(
  'datetime-dialog-resources',
  'datetime-dialog.gresource.xml',
  c_name: 'datetime_dialog',
  dependencies: resource_data,
  export: true
)


xfce_datetime_exe = executable(
  'xfce4-datetime-settings',
  xfce_datetime_sources,
  dependencies: [ xfce_datetime_deps, libwidgets_dep, datetime_panel_dep, m_dep ],
  sources: sources + resources,
  include_directories: top_inc,
  c_args: xfce_datetime_c_args,
  install: true,
  install_dir: datetime_setter_bindir,
)
