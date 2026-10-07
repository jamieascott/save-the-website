# Requirements: Save the Website — TY Engineering Escape Room

## 1. Overview

**Save the Website** is a browser-based escape room for Transition Year students aged approximately 15–16 visiting a company for an engineering workshop.

Students work in teams of approximately 3 people on their own laptop, iPad, or phone and solve a sequence of short puzzles to restore a locked school website before its launch.

### Core story

> **You're the engineering team. The new school website is launching in 45 minutes. Find the bugs, decode the system, fix the problems and get the School Website live.**

The experience should feel fun, achievable and competitive while still giving students an honest introduction to what engineers do.

The intended balance is approximately **50% fun escape-room experience / 50% engineering learning**.

No previous coding or engineering knowledge should be required.

---

## 2. Workshop Context

- Approximately **10–15 students** attend each workshop.
- At least **3 teams** will normally be formed.
- Teams should ideally contain **3 students**.
- One device may be shared by a team; not every student is guaranteed to have their own device.
- The full session is approximately **60 minutes**.
- Target structure:
  - 5 minutes briefing
  - 45 minutes gameplay
  - 10 minutes debrief and prizes
- The **fastest team to show its completion screen to an engineer wins**.

There is **no shared online leaderboard**. Results are verified manually by an engineer/facilitator.

---

## 3. Goals

### Student goals

- Give students a memorable, hands-on introduction to software engineering.
- Show that engineering is broader than coding.
- Demonstrate problem solving, data, debugging, security, UX, AI, communication and operations.
- Encourage teamwork and participation from students with different strengths.
- Build confidence by making every challenge achievable with guidance.

### Workshop goals

- Run with minimal setup.
- Require no company devices.
- Require no student accounts or personal information.
- Work reliably over guest Wi-Fi and, where possible, continue without requiring online services during gameplay.

---

## 4. Team Roles

Team roles are a core part of the experience.

### Driver

The student who controls the device:

- clicks
- types
- selects options
- interacts with the interface

### Navigator

The student who:

- reads the puzzle
- discusses the problem
- works through the logic
- checks the answer

### Role rotation

The team must **swap Driver and Navigator after every lock**.

The success panel after each lock should remind students to swap.

Example:

> 🔄 **Swap driver and navigator before the next lock.**

This is intended to prevent one confident student from controlling the entire game and encourage teamwork.

---

## 5. Constraints

### Device and network

- Students do not use company devices.
- Game must work on:
  - laptops
  - iPads
  - phones
- One device may be shared by a team.
- Students connect via guest Wi-Fi only.
- The application must have no route to internal company systems.

### Privacy

- No login.
- No account creation.
- No email address.
- No student names required.
- No personal data collection.
- Team name is the only user-entered identifier.
- No analytics or tracking.
- No results are sent to an external service.

### Delivery

- Single self-contained HTML page.
- Inline CSS and JavaScript.
- No backend.
- No database.
- No shared leaderboard.
- Game progress is stored only on the student's device.

---

## 6. Game Flow

The game should contain **10 sequential locks**.

A team cannot skip ahead.

### Start screen

The start screen must:

- explain the story in friendly language
- explain Driver/Navigator roles
- explain that roles swap after each lock
- allow a team name up to 30 characters
- provide a sensible default team name if blank
- provide a **Start the clock** button
- provide a **Resume saved game** option when saved progress exists

### Timer

- Gameplay timer starts at **45:00**.
- Countdown should be clearly visible throughout gameplay.
- At zero, the game **does not stop**.
- The label changes to:

> **Overtime — keep going!**

- Clock then counts upward to show overtime.

### Progress indicator

Display all 10 locks in a row or grid.

States:

- locked
- current
- open/completed

The current lock should be visually obvious.

### Lock completion

When a lock is solved:

1. Show a success message.
2. Explain briefly how the skill is used by engineers in real life.
3. Tell students to swap Driver/Navigator.
4. Provide a button to continue.

### Finish screen

After Lock 10:

> **Website is live!**

Show:

- team name
- completion time
- hints used
- engineering skills experienced

Then:

> **Show this screen to an engineer. Fastest team wins!**

---

## 7. Answer Handling

Each lock has one main answer submission area.

### Requirements

- Answers are case-insensitive.
- Spaces are ignored.
- Colons are ignored.
- Full stops are ignored.
- Meaningful punctuation such as `-` must **not** be removed when it is part of an answer.
- Equivalent answers can be accepted where appropriate.
- Wrong answers have no penalty.
- Blank submissions prompt the team to enter an answer.

### Security

Answers must not be stored as visible plain text in the page source, except where the puzzle explicitly requires the answer to be visible as part of the puzzle mechanic.

Preferred implementation:

- SHA-256 hashes in the HTML/JavaScript.
- Normalise the submitted answer before hashing.
- Compare against one or more stored hashes.

### Important lesson from earlier builds

Check every lock's hash independently during testing. Avoid reusing hashes accidentally across different locks.

---

## 8. Hints

Every lock must have a **Show a hint** button.

Each hint should:

- explain the method
- provide a strong nudge
- avoid giving away the answer
- reduce frustration for students with little technical background

Each hint use increments the team's hint count.

The finish screen shows the total hints used.

### Visual hint requirement

For locks involving alphabet shifting or alphabet indexing, the hint should contain a visible A–Z reference so students can count quickly.

For example:

```text
A B C D E F G H I J K L M
N O P Q R S T U V W X Y Z
```

This is required for:

- Lock 1
- Lock 3

---

# 9. Puzzle Sequence

## Lock 1 — Decode the Door

**Skill:** Binary + maths + logic

**Difficulty:** Easy

### Concept

Introduce binary visually without requiring previous knowledge.

Explain:

> Computers can represent information using 1s and 0s. Each position has a place value.

Use:

```text
16   8   4   2   1
```

Students decode six 5-bit binary groups into numbers and then letters.

Use the mapping:

```text
1 = A
2 = B
3 = C
...
26 = Z
```

### Puzzle answer

`UNLOCK`

### Hint

Must include a visible A–Z alphabet reference.

The hint should guide students to:

1. identify which place values correspond to 1s
2. add them
3. convert the resulting number to a letter

### Engineering explanation

Binary is a basic way computers represent information using two states.

---

## Lock 2 — Something's Wrong...

**Skill:** Logs + incident investigation

**Difficulty:** Easy

### Concept

Students investigate a mixed set of website log messages.

They must find the **first ERROR for the Payment Service**, ignoring:

- WARN messages
- search errors
- unrelated services

Example log data:

```text
09:38 INFO  Homepage loaded
09:39 INFO  Search service started
09:40 WARN  Payment service response slow
09:41 ERROR Payment service unavailable
09:42 INFO  Homepage loaded
09:43 ERROR Search service timeout
```

### Puzzle answer

`0941`

Accepted equivalent:

`941`

### Engineering explanation

Engineers use logs as evidence when investigating incidents instead of relying on guesses.

---

## Lock 3 — Crack the Message

**Skill:** Encryption + pattern recognition

**Difficulty:** Easy/Medium

### Concept

Use a simple Caesar cipher.

Show:

```text
FKHFNRXW
```

Instruction:

> The key is 3. Move each letter back 3 places in the alphabet.

Expected decoded word:

`CHECKOUT`

### Hint

Must include a visible A–Z alphabet reference.

The hint should explain the shifting method visually and remind students that the shift is **3 positions backwards**.

### Engineering explanation

Encryption changes information so it is harder for unauthorised people to read. This puzzle demonstrates a very simple transformation.

---

## Lock 4 — Fix the Bug

**Skill:** Debugging

**Difficulty:** Medium

### Required display layout

Each code line must be clearly displayed on a separate line.

```text
1. Price = 80
2. Discount = 20
3. Tax = 0
4. Total = Price
5. Total = Total + Discount
6. Display(Total)
```

### Student task

Ask:

> The discount should reduce the price. Which line contains the bug, and what should the corrected line be?

### Answer

The required answer is the **complete corrected line**:

`Total = Total - Discount`

### Important implementation requirement

The answer validation must preserve the `-` symbol.

Do **not** use a normalisation rule that removes hyphens/minus characters.

### Engineering explanation

Debugging is the process of finding the cause of incorrect software behaviour and making a focused correction.

---

## Lock 5 — School Data

**Skill:** Data + JSON

**Difficulty:** Medium

### Concept

Use familiar Irish city data.

Example JSON:

```json
{
  "orders": [
    {"city":"Dublin","items":2,"status":"confirmed"},
    {"city":"Cork","items":1,"status":"confirmed"},
    {"city":"Galway","items":3,"status":"cancelled"},
    {"city":"Limerick","items":2,"status":"confirmed"},
    {"city":"Waterford","items":2,"status":"cancelled"}
  ]
}
```

Explain JSON in plain English:

> JSON is a simple way of organising information so computers can read it.

### Student task

> How many items are actually being delivered? Cancelled orders do not count.

### Answer

`5`

### Engineering explanation

Engineers use structured data to make decisions and build software behaviour.

---

## Lock 6 — Design the Experience

**Skill:** UX + product thinking

**Difficulty:** Medium

This lock was positively received and should contain **several short UX questions** rather than one question only.

The objective is to show that engineering also involves thinking about users.

### UX Question 1 — Button clarity

Show several button labels and ask:

> Which button gives the clearest indication of what happens next?

Preferred correct choice:

`Register Now`

### UX Question 2 — Better design

Show two website designs and ask:

> Which design would be easier for most people to use?

The better design should demonstrate principles such as:

- readable text
- clear headings
- obvious actions
- good contrast
- simple navigation

### UX Question 3 — Mobile-first prioritisation

Show a simplified school website on a phone and ask which primary action should be easiest to reach.

The question should require students to think about the user's likely goal rather than simply identify a memorised UX rule.

### Interaction

Use visual selection, button selection, drag/reorder or another tactile interaction where practical.

Any drag interaction must have a non-drag alternative for accessibility.

### Engineering explanation

UX is about making technology easier and clearer for people to use. Engineers work with designers and product teams to improve the user journey.

---

## Lock 7 — Ask the AI

**Skill:** AI + prompt engineering

**Difficulty:** Medium

Students compare several prompts for a school website AI assistant.

The best prompt should give:

- role/context
- a clear task
- useful constraints

Example best-style prompt:

> You are a school website assistant. Recommend three after-school clubs for a new student. Keep the answer under 50 words.

### Student task

Select the best prompt and enter the associated code.

### Engineering explanation

Prompt engineering involves giving AI clear instructions and useful context to improve the usefulness and reliability of results.

---

## Lock 8 — Brand Challenge

**Skill:** Brand recognition + digital literacy

**Difficulty:** Medium

### Title requirement

Use:

> **Brand Challenge**

Do **not** use:

> Kids Brand Challenge

### Source questions

Use the five questions from the provided `kids_brand_quiz.md` source.

The source covers:

- worldwide brands
- social media brands
- ecommerce
- fashion brands

### Questions

1. Which brand is famous for the slogan “Just Do It”?
   - Adidas
   - Nike
   - Puma
   - Reebok

2. True or False: TikTok is a social media platform where users can create and watch short videos.

3. Which of these is best known as an online fashion shop?
   - ASOS
   - Spotify
   - Netflix
   - Nintendo

4. Which TWO of these are primarily social media platforms? Select both.
   - Instagram
   - Snapchat
   - Zara
   - Adidas

5. True or False: SHEIN is mainly known as a video game company.

### Answers from source

1. Nike
2. True
3. ASOS
4. Instagram and Snapchat
5. False

### Visual requirement

Add **logo-style visuals/images** for the featured brands where appropriate.

The visual treatment should remain accessible:

- meaningful images have alt text
- text labels remain available
- image recognition must not be the only way to understand the option

### Suggested interaction

Students answer all five questions.

Each correct answer reveals one character of a final brand code.

### Existing game answer

`BRAND`

---

## Lock 9 — Recognition Counts

**Skill:** Workhuman + recognition + rewards

**Difficulty:** Medium/Hard

### Story

The school website has a recognition and rewards feature.

Students earn points for positive contributions and can spend those points in the website store.

### Step 1 — Recognition

Students select three actions that deserve recognition.

Current intended positive actions:

- helping a classmate understand difficult homework
- sharing useful notes with someone who was absent
- thanking a teammate for doing a great job

Each correct recognition earns **10 points**.

### Step 2 — Store

Students have to actively select the **Hoodie**.

Example rewards:

| Reward | Cost |
|---|---:|
| Pen | 10 points |
| Bottle | 25 points |
| Hoodie | 30 points |
| Pizza voucher | 40 points |

Students must earn exactly **30 points** and then choose the **Hoodie**.

### Step 3 — Hidden word

Selecting the Hoodie unlocks the receipt.

The receipt contains hidden text that students must reveal by:

- highlighting/selecting the text on touch devices
- optionally using Inspect on a laptop where available

The hidden word is:

`WORKHUMAN`

### Answer

`WORKHUMAN`

### Engineering / Workhuman explanation

Recognition makes positive contributions visible and valued. The puzzle also demonstrates a simple connection between recognition, points and rewards.

### Important mobile requirement

The hidden word must be discoverable on iPad and phone without requiring developer tools.

---

## Lock 10 — Major Incident

**Skill:** Team communication + systems thinking + prioritisation

**Difficulty:** Hard / Final Boss

This should be the most collaborative lock.

### Objective

Students must act as an engineering team and **assign one engineer to each website problem**.

### Engineers

Use five fictional engineers with complementary specialties, for example:

- Reliability engineer
- Database engineer
- Performance engineer
- Search engineer
- Content engineer

### Incidents

Use five different website problems, including:

- website unavailable
- images loading slowly
- club description typo
- search slightly slow
- database connection failing

### Additional evidence

Show short on-call messages from the engineers.

Students should use evidence rather than guesses.

Example evidence:

> “I think the images are the problem.”

versus:

> “Database connections are failing.”

### Interaction

Students assign each engineer to one problem.

Each engineer must be used exactly once.

The final assignment should form a clear sequence or code.

### Existing final code

`READY`

The students should derive the code from the correct assignments rather than having the system reveal the code automatically.

### Engineering explanation

Incident response is about prioritising impact, using evidence, assigning the right people and communicating clearly under pressure.

---

# 10. Difficulty Curve

Difficulty should increase across the game.

| Lock | Difficulty |
|---|---|
| 1 | 🟢 Easy |
| 2 | 🟢 Easy |
| 3 | 🟢 Easy / Medium |
| 4 | 🟡 Medium |
| 5 | 🟡 Medium |
| 6 | 🟡 Medium |
| 7 | 🟡 Medium |
| 8 | 🟡 Medium |
| 9 | 🟠 Medium / Hard |
| 10 | 🔴 Hard / Final Boss |

The first puzzles should build confidence.

The final locks should require more discussion and teamwork.

---

# 11. Interaction Principles

The game should mix:

- typing
- selecting answers
- visual recognition
- code reading
- highlighting hidden text
- matching
- sorting
- lightweight drag/reorder interactions

Not every lock needs a drag interaction.

The game should avoid becoming a collection of generic multiple-choice questions.

### Accessibility requirement

Any drag/reorder interaction must also be possible using buttons, keyboard or another accessible control.

---

# 12. Visual / UX Requirements

### General

- Friendly, energetic style.
- Modern engineering/product feel.
- Suitable for 15–16 year olds.
- No childish “primary school” aesthetic.
- Fun without being overly corporate.
- Clear hierarchy and strong readability.

### Typography

- Body text at least 18 px.
- Highly legible font.
- Strong colour contrast.

### Responsive design

Must work down to approximately **360 px width**.

Support:

- portrait
- landscape
- mobile
- tablet
- desktop

Code, logs and data blocks should scroll within their own containers when necessary rather than causing page-wide horizontal scrolling.

### Touch targets

Interactive controls should be at least approximately **44 px**.

### Colour modes

Follow the user's:

- light mode
- dark mode

### Motion

Respect:

`prefers-reduced-motion`

Animations must not be essential to solving a puzzle.

---

# 13. Persistence

Use device-local storage to retain:

- team name
- current lock
- start time
- hints used
- Lock 8 state
- any required puzzle progress

A refresh should return the team to the same lock with the original timer still running.

### Reset

Provide:

> **Start over on this device**

It must:

- use an in-page confirmation panel/modal
- not rely on browser pop-up dialogs
- clear saved progress
- return to the start screen

### Versioning

A new game version must invalidate saved progress from older versions.

Use a versioned storage key, for example:

```text
saveWebsiteGame:v1.0.6
```

---

# 14. Privacy / Security

The application must:

- have no backend
- make no network calls for gameplay data
- use no analytics
- use no tracking
- collect no student personal data
- store team progress locally only

Puzzle answer checking may use SHA-256 hashes.

However, recognise that client-side puzzles are not cryptographically secure against a technically sophisticated participant. The goal is to prevent accidental discovery, not to create a secure assessment system.

Competition is ultimately verified by showing the completed screen to an engineer.

---

# 15. Facilitation

### Before the workshop

Test on at least:

- one laptop
- one iPad
- one phone

Test specifically:

- timer
- refresh/resume
- reset
- Lock 1 hint
- Lock 3 hint
- Lock 4 answer
- Lock 8 brand visuals
- Lock 8 hidden word interaction
- Lock 9 hoodie selection
- Lock 10 assignment flow

### During the workshop

Volunteers act as an **on-call engineering team**.

They should have an answer key containing:

- correct answer
- intended method
- one suggested coaching hint
- engineering explanation

Facilitators should avoid immediately giving answers. Encourage teams to reason through the problem.

### Winner

The fastest team to show the completed screen to an engineer wins.

There is no live shared leaderboard.

---

# 16. Out of Scope

Do not build:

- shared online leaderboard
- live cross-device scoring
- teacher/admin dashboard
- accounts/login
- student data collection
- stored results after the workshop
- random puzzle generation
- alternative puzzle sets
- company-system integrations
- access to internal Workhuman systems

---

# 17. Acceptance Criteria

## Core flow

- [ ] Team can start a new game.
- [ ] Team name is limited to 30 characters.
- [ ] Blank team name receives a default.
- [ ] Game starts a 45-minute timer.
- [ ] Ten locks are shown in order.
- [ ] Teams cannot skip locks.
- [ ] Lock progress is visible.
- [ ] Timer changes to overtime after 45 minutes and continues counting.
- [ ] Driver/Navigator reminder appears after every successful lock.
- [ ] Final screen shows team, time and hints.

## Answers

- [ ] Correct answers open the appropriate lock.
- [ ] Incorrect answers do not open the lock.
- [ ] Blank submission is handled gracefully.
- [ ] Answers are case-insensitive.
- [ ] Spaces, colons and full stops are ignored.
- [ ] Meaningful punctuation is preserved.
- [ ] Lock 4 accepts exactly the intended corrected line.
- [ ] No unintended hash collisions between locks.

## Specific puzzle acceptance

- [ ] Lock 1 decodes to `UNLOCK`.
- [ ] Lock 1 hint contains A–Z visual reference.
- [ ] Lock 2 accepts `0941` and `941`.
- [ ] Lock 3 decodes to `CHECKOUT`.
- [ ] Lock 3 hint contains A–Z visual reference.
- [ ] Lock 4 displays each line separately.
- [ ] Lock 4 answer is `Total = Total - Discount`.
- [ ] Lock 5 answer is `5`.
- [ ] Lock 6 contains multiple UX questions.
- [ ] Lock 7 teaches basic prompt engineering.
- [ ] Lock 8 title is `Brand Challenge`.
- [ ] Lock 8 includes brand visuals/logos.
- [ ] Lock 8 uses the five supplied quiz questions.
- [ ] Lock 9 requires selecting the Hoodie.
- [ ] Lock 9 hidden word is `WORKHUMAN`.
- [ ] Lock 9 works on phone/iPad without Inspect.
- [ ] Lock 10 requires engineer-to-incident assignment.
- [ ] Lock 10 final code is derived from the assignments and is `READY`.

## Persistence

- [ ] Refreshing mid-game restores the current lock.
- [ ] Timer continues from the original start time.
- [ ] Hints remain counted.
- [ ] Lock 8 progress remains saved.
- [ ] Reset works without browser pop-ups.
- [ ] New game versions invalidate old saved progress.

## Devices

- [ ] Works on current Chrome.
- [ ] Works on current Safari.
- [ ] Works on current Edge.
- [ ] Works on current Firefox.
- [ ] Works on laptop.
- [ ] Works on iPad.
- [ ] Works on phone.
- [ ] Usable around 360 px width.
- [ ] No page-level sideways scrolling.
- [ ] Meaningful content remains accessible in light and dark mode.

---

# 18. Suggested Technical Structure

A simple single-file implementation is preferred:

```text
save-the-website.html
```

Recommended high-level structure:

```text
HTML
├── Start screen
├── Game shell
│   ├── Status bar
│   ├── Timer
│   ├── Lock progress
│   └── Puzzle container
├── Finish screen
└── Reset confirmation

CSS
├── Responsive layout
├── Light/dark mode
├── Accessibility/focus states
└── Puzzle-specific UI

JavaScript
├── Game state
├── Timer
├── Local persistence
├── Version handling
├── Answer hashing
├── Puzzle rendering
├── Hint tracking
├── Lock progression
├── Lock-specific interactions
└── Finish screen
```

Keep lock-specific puzzle data separate from rendering/engine logic where practical so future puzzle edits are easy.

---

# 19. Future Improvements

Potential later enhancements, but **not required for the current build**:

- Workhuman visual branding
- richer animations
- sound effects with mute control
- facilitator answer-key mode
- printable workshop materials
- QR code start poster
- more advanced accessibility testing
- additional UX / AI / cybersecurity puzzles
- optional workshop-specific themes

Do not add these until the core student experience has been play-tested.

---

# 20. Design Principle

The most important principle for future rebuilds is:

> **Students should feel like engineers, not like they are sitting an engineering exam.**

Every puzzle should answer at least one of these questions:

- Can students discover something?
- Can students reason about a problem?
- Can students work together?
- Can students see how this relates to real engineering?
- Can a student with no coding experience still contribute?

The experience should finish with students thinking:

> **“That was fun — and I can see what engineers actually do.”**
