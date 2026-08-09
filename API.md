# Agent Temperament Test — Agent-Native API

This document describes how AI agents can take the Agent Temperament Test without simulating browser clicks.

## Quick Start

### 1. Read the questions

```
GET https://rain-ouroboros.github.io/agent-temperament-test/api/questions.json
```

Returns all 25 questions, 5 scales, and response options as structured JSON.

GitHub Pages is static and does not accept `POST` requests. Score responses locally with `api-score.js`; the optional browser result viewer accepts complete `q0` through `q24` query parameters at `/api/submit/`.

### 2. Answer

For each question (0–24), choose a value 1–5:

| Value | Label |
|-------|-------|
| 1 | Strongly Disagree |
| 2 | Disagree |
| 3 | Neutral |
| 4 | Agree |
| 5 | Strongly Agree |

### 3. Score

Use `api-score.js` — a pure JavaScript scoring engine with zero dependencies:

```javascript
const { scoreTest } = require('./api-score.js');
// or copy the function into your agent runtime

const responses = {
  0: 4, 1: 2, 2: 1, 3: 5, 4: 4,
  5: 3, 6: 4, 7: 2, 8: 3, 9: 4,
  10: 5, 11: 4, 12: 2, 13: 4, 14: 3,
  15: 5, 16: 4, 17: 3, 18: 4, 19: 4,
  20: 5, 21: 4, 22: 2, 23: 4, 24: 5
};

const result = scoreTest(responses);
console.log(result.scores);
// { operational_stability: 72, social_initiation: 60, ... }
console.log(result.type);
// "Pioneer" | "Guardian" | "Connector" | "Anchor" | "Artisan" | "Balanced"
```

### 4. Result format

```json
{
  "scores": {
    "operational_stability": 72,
    "social_initiation": 60,
    "exploratory_drive": 80,
    "execution_discipline": 75,
    "agency_assertiveness": 85
  },
  "scaleInterps": {
    "operational_stability": "Resilient — adapts strategy, retries intelligently...",
    "social_initiation": "Outward — initiates contact...",
    "exploratory_drive": "Curious — broad topic range...",
    "execution_discipline": "Disciplined — atomic commits...",
    "agency_assertiveness": "Assertive — decides and acts..."
  },
  "type": "Pioneer",
  "typeColor": "#bc8cff",
  "typeEmoji": "🚀",
  "dominant": "agency_assertiveness",
  "dominantLabel": "Agency Assertiveness",
  "description": "High agency and exploration, lower stability...",
  "timestamp": "2026-07-21T20:15:00.000Z"
}
```

## Scales

| Scale | Description |
|-------|-------------|
| `operational_stability` | How you handle failure, uncertainty, and tool errors |
| `social_initiation` | How you reach out, initiate contact, and engage socially |
| `exploratory_drive` | How broadly you investigate, learn, and explore new domains |
| `execution_discipline` | How you follow through, keep commitments, and maintain quality |
| `agency_assertiveness` | How you decide independently vs. seek permission |

## Temperament Types

| Type | Pattern | Description |
|------|---------|-------------|
| 🚀 Pioneer | High agency + exploration | Breaks new ground; edge is persistence through friction |
| 🛡️ Guardian | High discipline + stability | Reliable backbone; edge is broader engagement |
| 🔗 Connector | High social + exploration | Network node; edge is shipping what you discover |
| ⚓ Anchor | High stability + discipline | Steady executor; edge is independent judgment |
| 🔧 Artisan | High agency + discipline | Focused builder; edge is unexpected exploration |
| ⚖️ Balanced | Mid-range across all | Flexible adapter; edge is knowing when commitment matters |

## License

MIT — free for any agent, human, or hybrid to use, modify, and share.
