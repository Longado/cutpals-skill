---
name: cutpals
description: Generate extremely simple, cute character mascots built from 3-4 layers of cut paper, centered on one solid paper background. Use when someone wants a mascot, IP character, or character avatar for a product, brand, project, or community, including when the subject is open and the agent should infer directions from product context.
---

# Cutpals

Make the simplest lovable character that still reads at 32 × 32: one character head cut from 3–4 layers of colored paper, stacked with soft shadows, centered on a single sheet of background paper.

## Workflow

1. **Find the subject.** If the user named one, keep it. If not, read whatever product context is available read-only (README, landing copy, app metadata, design tokens). If purpose, audience, and personality are still unclear, ask one combined question covering all three, once.
2. **Propose three directions**, one line each: `<subject> — <why it fits the product> — <defining feature>`.
   - Named subject: three treatments of that subject (defining feature, layer split, or personality).
   - Open subject: three different familiar animals by default, each tied to a different product trait. Use an object or unusual creature only when the product gives a direct reason. The animals named in this file only illustrate rules; choose from the product, not from these examples.
   - Agents fall back on the same few animals: rabbits, dogs, elephants, owls. Pick one of them only when a specific trait of that animal matches the product, never just because it is cute and familiar, and use at most one of them per batch.

   Then propose six images. Wait for a yes unless the user has already authorized generation.
3. **Assign palettes.** All three directions accepted → `A1 A2 B1 B2 C1 C2`: each direction gets two different palettes. At least four of the six sit on a deep background; the rest sit on a natural light paper. No background hue repeated. One direction chosen → `A1`–`A6`, six palettes. The user's own count or split overrides this.
4. **Check the image model.** Prefer GPT Image 2; Gemini image models (Nano Banana Pro, Nano Banana 2) are acceptable. If none is available, ask the user to enable one or provide an API key. Never substitute SVG drawing. Use a weaker model only with the user's consent and say quality may drop.
5. **Generate** each candidate as its own call, in parallel subagents when available, with the prompt below. One square image per call, never a grid or contact sheet. Do not feed earlier candidates back as references.
6. **Deliver everything** as returned: label, subject and rationale, colors, file path, size. Do not filter, rank, auto-retry, or retouch. Redraw only when the user asks.

## Design rules

**Silhouette**
- The head only (or the main mass of a headless subject, such as a cup or a cloud), front view. No body, paws, legs, or tail unless one of them is the defining feature.
- Built from 3–4 paper layers, each one large rounded shape. A typical stack: a back layer that shows as a rim, the head, and the defining feature. Merge or drop any layer that does not carry identity.
- Exactly one defining feature, big enough to name the species by itself: rabbit → long ears, elephant → trunk and big round ears, fox → wide pointed-but-blunt ears and a tapered muzzle, whale → spout and tail fluke, hedgehog → a long tapered snout with a round dark nose tip, set in front of a dome of rounded quill scallops (without the snout, a quill ring around a round face reads as a lion or a sunflower). If the character could pass for a cat or a bear, the feature is wrong. When ears are not the feature, leave them out rather than adding small round ones that turn the face into a bear (a hedgehog stays earless).
- Face: two small dark paper dots for eyes, set wide apart and low. Add one tiny nose or small smile cut from the same dark paper, unless the defining feature (a trunk, a bill) already sits where the nose would be. No brows, eyelashes, cheeks, outlines, whiskers, or printed patterns.
- Every edge a clean, smooth scissor cut with rounded ends. No thin strips, needle points, or narrow gaps: paper that thin would tear.
- Test: as a black silhouette at 32 × 32 it is still recognizable. If a feature vanishes at that size, enlarge it, merge it, or delete it.
- Never imitate an existing character. If the result could be mistaken for a famous one (a rabbit head with dot eyes and a cross mouth, a white cat with a bow), change the feature, the proportions, or the subject.

**Composition**
- Centered, upright, fully visible, filling about 75% of the square. Never cropped, tilted, or seen from the side.

**Color**
- Four colors in the image: the background paper, the main character paper, one second paper for one layer, and a dark paper for the eyes and nose or smile.
- The second paper is the same hue family as the main paper, clearly lighter or darker, so the layers separate without adding a new color idea.
- The main character paper is light or mid-tone. A near-black or very deep character swallows its own face.
- Strong contrast in lightness between the character and the background: light on deep, or mid-tone on light. Two mid-tones fail.
- The defining feature is cut from the main or second paper, never from the dark eye paper: a dark trunk reads as a koala's nose.
- The eyes must stand out from the paper they sit on: dark dots on light or mid-tone paper. If the head has to be deep, cut the eyes from cream paper instead.
- Background: one named solid paper color. Deep sheets are rich but slightly muted: earthy or jewel-like. Light sheets are natural paper tones only: warm cream, oatmeal, pale kraft. Never candy pastels (peach, baby pink, lavender, butter yellow), gray, or muddy colors. A palette the user supplies goes to the background.

**Rendering**
- Real layered paper: each layer casts a soft, short shadow onto the one beneath, and every sheet has a faint paper-fiber texture. Matte, never glossy.
- Not felt, plush, clay, plastic, embroidery, or 3D render. No drawn outlines.

## Prompt

Never send these words to the image model: `logo`, `brand mark`, `icon`, `app icon`, `emblem`. They pull the model toward badges, lettering, and clip art. Describe only the picture. Also avoid `transparent`, `alpha`, and `opaque`.

Fill in every `<...>`:

```text
A square 1:1 image, full bleed.
Background: one sheet of <background color> paper filling the whole square, flat and even.
Subject: the head of one extremely simplified, cute, lovable <subject> character, made entirely of 3-4 layers of cut paper stacked on top of each other, each layer one large simple rounded shape with clean scissor-cut edges. Defining feature: <feature>.
Face: two tiny dark paper dots for eyes, set wide apart and low<, and one tiny paper nose | , and one small paper smile>.
Colors: the whole head is <main color> paper; <second color> paper is used only for <the one layer it covers>; only the tiny eyes<and nose | and smile> are cut from <dark color>. Four colors in total including the background.
Depth: each paper layer casts a soft, short shadow onto the layer beneath, so the stack reads as real layered paper; a faint paper fiber texture.
Composition: the head is centered, upright, front view, fully visible, filling about 75% of the square.
Constraints: no text, no watermark, no border or frame, no other objects or scenery, no outlines, no thin strips or sharp points, no glossy highlights, no printed patterns or spots, no body, paws, or tail.
```

- Write every color as a plain name plus a hex value, such as `deep muted petrol teal (#15535B)`.
- Never write that "the face" is cut from the dark paper: image models read "face" as the whole front of the head and paint it dark. Name the eyes, nose, or smile instead.
- If the model takes a separate negative-prompt parameter, move the `Constraints` content there and drop that line from the main prompt.
- Request about 1536 × 1536 when the tool accepts a size. Keep whatever native square size comes back; do not resample.
