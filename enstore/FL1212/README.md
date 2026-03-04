# FL1212 Logical Tape Layout

This directory mirrors the OSM mhvtl sample model by storing logical tape
segments that can be deterministically reconstructed later.

## Files

- `L1`: first 80-byte label/header block (from `vol1_FL1212.bin`).
- `L2`: second 80-byte header block.
  - In this dataset, `vol1_FL1212.bin` contains one 80-byte block, so `L2` is
    intentionally mirrored from `L1` to keep a stable two-label layout.
- `file1`: first payload segment (`fseq2_payload.bin`, first 1 MiB block).
- `file2`: remaining payload segment(s) (`fseq2_payload.bin`, blocks after
  `file1`).
- `manifest.json`: block sizes and ordered segment metadata.

## Rebuilding The Layout

Run:

```bash
./scripts/prepare_dump_layout.sh
```

This reads:

- `enstore/FL1212_f2/vol1_FL1212.bin`
- `enstore/FL1212_f2/fseq2_payload.bin`

and writes/refreshes this directory.

## Deterministic Reconstruction

To reconstruct a single byte stream from the logical pieces:

```bash
cat L1 L2 file1 file2 > FL1212_reconstructed.bin
```

The segment order and block assumptions are also encoded in
`manifest.json` for scripted reconstruction with `dd` or equivalent tools.
