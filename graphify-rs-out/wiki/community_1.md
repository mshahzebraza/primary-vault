# Community 1: strip_category_name()

**Members:** 10

## Nodes

- **category_cleanup** (`scripts_category_cleanup_py`, File, degree: 9)
- **cleanup_note()** (`scripts_category_cleanup_py_cleanup_note`, Function, degree: 5)
- **argparse** (`scripts_category_cleanup_py_import_argparse`, Module, degree: 1)
- **pathlib.Path** (`scripts_category_cleanup_py_import_pathlib_path`, Module, degree: 1)
- **re** (`scripts_category_cleanup_py_import_re`, Module, degree: 1)
- **yaml** (`scripts_category_cleanup_py_import_yaml`, Module, degree: 1)
- **load_fm()** (`scripts_category_cleanup_py_load_fm`, Function, degree: 2)
- **main()** (`scripts_category_cleanup_py_main`, Function, degree: 2)
- **save_fm()** (`scripts_category_cleanup_py_save_fm`, Function, degree: 2)
- **strip_category_name()** (`scripts_category_cleanup_py_strip_category_name`, Function, degree: 2)

## Relationships

- scripts_category_cleanup_py → scripts_category_cleanup_py_import_argparse (imports)
- scripts_category_cleanup_py → scripts_category_cleanup_py_import_re (imports)
- scripts_category_cleanup_py → scripts_category_cleanup_py_import_pathlib_path (imports)
- scripts_category_cleanup_py → scripts_category_cleanup_py_import_yaml (imports)
- scripts_category_cleanup_py → scripts_category_cleanup_py_strip_category_name (defines)
- scripts_category_cleanup_py → scripts_category_cleanup_py_load_fm (defines)
- scripts_category_cleanup_py → scripts_category_cleanup_py_save_fm (defines)
- scripts_category_cleanup_py → scripts_category_cleanup_py_cleanup_note (defines)
- scripts_category_cleanup_py → scripts_category_cleanup_py_main (defines)
- scripts_category_cleanup_py_cleanup_note → scripts_category_cleanup_py_load_fm (calls)
- scripts_category_cleanup_py_cleanup_note → scripts_category_cleanup_py_strip_category_name (calls)
- scripts_category_cleanup_py_cleanup_note → scripts_category_cleanup_py_save_fm (calls)
- scripts_category_cleanup_py_main → scripts_category_cleanup_py_cleanup_note (calls)

