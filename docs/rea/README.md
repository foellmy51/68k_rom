# REA: m68k raw-binary patch

`rea-m68k-raw-binary.patch` adds `m68k` as a headerless raw-binary architecture
to [morluto/rea](https://github.com/morluto/rea) 6.4.0 (Ghidra language
`68000:BE:32:default`, 2-byte entry alignment, 32-bit address width; Hopper
declines it).

Apply to a REA checkout:

    git am docs/rea/rea-m68k-raw-binary.patch   # from the REA repo
    npm ci && npm run build:cached
    export GHIDRA_INSTALL_DIR=/path/to/ghidra_12.1.x_PUBLIC
    rea doctor --provider ghidra
    rea inspect rom.bin --target-format raw-binary --architecture m68k \
        --entry-point 0x0 --provider ghidra --json

Status: typecheck, lint and unit tests pass. Not yet verified against a real
Ghidra. A ROM starting with a vector table (SP, reset PC) gets an `entry`
function seeded at the mapped start; see `docs/raw-binary.md` in the patch.
