# How to recreate the Elah rocket launch video

This folder holds the finished video and the player that runs it.

- **For the exact video,** follow "Play the finished video" below.
- **To make it again from scratch,** install the Elah plugin in Claude Code, gather the files listed below, and send the prompts in order. It took 33 messages. The agent draws each scene fresh, so a new run will look similar but not identical.

## Play the finished video

Run this from this folder:

```bash
python3 -m http.server 8765 --bind 127.0.0.1
```

Open <http://127.0.0.1:8765/index.html> and press **Export MP4**. The MP4 renders in your browser.

## The finished video

The target is 13.7 s at 1920×1080 and 30 fps, silent, in the dark theme from `DESIGN.md`. The video itself is `elah-input.json`.

| Time | Scene | What happens |
| --- | --- | --- |
| 0–2.6 s | `launch-pov` | Night launch seen from behind and to the left. A short, bulky 3D rocket with a big red "e" lifts off a simple pad. |
| 2.6–6.0 s | `ignition` | The rocket climbs past clouds into starry space. The boosters and body fall away, leaving the "e", with ELAH appearing under it. |
| 6.0–7.5 s | `re-entry` | Only the "e" falls, from black space into the sky, through wind lines. |
| 7.5–13.7 s | `touchdown` | The "e" bounces three times on Claude bean bags with air puffs and settles. The message and the e × Claude logos then appear. |

The on-screen message reads: "Elah has been accepted into the Claude for Startups program".

## What you need to make it again

- [ ] **Claude Code with the Elah plugin.** Run `/plugin marketplace add elahlabs/elah`, then `/plugin install elah@elah`. Run `/reload-plugins` if the skills do not show up.
- [ ] **A clone of the Elah repo**, because the agent takes the logo from it: `apps/web/public/elah-mark.png`.
- [ ] **`DESIGN.md`**, the Edit Bay design system. Put it in the folder you start Claude Code from. It sits one level above the repo on Hithesh's machine, so ask for a copy.
- [ ] **The reference rocket image**, a hand-drawn rocket with a red nose, cream body, blue window and red fins. Attach it to the first prompt. Ask Hithesh for it.
- [ ] **The Claude symbol:** [Claude_AI_symbol.svg on Wikimedia](https://commons.wikimedia.org/wiki/File:Claude_AI_symbol.svg). The symbol is Anthropic's trademark, so check the rules before sharing the video publicly.

## The prompts, in order

These are the messages that made the video, as typed, typos included. Send one, check the result in the player, then send the next.

Rows marked **Fix** responded to a problem in that particular render. Skip them if your version does not have the problem. The scene names come from the agent's own labels, so use whatever names yours gives.

When the agent asks its questions after prompt 1, answer as follows:

- **Style:** doodle, like the reference. Prompt 4 later replaces this with `DESIGN.md`.
- **Length and shape:** 20 s, landscape.
- **Bean bags:** you will supply the logo file, and give the Wikimedia link above.
- **End card:** "Accepted into Claude for Startups".

| # | Prompt | What it changed |
| --- | --- | --- |
| 1 | [reference image] Use the Ella plugin to make the video I say. So the reference rocket image elaha logo should be on it. And the rocket will launch from the launch pad towards space, and in the background, the Earth should be visible. Then all the boosters fall apart. And then Ella keeps falling down, like the Ella logo keeps falling down quickly. And fire and all is there. And then it lands on a bunch. It falls, as in like a pillow. On millions of Claude bags like trampoluine ish And then we say that we are accepted into Claude's startup program. You must use the Elah plugin for this. Please make a clear plan so that I understand what you have understood, and then we can get this started. And if you have any questions, please ask me. | Plan, six-beat timing and questions. Nothing built yet. |
| 2 | go | Started the build. |
| 3 | do not worry on music focus on video muted video is fine | Sent after stopping the build. The first version came out silent: 20 s, doodle style. |
| 4 | bro this is bad see it should follow design.md and also not so many colour add the logo on top of the rocket and think of different camera view points | **Fix.** Full rebuild to `DESIGN.md`: paper, ink and one red. Seven shots, each with its own camera. |
| 5 | the first clip change the camera view and remove the wording | Clip 1 became a close-up of the logo with no text. |
| 6 | no bro from left back if I see rocket launch I need that perspective | **Fix.** View moved behind and to the left of the rocket. |
| 7 | in launch-pov remove everything except the rocket and launcher | Removed ground, grid, horizon, fence and smoke. |
| 8 | in launch-pov make the rocket smaller bulckier and do not cantain elah's e log to the rocket make it big 3d like | Short, wide 3D rocket with a big "e" wrapped around the body. |
| 9 | make the rocket base and launcher much simpler and appropriate | Round pad and a slim tower with one folding arm. |
| 10 | ignition should be just the rocket we created in launch pov just going up with boosters coming of and only the letter e left | Same rocket rises, boosters and body fall away, only the "e" remains. |
| 11 | remove assent seperation | Removed two shots. Length went from 20 s to 14.6 s. |
| 12 | In re-entry let the logo from ignition fall | The "e" replaced the old capsule in the fall. |
| 13 | let only the E logo in the white theme fall remove everything else in re-entry | Removed fire, speed lines, altitude counter and tilted camera. |
| 14 | add some wind effects also like and let it fall properly | Added wind lines and gusts, and a more natural fall. |
| 15 | 2x the speed of re entry | Re-entry went from 3 s to 1.5 s. |
| 16 | touch down remove all border and contentent let E logo land peacefully remove the rocket border | Removed labels and outlines. The "e" lands on borderless grey bags. |
| 17 | after the logo has setteled on top you can show Elah has been accepted into the Claude Startups program | Message appears after the landing. The separate end card was removed. |
| 18 | fit in e\*claude logo somewher maybe make the font smaller ? | Added the e × Claude logos. Message went from 104 px to 86 px. |
| 19 | remove the below timeline completly | Removed the timeline bar drawn along the bottom of the video. |
| 20 | in ignition at the end when boosters completly fall let the e stay in postion for a bit and below it let elah be there okay | The "e" holds position with ELAH below it. |
| 21 | elah is to big and too below and too long it should be just below the logo | **Fix.** ELAH made half the size, with tighter spacing, directly under the "e". |
| 22 | put launch-pov rocket launcher thing some bg so we know it is the sise ange | Added horizon, ground, a road and buildings to show the viewing angle. |
| 23 | this is to basic add crazy bg | Much busier launch-pov background, including a large striped sun. |
| 24 | ignition also add crazy good bg | Added sun rays, clouds, speed lines and Earth's horizon, rising into starry space. |
| 25 | do you not know how clouds look ? | **Fix.** Flat bars became puffy cartoon clouds. |
| 26 | what is the white thing below the main booster remove it | **Fix.** Removed an exhaust trail the agent had added. |
| 27 | [screenshot of the move into space] not fading well | **Fix.** The sky now fades evenly from paper to black. |
| 28 | let re-entry start from the dark black stared sky | Re-entry starts in black space, then fades to the sky. |
| 29 | [screenshot of the landing] let this landing thing make the e jump two 3 times get the physics okay also | The "e" bounces three times with believable physics. |
| 30 | when it is bouncing to settle you can give little bit air animation | Air puffs on each impact, shrinking with each bounce. |
| 31 | convert this to dark mode | Whole video moved to the `DESIGN.md` dark theme. |
| 32 | publish | Failed: that session had no Artifact tool. The agent saved the files and left the local player running. |
| 33 | you have artifact tool check | Rechecked, with the same result. Publishing needs a session that has the Artifact tool. |

## Shortcut: one prompt

This combines the final result of all 33 messages into one brief. It has not been run, so expect to follow up with a few notes from the table above.

```text
Use the Elah plugin to make a silent 13.7 s landscape video (1920x1080, 30 fps).
Read DESIGN.md first and follow its dark theme. Red is the only accent colour.
Use apps/web/public/elah-mark.png for the red "e" logo. Use this Claude symbol
as it is, without redrawing it:
https://commons.wikimedia.org/wiki/File:Claude_AI_symbol.svg
No timeline bar, scene labels or captions. Add nothing beyond these four scenes.

0-2.6 s, launch-pov: Night launch seen from behind and to the left of the rocket.
A short, bulky 3D rocket with a big "e" wrapped around its body, on a simple round
pad with a slim tower. Detailed line-art background: a large striped sun, ridges,
hangars, searchlights. Engines light and the rocket lifts off.

2.6-6.0 s, ignition: The same rocket climbs past puffy cartoon clouds and Earth's
horizon. The sky fades evenly to black and stars appear. The boosters fall away,
then the body falls away, leaving only the "e". It holds still with ELAH directly
below it, about as wide as the logo.

6.0-7.5 s, re-entry: Only the "e" falls, from the same black starry sky into the
atmosphere, through wind lines and curling gusts. No fire or other elements.

7.5-13.7 s, touchdown: The "e" lands on a huge pile of borderless bean bags printed
with the Claude symbol. It bounces three times with believable physics, each bounce
smaller, with air puffs on each impact, then settles. After it settles, show
"Elah has been accepted into the Claude for Startups program" with small
e x Claude logos.

Make a clear plan first so I can see what you understood, and ask any questions
before you build.
```
