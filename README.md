# ens-mhvtl

This repository now stores Enstore samples as logical tape segments instead of
pre-generated raw tape images.

For `FL1212`, the OSM-style layout is:

- `enstore/FL1212/L1`
- `enstore/FL1212/L2`
- `enstore/FL1212/file1`
- `enstore/FL1212/file2`
- `enstore/FL1212/manifest.json`

`scripts/prepare_dump_layout.sh` converts legacy inputs from
`enstore/FL1212_f2/` into that layout using file-only `dd` operations. The
script does not run tests, does not access `/dev` tape devices, and does not
perform tape library operations.

For `FL1587` (EnstoreLarge), the OSM-style layout is:

- `enstorelarge/FL1587/L1`
- `enstorelarge/FL1587/L2`
- `enstorelarge/FL1587/file1`
- `enstorelarge/FL1587/file2`
- `enstorelarge/FL1587/manifest.json`

`scripts/prepare_dump_layout_large.sh` converts legacy inputs from
`enstorelarge/FL1587_f2/` into that layout using file-only `dd` operations.
