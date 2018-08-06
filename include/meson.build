header_conf = configuration_data()
header_conf.set('LIBPSL_VERSION', psl_version)
header_conf.set('LIBPSL_VERSION_MAJOR', psl_version_major)
header_conf.set('LIBPSL_VERSION_MINOR', psl_version_minor)
header_conf.set('LIBPSL_VERSION_PATCH', psl_version_patch)
header_conf.set('LIBPSL_VERSION_NUMBER', psl_version_number)
header_conf.set10('PSL_STATIC', get_option('default_library') == 'static')

configure_file(input : 'libpsl.h.in',
  output : 'libpsl.h',
  configuration : header_conf,
  install_dir : get_option('includedir'))
