                                                        Overview
This is a Single Page Application (SPA) that simulates a Magic 8 Ball. The user types a question, clicks a button, waits while the “magic is happening,” and then receives a random response—all without any page reloads. 

                                            Architecture & Technical Choices
•	SPA Model: One HTML document loaded once; all interaction happens by DOM updates (no navigation, no backend).
•	Language/Stack:
o	HTML for structure
o	CSS (embedded <style>) for simple visual design
o	JavaScript (vanilla ES6) for interactivity
•	Event Handling: A click on the Ask button triggers the logic (inline onclick="shakeBall()" in this version).

                                                      State & Logic:
o	Answers stored in a small array
o	Random selection via Math.random() + Math.floor()
o	5-second delay implemented with setTimeout(5000) to simulate “shaking” and build anticipation
o	A lightweight animated status (“The magic is happening…”) using setInterval to pulse dots
o	Button disabled during the delay to prevent overlapping requests

	                                                 Styling Decisions (CSS):
o	Minimalist, centered layout; soft background #f0f8ff
o	Readable defaults (Arial) and clear visual hierarchy
o	min-height on status/answer regions to avoid layout “jump”
o	Disabled button style (opacity: 0.6; cursor: not-allowed) for clear feedback

•	Accessibility Considerations: Clear text, large controls, and predictable focus/interaction. (Future improvement: add aria-live="polite" to status/answer containers.)
Features
•	Type any question
•	“Shaking/magic” status with animated dots
•	Randomized answer from a predefined set
•	Debounced interaction (button disabled during wait)
•	Works fully offline (static assets only)

                                                        How to Use
1.	Open the live site: https://tommylenot.github.io/CS-39AF-Lenot
2.	Enter a question.
3.	Click Ask the Magic 8 Ball.
4.	Wait ~5 seconds while the magic happens; your answer will appear.

