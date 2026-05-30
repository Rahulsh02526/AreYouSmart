# Are You Smart? — Quiz Platform

A scalable, JSON-driven quiz platform with voice narration, smart randomisation and no backend required.

## Repository Structure

```
/
├── are-you-smart.html          ← Main platform (open this in browser)
├── admin.html                  ← Question bank manager
├── index.json                  ← Master manifest of all modules
└── questions/
    ├── sports/
    │   ├── football/
    │   │   ├── worldcup.json
    │   │   ├── legends.json
    │   │   ├── clubs.json
    │   │   └── guess.json
    │   └── cricket/
    │       ├── ipl.json
    │       └── international.json
    ├── movies/
    └── gk/
```

## How to Add New Questions

1. Open `admin.html` in browser (password: `ays2026`)
2. Click **Load JSON** → select the relevant file (e.g. `ipl.json`)
3. Click **Add Question** → fill the form → save
4. Click **Download JSON** → save the updated file
5. Replace the file in this repo and commit
6. Cloudflare Pages auto-deploys in ~30 seconds

## How to Update an Answer

When a record changes (e.g. most IPL titles holder):
1. Open `admin.html`
2. Load the relevant JSON file
3. Click **Needs Review** to see outdatable questions
4. Click **Update** on the question → change answer and fact
5. Download → commit → deployed

## Deploying to Cloudflare Pages

1. Push this repo to GitHub
2. Go to Cloudflare Pages → Connect GitHub repo
3. Build settings: none (static files)
4. Deploy — your platform is live at `yourname.pages.dev`
5. Add custom domain (e.g. `areyousmart.in`) in Cloudflare DNS

## Question JSON Schema

```json
{
  "id": "ipl-001",
  "type": "mcq",
  "difficulty": "easy",
  "hook": "🏆 Optional tension line shown before question",
  "q": "Question text here",
  "opts": ["Option A", "Option B", "Option C", "Option D"],
  "ans": 1,
  "fact": "Fun fact shown after answer reveal",
  "outdatable": false,
  "review_after": "2027-06-01",
  "vs": {
    "pauseAfterQ": 900,
    "pauseBetweenOpts": 550
  }
}
```

### Fields

| Field | Required | Description |
|-------|----------|-------------|
| `id` | Yes | Unique ID — format: `module-number` (e.g. `ipl-021`) |
| `type` | Yes | `mcq`, `guess_player`, or `true_false` |
| `difficulty` | Yes | `easy`, `medium`, or `hard` |
| `q` | Yes | Question text |
| `opts` | Yes | Array of 4 options |
| `ans` | Yes | Index of correct answer (0=A, 1=B, 2=C, 3=D) |
| `fact` | Yes | Fun fact shown after answer |
| `outdatable` | No | `true` if answer may change in future |
| `review_after` | No | Date to review this question (YYYY-MM-DD) |
| `hook` | No | Tension hook shown before question |
| `vs.pauseAfterQ` | No | Milliseconds pause after reading question (default 900) |
| `vs.pauseBetweenOpts` | No | Milliseconds pause between options (default 550) |

## Adding a New Module

1. Create the question JSON file in the correct folder
2. Add the module entry to `index.json` under the relevant subcategory
3. Commit both files — platform auto-updates

## Custom Background Music

To use your own royalty-free music instead of the built-in synthesised audio:

1. Find a royalty-free track on YouTube Audio Library
2. Download as MP3 and host it (or use a CDN URL)
3. In `are-you-smart.html`, find this line:
   ```javascript
   const CUSTOM_MUSIC_URL = null;
   ```
4. Replace `null` with your MP3 URL in quotes

## Tech Stack

- Pure HTML/CSS/JavaScript — no framework, no build step
- Web Speech API — voice narration
- Web Audio API — all sound effects synthesised in browser
- localStorage — question tracking, no server needed
- Cloudflare Pages — hosting (free tier)
- GitHub — version control + auto-deploy

## Roadmap

- [ ] User login (Google OAuth via Supabase)
- [ ] Leaderboards
- [ ] Championships
- [ ] Subscription payments (Razorpay)
- [ ] 200,000 question bank
- [ ] Cricket, Movies, GK modules
- [ ] Hindi/multilingual support
