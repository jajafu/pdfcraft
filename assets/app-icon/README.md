# PdfCraft app icon

<img src="pdfcraft-small.svg" alt="PdfCraft app icon: a red-orange PDF document tile" width="128">

**Motif:** a red-orange gradient document with a folded corner and white `PDF` lettering,
stacked over a second sheet, with a soft shadow on a transparent background.

**Status (interim):** contributor-original raster artwork (`MIT OR Apache-2.0`). `pdfcraft.svg`
and `pdfcraft-small.svg` are interim raster-embedded wrappers, not vector masters; every PNG,
the `.ico` and the scalable copy are resized from the raster. `pdfcraft.icns` is still the
previous artwork — it needs a macOS `iconutil` run.

**TODO after the upstream merge:** supply a proper vector master, re-run `packaging/icons.sh`
(needs resvg; `iconutil` on macOS for the `.icns`), then `cargo xtask assets --write`.

## Files

| File | What it is |
|---|---|
| `pdfcraft.svg` | the interim master (raster-embedded); a proper vector master is TODO — see above |
| `pdfcraft-small.svg` | a lighter interim master (raster-embedded) for places where size matters, such as this README |
| `pdfcraft-1024.png` | 1024 px render of the interim master; also the runtime Dock icon on macOS |
| `pdfcraft.icns` | macOS icon (16–1024 px) |
| `pdfcraft.ico` | Windows icon (16–256 px), embedded in `pdfcraft.exe` by `apps/pdfcraft/build.rs` |
| `pdfcraft-document.svg` | Windows PDF file icon master: a Lucide document outline, green badge and outlined PDF lettering; no font dependency |
| `pdfcraft-document.ico` | Windows PDF file icon (16–256 px), embedded as resource 2 in `pdfcraft.exe` |
| `hicolor/<n>x<n>/apps/ai.storyteller.pdfcraft.png` | Linux hicolor theme, 16–512 px; the 256 px one is the runtime icon on Windows and Linux |
| `hicolor/scalable/apps/ai.storyteller.pdfcraft.svg` | Linux scalable icon (copy of the master) |

Where it shows: `apps/pdfcraft/src/main.rs` sets the window icon (Dock, taskbar, Alt-Tab, launcher) and the
Wayland app id `ai.storyteller.pdfcraft`; `packaging/linux/ai.storyteller.pdfcraft.desktop` names the
hicolor icon.

Windows PDF files use resource 2 (`"pdfcraft.exe",-2`) when PdfCraft is chosen as the default
reader; the app keeps resource 1. The document outline is adapted from Lucide `file-text`
1.49.0 (ISC); its badge and outlined lettering are original (`MIT OR Apache-2.0`), covered by
[LICENSE-document.txt](LICENSE-document.txt). Both icons are embedded, requiring no runtime
sidecar. This provides a file type icon; first-page thumbnails still need a thumbnail provider.

## Regenerate

```sh
packaging/icons.sh        # needs resvg and python3; iconutil (macOS) for the .icns
cargo xtask assets        # then update the sha256 values in ATTRIBUTION.toml and run with --write
```
