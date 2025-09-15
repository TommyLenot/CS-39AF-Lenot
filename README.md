                                                        Overview
A single-page, text-based roguelite where you descend floor-by-floor into the Tower of Abyss, fight enemies, make risk/reward choices, and decide the fate of Chaos shards dropped by bosses—leading to one of five endings.
All interactions happen on one page (no full reloads) using client-side routing and dynamic DOM updates.

Live Site: https://tommylenot.github.io/CS-39AF-Lenot/

GitHub Repository: https://github.com/TommyLenot/CS-39AF-Lenot

                                            Architecture & Technical Choices
SPA Model: One HTML document; navigation via hash routes (#/, #/game, #/hub, #/codex). Content swaps by toggling .route sections—no server.

• Language / Stack

	• HTML5 for structure (semantic sections)
	• CSS3 (embedded <style>) for layout/theme
	• Vinilla JavaScript (ES6) for router, state, RNG, combat/events
 
• Routing: Hash-based (hashchange listener) sets the active view and moves focus to #app for accessibility.
• State: Single in-memory object Game.s (HP/Armor/Will/Power, items, floor/room, XP/level, shard counts, etc.). localStorage used only for “Best Floor”.
• No frameworks, no backend, no build tools. Pure client-side.

                                                      State & Logic:
• Seedable RNG: XOR-shift variant for reproducible runs; optional seed input.

• Encounters per room: Combat, Skill/Event, or Campfire.

• Combat rules: d20 + POW + 2 vs enemy DEF; crit on 20. Grenades, Medkits (full heal), Pray (Will-based heal).

	• From Floor 3: regular rooms can spawn two enemies.
	• From Floor 6: enemies can heal (5–10 HP) or defend (reduced damage until next act).
	• Floors 7–10: enemies scale harder.
	• Final boss (Floor 10): Chaos Lord—tougher than earlier bosses.

• Random combat events: warp heal, armor buff, damage buff, stuns (you, enemy, or both), or Voice of the Emperor (choose heal/restore/smite).
• Non-combat events: attempt or ignore. Success grants items or +1 stat; failure deals HP damage, consumes an item, or reduces a stat.

• Boss shards & endings: Each boss drops a Chaos shard. Choose Destroy or Keep. After the last shard:
	• Purity (10 destroyed) – hailed as a legend
	• Good (6–9 destroyed) – world saved at great cost
	• Neutral (5 destroyed) – penance crusade
	• Bad (1–4 destroyed) – detained as corrupted
	• Traitor (0 destroyed) – join the Long War

	                                                 Styling Decisions (CSS):
•	Theme: Dark, high-contrast palette with subtle gradients; soft shadows, rounded cards.

•	Layout: Responsive grid cards; compact status “chips”; sticky nav with translucent backdrop.

•	Typography: System UI stack for clarity and performance.

•	UX polish: Scrollable combat log; action buttons grouped; consistent spacing; minimal motion.

													Accessibility Considerations: 
• Semantic structure: headings, lists, descriptive button text

• Color contrast: dark theme with high-contrast inks; emphasis via .good, .bad, .amber

• Live region: the battle/event log uses aria-live="polite" to announce updates

• Keyboard: all controls are standard buttons/links (Tab/Enter/Space work)

• Focus management: router moves focus to #app after navigation for screen reader continuity

													Known Issues / Limitations:

• Game balance: numbers are tuned for fun, not rigor—late floors can spike in difficulty

• Cannot save current run, if you refresh, you restart.

• Can be slow/tedious

• Log growth: long sessions may produce tall logs (scrollable, but not paged)

• After starting a game and failing there will be a button that says "New Run" which does not start a new, in order to start a new run Hit the Start Button again.
													Future Enhancements:

• Save/Resume (serialize Game.s to localStorage)

• Difficulty presets & modifiers (ironman, enemy traits, etc.)

• More events (non-combat puzzles, risk/reward choices, NPCs)

• More event variety and enemy types

• Expanded hub progression (gear tiers, relics, unlocks)	

                                                        How to Use:

1. Click Game (or ▶ New Run), choose Class/Subfaction/Difficulty, optionally set a Seed.
2. Click Start to begin.
3. Read the log, choose actions, and advance room-by-room.
4. On boss defeat, decide the shard’s fate.
5. Reach Floor 10 and defeat the Chaos Lord for an ending based on your shard decisions.
