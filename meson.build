project('libpsl', 'c', version : '0.20.2')

cc = meson.get_compiler('c')

add_project_arguments('-DBUILDING_PSL', language : 'c')

python3 = import('python3').find_python()

psl_file = files('list/public_suffix_list.dat')

psl_version = meson.project_version()
psl_version_tokens = psl_version.split('.')
psl_version_major = psl_version_tokens[0].to_int()
psl_version_minor = psl_version_tokens[1].to_int()
psl_version_patch = psl_version_tokens[2].to_int()
result = run_command(python3, '-c', 'import sys;\n' +
  'sys.stdout.write("0x{:02x}{:02x}{:02x}".format(@0@, @1@, @2@))'
  .format(psl_version_major, psl_version_minor, psl_version_patch)
)
if result.returncode() != 0
  error('Unable to generate version number: ' + result.stdout() + result.stderr())
endif
psl_version_number = result.stdout()

config_inc = include_directories('.')
header_inc = include_directories('include')

psl_conf = configuration_data()
psl_conf.set_quoted('PACKAGE_VERSION', psl_version)
psl_conf.set('BUILTIN_GENERATOR_LIBICU', 1)
if host_machine.system() == 'windows'
  psl_conf.set('_WIN32', 1)
endif
if cc.has_header('alloca.h')
  psl_conf.set('HAVE_ALLOCA_H', 1)
endif
configure_file(output : 'config.h', configuration : psl_conf)
add_project_arguments('-DHAVE_CONFIG_H', language : 'c')

subdir('include')
subdir('src')
