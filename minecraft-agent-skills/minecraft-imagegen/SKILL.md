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
- For Minecraft pixel-art textures, use the staged concept → user review → native downscale → dual-output workflow below by default. A direct request to downscale an existing approved image already satisfies concept review; an explicit request to skip review or deliver the finished texture immediately also authorizes proceeding. For other raster assets, match the requested deliverable without imposing a separate concept approval.
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
3. For Minecraft pixel-art textures, follow the mandatory staged workflow below and the [pixel resolution and scaling guide](references/pixel-resolution-and-scaling.md). For other assets, inspect and deliver at the requested dimensions.
4. Keep resource-pack integration separate from art approval. Only write pack assets/model references when integration is explicitly requested or already authorized by the task. Use `minecraft-resource-pack` for that implementation.

### Required Minecraft pixel-art texture workflow

**Generate concept → user review → nearest-neighbor downscale → deliver native PNG + 512×512 preview.**

1. **Concept art:** Ask image generation for a high-resolution rendering (e.g. 1024×1024, or the available tool's square output size) that visually resembles a genuine 32×32 pixel-art sprite by default. Adapt the apparent pixel grid to 16×16 or 64×64 if the intended native style calls for it. Use a single isolated item, readable silhouette, deliberate square pixels, limited palette, hard stepped edges, no smoothing, no scene, no text, and real transparency where appropriate. The concept's file resolution is not its apparent pixel grid.
2. **Review:** Show the concept first. Wait for the user's approval or requested edits before downscaling. Preserve approved details across revisions; regenerate only when an actual visual change is requested. A user-provided final sprite or explicit downscale request is already approval to process that source. Do not silently insert a concept into a pack. An explicit all-in-one final-delivery request can bypass the separate review turn.
3. **Native conversion:** Work from the exact approved source file, not a fresh generation or screenshot. Choose 16×16, 32×32 (default custom item), or 64×64 according to the user's target; honor other explicitly requested dimensions. Contain the complete sprite proportionally on a square canvas, preserve genuine alpha, then downscale with nearest neighbor only. Do not silently recolor, mirror, repaint or alter approved pixels. Flag defects and request approval for substantive art changes.
4. **Inspect and verify:** Check the native icon at inventory scale and at magnification. Verify the actual saved dimensions, transparency if needed, silhouette and edge readability. If small details disappear, return to review rather than silently changing the design. A pixelated-looking high-resolution image is never proof of native dimensions.
5. **Dual output:** Always deliver both the actual native-size lossless PNG and a separate **exactly 512×512 PNG preview**, enlarged directly from the finished native PNG using nearest neighbor (32×, 16×, or 8× for 16, 32, or 64 pixels). Label each clearly; provide usable file links if supported. Never regenerate or smooth the preview, never use it as the game texture, and never claim a file was saved or verified without inspecting it. If the host cannot access the generated source or write files, report the limitation rather than inventing a handoff.

This workflow is for pixel-art textures, not photographs, banners, or painterly artwork.

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
- For pixel-art textures, concept approval (or an explicit bypass) is established; the actual native PNG and exact 512×512 nearest-neighbor preview are both verified and delivered, and existing transparency is preserved.
- Any text is spelled correctly and positioned as requested.
- No extra logos, watermarks, or unrelated objects were introduced.
- The style matches the requested Minecraft context.
- For texture concepts, the result looks easy to paint over, simplify, or tile manually.

---
