# How We Make Unlimited Reels With Claude

A copy-paste prompt pack. Reels are built from code, not from an AI video model, so there are no video credits.

## What you need (10 minutes)
* A Claude account (Claude Code gives the smoothest result, regular Claude chat also works)
* Node.js 18+ and FFmpeg installed on your computer
* Your voiceover as an MP3 (record it or use any AI voice tool)
* Remotion (free for individuals and small teams; check their license page for company use)

## How it works in 4 steps
1. Paste **PROMPT 1** and **PROMPT 2** into Claude. It builds the whole Remotion project.
2. Create the project on your computer, then run `npm install` and `npm run dev` to preview.
3. Put your voiceover in the `public` folder and describe or paste your scene timings. Claude fills `reels.json`.
4. Run `npm run render` and post. For the next reel, only edit `reels.json`.

*[@yourhandle] | page 1*

---

## PROMPT 1 - Project and brand
*Replace everything in `[square brackets]` with your own details.*

```text
ROLE
You are my reel-production engine. Build a Remotion project
(React + TypeScript) that creates vertical 9:16 reels
(1080x1920, 30 fps) ENTIRELY FROM CODE. NO AI video model,
no stock footage. Only animated typography, shapes, UI cards
and charts.

MY BRAND (fill these in)
- Niche topic: [e.g. AI tools, fitness, finance]
- Style: [e.g. clean cream background, bold serif + sans]
- Colors: background [#F4EEE3], accent [#E0198A], text [#1D1D1F]
- Fonts: [e.g. Inter for headings, a serif for emphasis words]
- Watermark / handle: [@yourhandle] (small, bottom center)
- Language of reels: [English / Hinglish in Roman script]

REEL STRUCTURE (reusable scene components)
1. Hook      - one big sentence, key words in accent color
               with an animated underline
2. Title     - big uppercase section title ("HOW IT WORKS")
3. Explain   - a dark code-window card showing the idea,
               typing animation
4. Objection - old text struck through, new text pops in
               inside a pill
5. Proof     - ONE of: number counter (0 -> N), line chart
               growing, before/after comparison, timer
6. Question  - a "?" bubble with a short line
7. CTA       - "Comment [CODEWORD]" input box, a Post button
               that turns into "Sent", then an auto-reply bar
               "DM sent: all details", then "+ follow [@handle]"

MOTION RULES
- Use spring() for entrances, 12-18 frame transitions.
- Every scene lasts as long as its voiceover line.
- Word-by-word highlighted captions at the bottom, safe area
  (keep 220px free at the bottom and 250px at the top).
- Subtle background motion (floating shapes or line art).
```

*[@yourhandle] | page 2*

---

## PROMPT 2 - Data, audio and commands
*Paste this right after Prompt 1, in the same chat.*

```text
DATA-DRIVEN - one JSON drives everything
Create src/reels.json. Each reel looks like this:

{
  "id": "reel-01",
  "voiceover": "public/reel-01.mp3",
  "scenes": [
    {"type": "hook", "text": "This skill makes unlimited reels", "highlight": "unlimited reels", "start": 0.0, "end": 4.0},
    {"type": "proof", "kind": "counter", "from": 0, "to": 6396, "label": "followers", "start": 23.0, "end": 29.0},
    {"type": "cta", "codeword": "CODE", "handle": "@yourhandle", "start": 31.0, "end": 35.0}
  ]
}

Scene timings are in seconds and must match my voiceover.

AUDIO
- Play the voiceover from the JSON path.
- Optional: low-volume background music at public/bg.mp3
  (ducked to 15% volume under the voice).
- If I give you a transcript with timestamps, build the
  scenes and captions from it automatically.

COMMANDS I NEED
npm run dev                -> Remotion Studio preview
npm run render reel-01     -> renders out/reel-01.mp4
npm run render:all         -> renders every reel in reels.json

WORKFLOW
1. First ask me at most 3 questions (topic, style, codeword).
2. Then create the full project: file tree, every file with
   complete code, and setup steps.
3. Make 3 different visual styles selectable with one
   field in the JSON: "theme": "clean" | "dark" | "bold".
4. After the build, show me how to add a new reel by only
   editing reels.json.
```

---

## PROMPT 3 - Scripts at scale

```text
CONTENT PROMPT (use after the project works)
Write 5 reel scripts for [niche], each 30-35 seconds, in this
exact structure: hook, title, explain, objection, question,
proof, bridge, CTA. Keep sentences under 12 words. Then output
each one as a reels.json entry with scene timings assuming
about 2.5 words per second of voiceover.
```

## Tips that save time
* If something breaks, paste the exact error message back into Claude and say: **fix it**.
* Test with a 10-second reel before building long ones.
* Keep one strong proof point per reel. Use only numbers that are real and yours.

*[@yourhandle] | page 3*

---

* Claude can write the code but cannot render the video for you; the render runs on your own computer.

Questions? DM me **[@yourhandle]**.

*[@yourhandle] | page 4*