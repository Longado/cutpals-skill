<p align="center"><img src="assets/header.png" width="112" alt="Cutpals"></p>

<h1 align="center">Cutpals</h1>
<p align="center"><strong>Your AI agent cuts a mascot for your product out of colored paper.</strong></p>
<p align="center">One Agent Skill for Codex, Claude Code, or any agent that can call an image model. Describe your product; get six paper mascot candidates.</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue" alt="MIT"></a>
  <img src="https://img.shields.io/badge/tested%20with-Codex%20CLI-black" alt="tested with Codex CLI">
  <img src="https://img.shields.io/badge/format-Agent%20Skill-green" alt="Agent Skill">
  <img src="https://img.shields.io/badge/status-Alpha-orange" alt="Alpha">
</p>

<p align="center">
  <a href="README.zh-CN.md">中文</a> ·
  <a href="#quick-start">Quick start</a> ·
  <a href="#build-with-us">Build with us</a>
</p>

Ask an image model for a mascot and you usually get flat clip art or a shiny 3D toy. Cutpals has it build one from three or four sheets of colored paper instead: a big simple head, two dot eyes, soft shadows between the layers.

**One Markdown file · Works with any agent · Nothing to run**

## What it is

`cutpals` is a single `SKILL.md` in the open Agent Skills format. It tells your agent how to read your product, pick three characters that fit it, and write six image prompts that keep every result in the same cut-paper style: a centered head, 3–4 paper layers, one feature that names the animal, four colors, a rich solid background.

Your agent does the reading and the prompt writing; your agent's image model does the drawing. Nothing is installed besides the Markdown file.

> **Early version.** So far it has been run only with Codex CLI and its built-in image tool, on six product descriptions, for 48 images across four rounds of rule changes. Claude Code, Gemini image models, and other agents have not been tried yet. See [Known issues](#known-issues).

![Cutpals showcase](assets/wall.webp)

<sub>18 picks from the 48 images generated for six product descriptions while the rules were being tuned. Not retouched.</sub>

## How it works

| You… | It… |
|---|---|
| ask for a mascot without naming an animal | reads your README or landing copy and proposes three characters, each tied to a different trait of the product |
| say yes | generates six images: each character in two palettes, most on deep backgrounds and the rest on light natural paper |
| name your own subject | keeps it and proposes three treatments of it instead |
| bring brand colors | uses them for the background paper |

Rules it holds every image to:

- The head only, centered, about 75% of the square, front view.
- 3–4 paper layers with clean scissor-cut edges and soft shadows between them; no outlines, no gloss.
- Exactly one feature that names the animal on its own (long ears, a trunk, a bill). If it could pass for a cat or a bear, the feature is wrong.
- Four colors: background paper, main paper, one second paper for one layer, dark paper for the eyes and nose.
- Still recognizable as a black silhouette at 32 × 32.
- It never says "logo" or "icon" to the image model, which pulls results toward badges and lettering.
- It hands you all six as returned, without filtering or retrying.

## Try these

Each of these produced six images in our tests (the full texts are in [`examples/briefs`](examples/briefs)):

| Say to your agent | What came back |
|---|---|
| "Make a mascot for my product. Steamcup is a small free macOS menu-bar app (its menu-bar mark is a little coffee cup) that keeps the Mac awake…" | an owl, an elephant, and a coffee cup with a face |
| "Make a mascot for my product: a weather app for people who commute by bike…" | a rabbit, a duck, a floppy-eared dog |
| "…an open-source command-line tool that replays a failed CI job on your own laptop…" | a fox, an elephant, a bloodhound |
| "Make a mascot for my business: a small neighborhood sourdough bakery…" | a rooster, a puppy, a rabbit |
| "…a small open-source notes app that keeps every note as a plain Markdown file…" | a barn owl, an elephant, a hedgehog |

## Quick start

### Option A: let your AI install it

Paste this into Claude Code, Codex, or another coding agent:

```text
Install the Cutpals skill from https://github.com/Longado/cutpals-skill.
1. Read its README.md and SKILL.md.
2. Run: npx skills@latest add Longado/cutpals-skill --global
   (pick this agent when the installer asks).
3. Check which image model you can call. GPT Image 2 is preferred; Gemini image models
   (Nano Banana Pro, Nano Banana 2) are fine. If none is available, tell me what I need to enable.
4. Then ask me what product the mascot is for.
```

### Option B: install it yourself

```bash
npx skills@latest add Longado/cutpals-skill            # into the current project
npx skills@latest add Longado/cutpals-skill --global   # for all your projects
```

Or copy `SKILL.md` into your agent's skills folder by hand, for example `~/.claude/skills/cutpals/SKILL.md`.

Then just ask: *"Make a mascot for my product."*

## Known issues

- **Hedgehogs don't read as hedgehogs.** All 6 hedgehog images so far came out looking like a lion, a sunflower, or a bear.
- **The same animals keep coming back.** Over 8 runs on six products, rabbits, elephants, and dogs each showed up in 4 runs.
- **The dark-head fix has one round behind it.** Rounds 1–3 used a prompt that said "the face is cut from dark paper", and the image model sometimes painted the whole head dark (a rooster and two elephants in round 3). Round 4 switched to the current wording and all 12 heads came out light or mid-tone, but that is 12 images.
- **One agent, one image tool.** Every image so far came from Codex CLI's built-in image tool (1254 × 1254 output). Other agents and models are untested.

## Build with us

**How simple can a mascot get and still look handmade?**

| If you… | You could… |
|---|---|
| use Gemini or another image model | run the briefs in `examples/briefs` and share what comes back |
| have an animal that keeps failing (hedgehogs, for one) | add a better "defining feature" line to `SKILL.md` |
| make paper craft | tell us what real layered paper does that the rules miss |
| want a different look | fork it: most of the style lives in the Design rules and the prompt template |

Issues and pull requests are welcome.

## Credits

The workflow (three directions, six candidates, never saying "logo" to the image model, the 32 × 32 test) is adapted from [s1dashu/ip-as-logo-skill](https://github.com/s1dashu/ip-as-logo-skill) (MIT). Cutpals replaces its corner-peeking, matte look with centered cut-paper heads.

## License

[MIT](LICENSE)
