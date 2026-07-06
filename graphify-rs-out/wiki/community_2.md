# Community 2: process_file()

**Members:** 10

## Nodes

- **normalize_property_keys** (`scripts_normalize_property_keys_py`, File, degree: 9)
- **dump_fm()** (`scripts_normalize_property_keys_py_dump_fm`, Function, degree: 2)
- **argparse** (`scripts_normalize_property_keys_py_import_argparse`, Module, degree: 1)
- **pathlib.Path** (`scripts_normalize_property_keys_py_import_pathlib_path`, Module, degree: 1)
- **re** (`scripts_normalize_property_keys_py_import_re`, Module, degree: 1)
- **sys** (`scripts_normalize_property_keys_py_import_sys`, Module, degree: 1)
- **yaml** (`scripts_normalize_property_keys_py_import_yaml`, Module, degree: 1)
- **is_bug_type()** (`scripts_normalize_property_keys_py_is_bug_type`, Function, degree: 2)
- **main()** (`scripts_normalize_property_keys_py_main`, Function, degree: 2)
- **process_file()** (`scripts_normalize_property_keys_py_process_file`, Function, degree: 4)

## Relationships

- scripts_normalize_property_keys_py → scripts_normalize_property_keys_py_import_argparse (imports)
- scripts_normalize_property_keys_py → scripts_normalize_property_keys_py_import_re (imports)
- scripts_normalize_property_keys_py → scripts_normalize_property_keys_py_import_sys (imports)
- scripts_normalize_property_keys_py → scripts_normalize_property_keys_py_import_pathlib_path (imports)
- scripts_normalize_property_keys_py → scripts_normalize_property_keys_py_import_yaml (imports)
- scripts_normalize_property_keys_py → scripts_normalize_property_keys_py_dump_fm (defines)
- scripts_normalize_property_keys_py → scripts_normalize_property_keys_py_is_bug_type (defines)
- scripts_normalize_property_keys_py → scripts_normalize_property_keys_py_process_file (defines)
- scripts_normalize_property_keys_py → scripts_normalize_property_keys_py_main (defines)
- scripts_normalize_property_keys_py_process_file → scripts_normalize_property_keys_py_is_bug_type (calls)
- scripts_normalize_property_keys_py_process_file → scripts_normalize_property_keys_py_dump_fm (calls)
- scripts_normalize_property_keys_py_main → scripts_normalize_property_keys_py_process_file (calls)

