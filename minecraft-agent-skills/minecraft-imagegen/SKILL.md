---
name: minecraft-imagegen
description: "Generate or edit Minecraft raster assets such as pack icons, promo art, concept textures, thumbnails, banners, and UI mockups. Use when the deliverable is a bitmap image rather than JSON, SVG, or code-native assets."
---

# Minecraft Image Generation Skill

Use this skill when a Minecraft project needs new raster art or a visual concept
that will later be refined into a resource pack, release post, store listing, or
server brand asset.

## Scope

### Routing Boundaries
- `Use when`: the task is generating or editing a bitmap image for a Minecraft project, such as `pack.png`, release art, store thumbnails, concept textures, UI mockups, or server/banner art.
- `Do not use when`: the task is deterministic resource-pack implementation work such as `pack.mcmeta`, block/item model JSON, blockstates, fonts, sounds, or shader files (`minecraft-resource-pack`).
- `Do not use when`: the task is vector/code-native UI, an existing SVG/logo system, or non-image code/assets.
- `Do not use when`: the current host does not expose built-in image generation or an equivalent image-editing tool.

### References

- Read [prompt patterns](references/prompt-patterns.md) for an underspecified request or a generation/edit prompt template.
- Read [asset recipes](references/asset-recipes.md) for a pack icon, release banner, server header, or texture concept sheet.
- For pixel-art item assets, follow [pixel resolution and nearest-neighbor scaling](references/pixel-resolution-and-scaling.md) to produce a native-size texture and crisp enlarged preview without blur.
- Use `scripts/scaffold-asset-brief.sh` only when a saved brief is useful for stakeholder feedback or repeated rounds; a clear image request can proceed directly.
- Invoke the helper by its absolute installed path from the project workspace. Relative `--out` values resolve from that workspace. When running from the installed skill directory, pass an absolute `--out` project path or set `CODEX_WORKSPACE_ROOT`.

---

## Default Execution

- If the current host does not expose built-in image generation or an equivalent image-editing tool, stop and tell the user this skill is unavailable on that host; offer prompt/brief preparation or a host with an available image-generation tool.
- Use the built-in `image_gen` tool by default when the host supports it.
- Match the requested deliverable: complete a requested asset, or produce concepts when the user asks for exploration. Do not require a separate concept approval for a clear generation or edit request.
- The built-in image generation workflow supports fresh generations and edits against existing local/reference images; prefer that over describing a manual paint-over process.
- Save a requested project asset at the intended workspace path when the host exposes the output file; otherwise return the generated image and state that a local save could not be verified.
- Preserve existing assets non-destructively by using versioned filenames unless the user explicitly asked to overwrite.
- If editing a local image, load or attach it first so the image is visible to the agent before requesting an edit.

---

## Good Use Cases

- `pack.png` concepts or replacements for mods, datapacks, or resource packs
- Release-banner art for GitHub, Modrinth, CurseForge, or social posts
- Texture look-dev references that will be cleaned up manually into final pixel art
- Server logos, banners, splash artwork, or rules-screen art
- HUD/menu mockups for plugin or mod UX planning
- Promo sheets that show blocks, mobs, or themed environments in-context

---

## Workflow

1. Use the request to identify the asset type, target dimensions, output path, and whether this is a generation or edit. Inspect the existing image for an edit; gather style references only when needed.
2. Generate the requested asset using the available tool. Describe the subject, composition, Minecraft style, and constraints. For an edit, state the change and what must remain unchanged.
3. For a Minecraft item or other pixel-art texture, resize the generated art to the user's preferred **native resolution** (commonly 16×16, 32×32, or 64×64; for custom item icons with no stated preference, default to 32×32). Use **nearest-neighbor resampling**, never bilinear/bicubic smoothing, for this pixel-texture workflow. Preserve an existing alpha channel, center/contain the entire sprite, and inspect the actual native-size pixels. See [pixel resolution and scaling](references/pixel-resolution-and-scaling.md). This is not a general resizing rule for photographs, banners, or painterly artwork.
4. Inspect the result at the intended display size. Correct lost details, jagged silhouette breaks, stray pixels or unwanted edge halos. Nearest-neighbor keeps hard boundaries but cannot restore detail lost when shrinking or fix an already anti-aliased source.
5. Save or return the native-resolution PNG and, when useful, a separate **nearest-neighbor enlarged preview** (e.g. 32×32 → 512×512). Verify the actual file dimensions and alpha channel; do not mistake a preview for the texture. Complete pixel cleanup, tiling, and pack references when integration is in scope. Additional skills are optional.

---

## Asset-Specific Guidance

### Pack Icons

- Design for square cropping and tiny-size readability.
- Keep the silhouette bold and text minimal.
- Check readability at `64x64`; that is a useful preview size, not a required `pack.png` resolution. Use the project's target dimensions and the host's supported image-editing workflow.

### Texture Concepts

- Ask for flat, front-on presentation with even lighting and minimal perspective.
- State whether the texture should feel vanilla-faithful, noisy/gritty, hand-painted, or stylized.
- Assume manual cleanup before shipping. Generated textures are best used as concept or paint-over references, not automatic drop-ins.

### UI Mockups

- Reserve negative space for labels, slots, and status text.
- Keep text large and high-contrast.
- Call out whether the mockup should feel vanilla, modded-tech, fantasy, or admin-panel inspired.

### Promo Art and Thumbnails

- Leave copy-safe negative space for release titles or taglines.
- Avoid tiny text and clutter that will collapse on mobile or store cards.
- Specify whether the output should show gameplay-like framing, hero artwork, or a clean showcase layout.

---

## Review Checklist

- The image reads clearly at the actual target size.
- For pixel-art textures, native PNG dimensions are confirmed; nearest-neighbor was used for resizing and previews, and existing transparency was preserved.
- Any text is spelled correctly and positioned as requested.
- No extra logos, watermarks, or unrelated objects were introduced.
- The style matches the requested Minecraft context.
- For texture concepts, the result looks easy to paint over, simplify, or tile manually.

---
