                                                        Overview
A single-page, text-based roguelite where you descend floor-by-floor into the Tower of Abyss, fight enemies, make risk/reward choices, and decide the fate of Chaos shards dropped by bosses—leading to one of five endings.
All interactions happen on one page (no full reloads) using client-side routing and dynamic DOM updates.

Live Site: https://tommylenot.github.io/CS-39AF-Lenot/

GitHub Repository: https://github.com/TommyLenot/CS-39AF-Lenot

                                            Architecture & Technical Choices
SPA Model: One HTML document; navigation via hash routes (#/, #/game, #/hub, #/codex). Content swaps by toggling .route sections—no server.
o Language / Stack
	o HTML5 for structure (semantic sections)
	o CSS3 (embedded <style>) for layout/theme
	o Vinilla JavaScript (ES6) for router, state, RNG, combat/events
o Routing: Hash-based (hashchange listener) sets the active view and moves focus to #app for accessibility.
o State: Single in-memory object Game.s (HP/Armor/Will/Power, items, floor/room, XP/level, shard counts, etc.). localStorage used only for “Best Floor”.
o No frameworks, no backend, no build tools. Pure client-side.

                                                      State & Logic:
o Seedable RNG: XOR-shift variant for reproducible runs; optional seed input.
o Encounters per room: Combat, Skill/Event, or Campfire.
o Combat rules: d20 + POW + 2 vs enemy DEF; crit on 20. Grenades, Medkits (full heal), Pray (Will-based heal).

	o From Floor 3: regular rooms can spawn two enemies.
	o From Floor 6: enemies can heal (5–10 HP) or defend (reduced damage until next act).
	o Floors 7–10: enemies scale harder.
	o Final boss (Floor 10): Chaos Lord—tougher than earlier bosses.

o Random combat events: warp heal, armor buff, damage buff, stuns (you, enemy, or both), or Voice of the Emperor (choose heal/restore/smite).
o Non-combat events: attempt or ignore. Success grants items or +1 stat; failure deals HP damage, consumes an item, or reduces a stat.

o Boss shards & endings: Each boss drops a Chaos shard. Choose Destroy or Keep. After the last shard:
	o Purity (10 destroyed) – hailed as a legend
	o Good (6–9 destroyed) – world saved at great cost
	o Neutral (5 destroyed) – penance crusade
	o Bad (1–4 destroyed) – detained as corrupted
	o Traitor (0 destroyed) – join the Long War

	                                                 Styling Decisions (CSS):
o	Theme: Dark, high-contrast palette with subtle gradients; soft shadows, rounded cards.
o	Layout: Responsive grid cards; compact status “chips”; sticky nav with translucent backdrop.
o	Typography: System UI stack for clarity and performance.
o	UX polish: Scrollable combat log; action buttons grouped; consistent spacing; minimal motion.

													Accessibility Considerations: 
o Semantic structure: headings, lists, descriptive button text
o Color contrast: dark theme with high-contrast inks; emphasis via .good, .bad, .amber
o Live region: the battle/event log uses aria-live="polite" to announce updates
o Keyboard: all controls are standard buttons/links (Tab/Enter/Space work)
o Focus management: router moves focus to #app after navigation for screen reader continuity
                                                        How to Use

1. Click Game (or ▶ New Run), choose Class/Subfaction/Difficulty, optionally set a Seed.
2. Click Start to begin.
3. Read the log, choose actions, and advance room-by-room.
4. On boss defeat, decide the shard’s fate.
5. Reach Floor 10 and defeat the Chaos Lord for an ending based on your shard decisions.
