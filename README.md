# Ad Squad 🎯

**An AI ad team for small Indian advertisers running Meta (Facebook/Instagram) ads on ₹5,000 to ₹50,000.**

Most beginners lose their first ₹10k because they launch one ad, one hook, one audience, and then nobody watches the numbers. Ad Squad is a [Claude Skill](https://docs.claude.com) that acts like a 4-person team so that doesn't happen to you.

> ⚠️ Ad Squad gives structure and honest hints. It **cannot promise sales, leads or ROAS.** Always check Meta's ad policies and your own numbers.

---

## Meet the squad

| Teammate | Job | File |
|---|---|---|
| 🔍 **Scout** | Finds what competitors are running (Meta Ad Library) and what gaps nobody uses | `scout.md` |
| ✍️ **Hooks** | Writes 5 ad hooks per product: pain, curiosity, social proof, offer/urgency, before-after | `hooks.md` |
| 👥 **Personas** | Rewrites the same offer for students, homemakers, professionals, shop owners, parents and job seekers | `personas.md` |
| 📊 **Coach** | Reads your ad numbers and says what to pause, scale and test next | `coach.md` + `scripts/analyze_ads.py` |

You get a short **Squad Report** you can copy straight into Meta Ads Manager, plus a **Launch Plan** that splits your budget across tests (never one ad with all the money).

---

## Install

**Claude.ai**
1. Download `ad-squad.skill` (from the Releases page) or zip the `ad-squad` folder.
2. Go to **Settings → Capabilities → Skills → Upload skill**.

**Claude Code**
```bash
git clone https://github.com/YOUR-USERNAME/ad-squad ~/.claude/skills/ad-squad
```

**For the CSV analyzer** (optional, Python 3.8+):
```bash
pip install pandas
```

---

## How to use it

Just talk to Claude. The skill switches on when you mention Meta ads, Facebook/Instagram ads, hooks, ad copy, ad budget, ROAS, CPA, or upload a Meta Ads CSV.

**Example prompts**
1. *"I sell homemade pickles in Nanded for ₹250/jar. I have ₹10,000. Plan my Meta ads in Marathi and Hinglish."*
2. *"My Instagram ads got 40 clicks and zero sales. What's wrong?"*
3. *"Here's my Ads Manager CSV. My target is ₹150 per lead. What should I pause or scale?"*

Ad Squad first asks only for what's missing: product, price, city, goal (sales or leads), budget, where people should land (website, WhatsApp or call) and your language (Hindi, Marathi, English or Hinglish).

---

## The CSV analyzer

Export your ads from Meta Ads Manager as CSV, then run:

```bash
python scripts/analyze_ads.py tests/sample_ads.csv --target-cpr 150
```

It calculates CTR, CPC and cost per result for every ad and flags each one:

| Flag | Meaning |
|---|---|
| **PAUSE** | Low CTR, spending with no results, or audience fatigue |
| **SCALE** | Beats your target cost per result (raise budget by 20% at most, every 2 to 3 days) |
| **FIX LANDING PAGE** | Good CTR but no conversions, so the problem is the page, offer, price or tracking |
| **WAIT** | Not enough data yet (under ₹300 spent) or no clear winner |

**Default thresholds** (edit the constants at the top of `scripts/analyze_ads.py` and the table in `coach.md`):

| Rule | Default |
|---|---|
| Low CTR | below 0.8% after ~1,000 impressions |
| Good CTR | above 1.5% |
| Landing-page check | 0 results after ~100 clicks |
| Pause threshold | spend above 2x target cost per result with 0 results |
| Minimum data | ₹300 spent per ad |
| Frequency limit | above 3 |
| Scaling step | max 20% every 2 to 3 days |

The script copes with different Meta column names and shows a clear error if a column or the data is missing.

---

## Folder structure

```
ad-squad/
├── SKILL.md              # workflow and rules Claude follows
├── scout.md              # competitor research
├── hooks.md              # hook writing + honest-claims rules
├── personas.md           # six Indian audience personas
├── coach.md              # decision rules for your numbers
├── scripts/
│   └── analyze_ads.py    # CSV analyzer
└── tests/
    └── sample_ads.csv    # 6 fake ads to try the script
```

---

## Rules built into the skill
- Never promises results.
- Never invents competitor ads, testimonials or statistics.
- Labels guesses clearly as **"Assumption"**.
- Keeps language simple for beginners.
- Reminds you about Meta policy and Indian ad rules (ASCI) for health, finance and income claims.

---

## Contributing

Contributions are welcome, especially:
- Hook examples in Marathi, Hindi, Tamil, Bengali, Gujarati and other Indian languages
- Industry-specific personas (salons, tuition classes, restaurants, real estate)
- Better thresholds from real small-budget campaigns (share what you tested)
- Bug fixes for the analyzer on different Meta export formats

Open an issue or send a pull request. Please don't include real customer data in `tests/`.

## License
MIT. Add a `LICENSE` file to your repo.

## Disclaimer
Ad Squad is not affiliated with Meta or Anthropic. Ad results depend on your product, price, offer, market and budget. Use the advice as a starting point and always verify in Ads Manager.
