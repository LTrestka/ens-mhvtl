# FL1587 Logical Tape Layout

This directory mirrors the OSM mhvtl sample model by storing logical tape
segments instead of a monolithic image.

## Files

- `L1`: first 80-byte VOL1 label block (from `vol1_FL1587.bin`).
- `L2`: second 80-byte header block (first 80 bytes of `fseq2_header.bin`).
- `file1`: first payload segment (`fseq2_payload.bin`, first 262144-byte block).
- `file2`: second payload segment (`fseq2_payload.bin`, remaining block(s)).
- `manifest.json`: ordered segment metadata and block sizes.

## Rebuilding The Layout

Run:

```bash
./scripts/prepare_dump_layout_large.sh
```

This reads:

- `enstorelarge/FL1587_f2/vol1_FL1587.bin`
- `enstorelarge/FL1587_f2/fseq2_header.bin`
- `enstorelarge/FL1587_f2/fseq2_payload.bin`

and writes/refreshes this directory.

## Deterministic Reconstruction

To rebuild a single byte stream from logical pieces:

```bash
cat L1 L2 file1 file2 > FL1587_reconstructed.bin
```

`manifest.json` defines the segment order and block sizes for scripted
reconstruction with `dd` or equivalent tools.
