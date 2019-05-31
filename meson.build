# NO-AUTO-UPGRADE

project(
  'xfce4-datetime-setter', 'c',
        version : '3.32.2',
        license : 'GPL2+',
  meson_version : '>= 0.48.0'
)

datetime_setter_prefix = get_option('prefix')
datetime_setter_bindir = join_paths(datetime_setter_prefix, get_option('bindir'))
datetime_setter_datadir = join_paths(datetime_setter_prefix, get_option('datadir'))
datetime_setter_libexecdir = join_paths(datetime_setter_prefix, get_option('libexecdir'))
datetime_setter_localedir = join_paths(datetime_setter_prefix, get_option('localedir'))
datetime_setter_mandir = join_paths(datetime_setter_prefix, get_option('mandir'))
datetime_setter_sysconfdir = join_paths(datetime_setter_prefix, get_option('sysconfdir'))

datetime_setter_pkgdatadir = join_paths(datetime_setter_datadir, meson.project_name())
datetime_setter_desktopdir = join_paths(datetime_setter_datadir, 'applications')
datetime_setter_icondir = join_paths(datetime_setter_datadir, 'icons')
datetime_setter_schemadir = join_paths (datetime_setter_datadir, 'glib-2.0', 'schemas')

datetime_setter_gettext = meson.project_name() + '-2.0'

host_is_linux = host_machine.system().contains('linux')
host_is_linux_not_s390 = host_is_linux and not host_machine.cpu().contains('s390')

cc = meson.get_compiler('c')

config_h = configuration_data()

# defines
set_defines = [
  # package
  ['PACKAGE', meson.project_name()],
  ['PACKAGE_VERSION', meson.project_version()],
  ['VERSION', meson.project_version()],
  # i18n
  ['GETTEXT_PACKAGE', datetime_setter_gettext]
]

foreach define: set_defines
  config_h.set_quoted(define[0], define[1])
endforeach

# compiler flags
common_flags = ['-DHAVE_CONFIG_H']

# Only add this when optimizing is enabled (default)
optimized_src = '''
  #if __OPTIMIZE__ == 0
  #error No optimization
  #endif
'''

datetime_setter_optimized = get_option('buildtype').contains('optimized') and cc.compiles(optimized_src)

if datetime_setter_optimized
  common_flags += '-Wp,-D_FORTIFY_SOURCE=2'
endif


add_project_arguments(common_flags, language: 'c')


libxfce4ui_dep = dependency('libxfce4ui-2', version: '>= 4.13.0')
gdk_pixbuf_dep = dependency('gdk-pixbuf-2.0', version: '>= 2.23.0')
gio_dep = dependency('gio-2.0')
glib_dep = dependency('glib-2.0', version: '>= 2.53.0')
libxml_dep = dependency('libxml-2.0')
x11_dep = dependency('x11')

m_dep = cc.find_library('m')

common_deps = [
  gio_dep,
  glib_dep,
  dependency('gio-unix-2.0'),
  dependency('gthread-2.0'),
  dependency('gtk+-3.0', version: '>= 3.22.20')
]

# Check for info panel
datetime_setter_libexecdir = get_option('datetime_setter_libexecdir')
if datetime_setter_libexecdir == ''
  datetime_setter_libexecdir = datetime_setter_libexecdir
endif

gnome = import('gnome')
i18n = import('i18n')
pkg = import('pkgconfig')

desktop_conf = configuration_data()
desktop_conf.set('VERSION', meson.project_version())

po_dir = join_paths(meson.source_root(), 'po')
its_dir = join_paths(meson.source_root(), 'gettext')

top_inc = [ include_directories('.'), include_directories('./stubs'), include_directories('./libgnome-desktop') ]

subdir('po')
subdir('panels')
subdir('xfce')


configure_file(
  output: 'config.h',
  configuration: config_h
)

output = ''
output += '\n        ' + meson.project_name() + ' - ' + meson.project_version() + '\n'
output += '    ===================================\n'
output += ' Options \n'
output += '     gnome-session libexecdir ................... ' + datetime_setter_libexecdir + '\n'
output += '     Optimized .................................. ' + datetime_setter_optimized.to_string() + '\n'

message(output)
