help2man = find_program('help2man', required: false)
groff = find_program('groff', required: false)
robodoc = find_program('robodoc', required: false)

if help2man.found()
cygport_1 = custom_target('cygport.1',
                          input: cygport_inplace,
                          output: 'cygport.1',
                          depend_files: cygparts,
                          command: [help2man, '-o', '@OUTPUT@', '--no-info',
                                    '--name=Cygwin source packaging tool', '@INPUT@'],
                          install: true,
                          install_dir: man1dir)

if groff.found()
cygport_1_html = custom_target('cygport.1.html',
                               input: cygport_1,
                               output: 'cygport.1.html',
                               command: [groff, '-t', '-mandoc', '-Thtml', '@INPUT@'],
                               capture: true,
                               install: true,
                               install_dir: join_paths(htmldir, 'manual'))
endif
endif

if robodoc.found()
robodoc_cmd = find_program('robodoc.sh')
cygport_manual = custom_target('cygport-manual',
                               input: 'robodoc.rc',
                               output: 'manual',
                               depend_files: cygport_in + cygclasses + cygclass_top + cygparts + datadocs,
                               command: [robodoc_cmd,
                                         meson.source_root(), meson.build_root()],
                               install: true,
                               install_dir: htmldir)
install_data('index.html',
             install_dir: join_paths(htmldir, 'manual'))
endif
