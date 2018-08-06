suffixes_dafsa = custom_target('suffixes-dafsa',
  input : psl_file,
  output : 'suffixes_dafsa.inc',
  command : [python3, files('psl-make-dafsa'), '--output-format=cxx+', '@INPUT@', '@OUTPUT@']
)

psl_sources = [
  'psl.c',
  'lookup_string_in_fixed_set.c',
  suffixes_dafsa
]

libpsl = library('psl', psl_sources,
  include_directories : [config_inc, header_inc],
  install : true
)

pkg = import('pkgconfig')
pkg.generate(name: meson.project_name(),
  description: 'Public Suffix List C library',
  libraries: [libpsl]
)
