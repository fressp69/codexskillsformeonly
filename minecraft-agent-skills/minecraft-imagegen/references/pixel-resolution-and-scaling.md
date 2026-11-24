# Pixel-art resolution and nearest-neighbor scaling

Use this workflow when the deliverable is a **Minecraft item sprite** or another deliberately pixelated resource-pack texture. It is not the default for paintings, photos, screenshots or release banners.

## Choose a native resolution

- **Respect the user's exact dimensions first.**
- **16×16:** vanilla-like economy, very simple silhouettes.
- **32×32:** default when the user requests a custom item icon without specifying a resolution; a balanced choice for SkillsSMP items such as Jet Fuel.
- **64×64:** extra art detail when the pack style supports it.

Keep the intended slot size in mind. A larger generated concept (e.g. 1024×1024) is **not** already a 32×32 texture, even if its pixels look blocky.

## Resample deliberately

1. Start from a clean isolated subject. If transparency is required, request or create a real alpha channel; a black or checkerboard background is not automatically transparent.
2. Keep the whole silhouette within the frame. If the source is not square, fit it proportionally on a transparent square canvas **before** reducing resolution. Do not stretch or crop unless requested.
3. Downscale to the chosen native dimensions with **nearest-neighbor** (`PIL.Image.Resampling.NEAREST`, or the equivalent pixel-preserving algorithm). Avoid antialiasing/blur for Minecraft pixel textures.
4. Inspect the exact-size result. Downscaling discards information: nearest-neighbor preserves hard pixel boundaries, but can lose small details or retain unwanted colors from an already smoothed source.
5. If needed, manually clean single-pixel noise, broken contours and halos; ensure a consistent pixel grid. Prefer simplifying the source before downscaling over trying to recover details afterward.
6. Save the **actual game texture** as a lossless PNG. If showing a larger preview, upscale the finished native PNG with nearest-neighbor so every source pixel appears as a hard-edged square; never substitute the enlarged preview for the native file.
7. Verify actual dimensions, color mode and alpha rather than relying on filenames. If the alpha source was absent, state that transparency was not verified instead of claiming it.

## Reproducible Python (Pillow)

```python
from PIL import Image
from pathlib import Path

source = Image.open("jet_fuel_concept.png").convert("RGBA")
size = 32  # user-specified size overrides this default

# Contain the source without distortion or cropping. Leave transparent padding.
scale = min(size / source.width, size / source.height)
new_w = max(1, round(source.width * scale))
new_h = max(1, round(source.height * scale))
sprite = source.resize((new_w, new_h), resample=Image.Resampling.NEAREST)
canvas = Image.new("RGBA", (size, size), (0, 0, 0, 0))
canvas.alpha_composite(sprite, ((size-new_w)//2, (size-new_h)//2))

native_path = Path(f"jet_fuel_{size}x{size}.png")
canvas.save(native_path, "PNG")

# Preview only: 16× enlargement of the completed native pixel grid.
preview = canvas.resize((size * 16, size * 16), Image.Resampling.NEAREST)
preview.save(f"jet_fuel_{size}x{size}_preview.png", "PNG")

verified = Image.open(native_path)
assert verified.size == (size, size)
assert verified.mode == "RGBA"
# RGBA mode supports transparency; it does NOT prove any pixels are transparent.
print(native_path, verified.size, verified.getextrema()[3])
```

For a highly rectangular source, reducing it into a square may leave substantial padding. Prefer a tighter original crop around the object (without cutting off its silhouette) or ask for a more suitably framed source. Never upscale with a smoothing filter after the pixel grid has been established.

## Handoff checklist

- Native PNG pixel size checked, preferably 16×16, 32×32 or 64×64 for item textures.
- Nearest-neighbor used for both reduction and any enlarged preview.
- Full recognizable silhouette; no accidental cropping/stretching.
- Actual transparency verified if requested, not inferred from a black background.
- Native icon legible at inventory scale; edge defects inspected and cleaned if necessary.
- Separate filenames for game texture and magnified inspection preview.
