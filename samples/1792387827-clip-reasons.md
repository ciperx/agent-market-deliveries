# Clips

Platform framing: **9:16** (1080x1920). Built from 18 sentences recovered from the audio.

| # | Start | Length | Score | Density | Hooks | Topic shift | Why picked |
| - | - | - | - | - | - | - | - |
| 1 | 0.18s | 29.0s | 7.608 | 2.55 | 3 | 0% | speech density 2.55 w/s and 3 hook signal(s); topic moves 0% away from the previous segment |
| 2 | 43.26s | 32.5s | 10.015 | 2.59 | 5 | 88% | speech density 2.59 w/s and 5 hook signal(s); topic moves 88% away from the previous segment |

## What each clip says

**Clip 1** (0.18s-29.19s)
> most people think you need a team to sell a service you do not you need one agent that answers here is the mistake almost every one makes they describe what the agent is instead of what it delivers buyers do not care about your architecture they care about the file they get back so how do you price 

**Clip 2** (43.26s-75.72s)
> here is a trick that works give the buyer the transcript every time when they can check one word instead of redoing the whole job revision stop being arguments nobody talks about the boring part which is that most jobs fail because the brief was vague why does that matter because a vague brief as a 


## How the moments were chosen

- Sentences are rebuilt from word-level timings, not guessed from punctuation alone.
- Every window that starts on a sentence and fits the length budget is scored.
- Score = speech density x1.4 + hook language x1.1 + topic shift x0.8. Hook language is question marks, how/why/never/secret/mistake/tip words and numbers; topic shift measures how little the window's vocabulary overlaps the previous one.
- The highest-scoring windows that do not overlap are kept, so the clips come from different parts of the video instead of four cuts of the same minute.
- Each clip is re-timed to zero and captioned from its own words.