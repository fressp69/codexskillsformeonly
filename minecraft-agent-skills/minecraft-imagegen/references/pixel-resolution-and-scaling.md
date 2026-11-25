# Pixel-art resolution and nearest-neighbor scaling

Use this workflow when the deliverable is a **Minecraft item sprite** or another deliberately pixelated resource-pack texture. It is not the default for paintings, photos, screenshots or release banners.

## Stage 1 — Generate and review a concept

Generate a high-resolution square image that *looks* like authentic 32×32 pixel art by default (or the chosen 16×16/64×64 style). Specify a flat isolated sprite, visible square pixel clusters, clean stepped silhouette, limited palette, no smooth gradients or anti-aliasing, no background scene and real transparency where needed. The output may be 1024×1024 or another supported generation size; it is a concept, not the native texture.

Show the concept and get user approval before conversion. Apply requested visual edits at this stage, keeping approved details unchanged. If the user supplies approved artwork, explicitly asks to downscale the current image, or authorizes a final texture in one pass, proceed without another approval request. Otherwise stop after the concept and wait for feedback. Do not integrate it into a pack without authorization.

## Stage 2 — Choose a native resolution

- **Respect the user's exact dimensions first.**
- **16×16:** vanilla-like economy, very simple silhouettes.
- **32×32:** default when the user requests a custom item icon without specifying a resolution; a balanced choice for SkillsSMP items such as Jet Fuel.
- **64×64:** extra art detail when the pack style supports it.

Keep the intended slot size in mind. A larger generated concept (e.g. 1024×1024) is **not** already a 32×32 texture, even if its pixels look blocky.

## Stage 3 — Resample the approved source deliberately

1. Start from a clean isolated subject. If transparency is required, request or create a real alpha channel; a black or checkerboard background is not automatically transparent.
2. Keep the whole silhouette within the frame. If the source is not square, fit it proportionally on a transparent square canvas **before** reducing resolution. Do not stretch or crop unless requested.
3. Downscale to the chosen native dimensions with **nearest-neighbor** (`PIL.Image.Resampling.NEAREST`, or the equivalent pixel-preserving algorithm). Avoid antialiasing/blur for Minecraft pixel textures.
4. Inspect the exact-size result. Downscaling discards information: nearest-neighbor preserves hard pixel boundaries, but can lose small details or retain unwanted colors from an already smoothed source.
5. Inspect single-pixel noise, broken contours and halos. Do not silently repaint approved artwork; obtain approval for visual changes or report the defect. Prefer revising the concept before downscaling. If the user supplies a retouched native-size PNG, preserve its pixels and avoid unnecessary resampling.
6. Save the **actual game texture** as a lossless PNG. Always create a separate **512×512 PNG preview** by upscaling the finished native PNG with nearest-neighbor so every source pixel appears as a hard-edged square. For 16×16 use 32× enlargement, for 32×32 use 16×, and for 64×64 use 8×. Never substitute the enlarged preview for the native file.
7. Verify actual dimensions, color mode and alpha rather than relying on filenames. If the alpha source was absent, state that transparency was not verified instead of claiming it.

## Stage 4 — Deliver both files (reproducible Pillow example)

Run this only after review or explicit authorization. The example assumes an approved source with genuine alpha when transparency is required; converting to RGBA alone does not remove an opaque background.

```python
from PIL import Image
from pathlib import Path

source = Image.open("approved_concept.png").convert("RGBA")
size = 32  # user-specified size overrides this default

# Contain the source without distortion or cropping. Leave transparent padding.
scale = min(size / source.width, size / source.height)
new_w = max(1, round(source.width * scale))
new_h = max(1, round(source.height * scale))
sprite = source.resize((new_w, new_h), resample=Image.Resampling.NEAREST)
canvas = Image.new("RGBA", (size, size), (0, 0, 0, 0))
canvas.alpha_composite(sprite, ((size-new_w)//2, (size-new_h)//2))

native_path = Path(f"item_{size}x{size}.png")
canvas.save(native_path, "PNG")

# Preview only: fixed 512×512, derived from the saved native file.
preview_path = Path(f"item_{size}x{size}_preview_512x512.png")
with Image.open(native_path) as native:
    native.resize((512, 512), Image.Resampling.NEAREST).save(preview_path, "PNG")
with Image.open(preview_path) as preview:
    assert preview.size == (512, 512)

verified = Image.open(native_path)
assert verified.size == (size, size)
assert verified.mode == "RGBA"
# RGBA mode supports transparency; it does NOT prove any pixels are transparent.
print(native_path, verified.size, verified.getextrema()[3])
```

For a highly rectangular source, reducing it into a square may leave substantial padding. Prefer a tighter original crop around the object (without cutting off its silhouette) or ask for a more suitably framed source. Never upscale with a smoothing filter after the pixel grid has been established.

## Handoff checklist

- Native PNG pixel size checked, preferably 16×16, 32×32 or 64×64 for item textures.
- Approved concept (or explicit review bypass) established; nearest-neighbor used for both reduction and the mandatory 512×512 preview.
- Full recognizable silhouette; no accidental cropping/stretching.
- Actual transparency verified if requested, not inferred from a black background.
- Native icon legible at inventory scale; edge defects inspected and cleaned if necessary.
- Both files exist and are delivered with separate, clearly labelled links/paths: native game PNG and verified 512×512 preview PNG. If file access or writing is unavailable, explain the blocker instead of inventing paths.
