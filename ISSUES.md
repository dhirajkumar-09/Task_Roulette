# 📋 GitHub Issues Roadmap for Task Roulette

You can copy and paste these directly into [GitHub Issues](https://github.com/dhirajkumar-09/Task_Roulette/issues/new) for project tracking, feature planning, and contributor onboarding.

---

### Issue 1: [Feature] Add Audio Volume Slider in UI
- **Label**: `enhancement`, `ui/ux`
- **Description**: Currently, sound can only be toggled ON or OFF (🔊/🔇). Add a volume range slider (0% to 100%) in the header settings modal so users can adjust ticking and chime volume levels without muting completely.
- **Tasks**:
  - [x] Add `<input type="range" min="0" max="1" step="0.05">` in header.
  - [x] Connect slider value to Web Audio API `gainNode.gain.value`.
  - [x] Persist user volume preference in `localStorage`.

---

### Issue 2: [Feature] Add Task Priority / Tags (High, Medium, Low)
- **Label**: `enhancement`, `database`
- **Description**: Allow users to assign priorities (`HIGH`, `MED`, `LOW`) or tags (e.g., `#study`, `#work`, `#fitness`) when adding tasks.
- **Tasks**:
  - [x] Add `priority` column to SQLite `tasks` table (`ALTER TABLE tasks ADD COLUMN priority TEXT DEFAULT 'MED'`).
  - [x] Update POST & PUT endpoints to accept priority parameter.
  - [x] Add colored priority badges in frontend task cards.

---

### Issue 3: [Feature] Weighted Roulette Wheel Based on Priority
- **Label**: `enhancement`, `algorithm`
- **Description**: Make high-priority tasks have wider wheel sectors (higher probability of being picked) on the roulette wheel.
- **Tasks**:
  - [x] Calculate sector arc dynamically based on task priority weights (High: 3x, Med: 2x, Low: 1x).
  - [x] Update `drawWheel()` slice angles according to weight distribution.
  - [x] Adjust winning sector calculation logic to match weighted probability.

---

### Issue 4: [Feature] Sound Effect Options / Sound Themes
- **Label**: `enhancement`, `audio`
- **Description**: Provide multiple sound packs (e.g., Casino Roulette, 8-Bit Arcade, Soft Zen Chimes) instead of a single synthesizer sound set.
- **Tasks**:
  - [x] Create Web Audio oscillator presets for each theme.
  - [x] Add a sound theme selector dropdown in settings.
  - [x] Save selected theme in `localStorage`.

---

### Issue 5: [Bug/Enhancement] Prevent Duplicate Task Names
- **Label**: `bug`, `validation`
- **Description**: Currently, duplicate task names can be added multiple times. Add validation to alert user if an identical incomplete task already exists.
- **Tasks**:
  - [x] Add backend check in `handlePost` for existing active tasks with identical text.
  - [x] Show friendly toast warning in UI if duplicate task is entered.

---

### Issue 6: [Feature] Export & Import Tasks (JSON / CSV Backup)
- **Label**: `enhancement`, `data`
- **Description**: Allow users to export all tasks and streak history to a `.json` or `.csv` file and import it back to another device.
- **Tasks**:
  - [x] Create `GET /api/export` endpoint returning full JSON dump.
  - [x] Create `POST /api/import` endpoint to load tasks into SQLite.
  - [x] Add Export/Import buttons in the UI settings panel.

---

### Issue 7: [Feature] Keyboard Shortcuts for Power Users
- **Label**: `enhancement`, `accessibility`
- **Description**: Enable keyboard navigation and shortcuts for faster task management and wheel spinning.
- **Tasks**:
  - [x] `Spacebar` / `S`: Spin roulette wheel.
  - [x] `T`: Start / Pause focus timer.
  - [x] `R`: Reset timer.
  - [x] `/`: Focus task input field.
  - [x] `Escape`: Close modals and unfocus.

---

### Issue 8: [Feature] Browser Push Notifications when Focus Timer Finishes
- **Label**: `enhancement`, `notifications`
- **Description**: When the focus timer reaches `00:00`, send a native browser notification (via Notification API) so the user gets notified even if the browser tab is minimized or in the background.
- **Tasks**:
  - [x] Request `Notification.requestPermission()` on first timer start.
  - [x] Trigger `new Notification('Focus session complete! 🎉')` at `00:00`.
  - [x] Play chime sound in background tab if allowed.

---

### Issue 9: [Feature] Task Edit In-Place (Rename Task)
- **Label**: `enhancement`, `ui/ux`
- **Description**: Allow double-clicking or clicking an edit icon ✏️ on an existing task card to edit its text without deleting and re-adding.
- **Tasks**:
  - [x] Add ✏️ edit button to task action buttons.
  - [x] Convert task title to editable inline input on click.
  - [x] Send `PUT /api/tasks/{id}` with new text on Enter or blur.

---

### Issue 10: [Feature] Dark/Light Theme Auto-Sync with System Preference
- **Label**: `enhancement`, `ui/ux`
- **Description**: Automatically detect OS color scheme (`prefers-color-scheme: dark`) on first visit while preserving manual toggle overrides.
- **Tasks**:
  - [x] Add `window.matchMedia('(prefers-color-scheme: dark)')` listener in frontend JS.
  - [x] Update theme automatically if user hasn't explicitly set a preference in `localStorage`.

---

### Issue 11: [DevOps] Add Dockerfile and docker-compose.yml
- **Label**: `devops`, `infrastructure`
- **Description**: Containerize the Java application so anyone can run it with a single command without installing local JDK manually.
- **Tasks**:
  - [x] Create multi-stage `Dockerfile` with Eclipse Temurin Java 17.
  - [x] Add `docker-compose.yml` mapping port 8080 and mounting SQLite volume for database persistence.
  - [x] Update `README.md` with Docker run instructions.

---

### Issue 12: [DevOps] Add GitHub Actions CI Workflow for Automated Compilation Tests
- **Label**: `ci/cd`, `automation`
- **Description**: Set up automated tests on pull requests and pushes to ensure code compiles and starts properly on Linux and Windows runners.
- **Tasks**:
  - [x] Create `.github/workflows/ci.yml`.
  - [x] Add steps to compile `TaskRouletteServer.java` with SQLite driver on JDK 17.
  - [x] Run automated API endpoint smoke tests using curl.

---

### Issue 13: [Feature] Daily & Weekly Productivity Stats Modal
- **Label**: `enhancement`, `analytics`
- **Description**: Add an analytics modal displaying total focus hours completed, average daily tasks done, and a monthly heatmap calendar.
- **Tasks**:
  - [x] Create `GET /api/stats` endpoint summarizing completed tasks by month/week.
  - [x] Design SVG / Canvas heatmap (similar to GitHub contributions graph).
  - [x] Add "View Analytics 📊" button in header.

---

### Issue 14: [Security/Performance] Add Rate Limiting and Input Sanitization
- **Label**: `security`, `backend`
- **Description**: Protect endpoints against rapid spamming and sanitize text inputs against XSS and SQL injection.
- **Tasks**:
  - [x] Enforce max character limit (150 chars) on task text in Java backend.
  - [x] Add in-memory sliding window rate limiter in `TaskRouletteServer`.
  - [x] Validate and escape HTML tags properly on server responses.

---

### Issue 15: [Feature] Pomodoro Break Interval (Short & Long Breaks)
- **Label**: `enhancement`, `timer`
- **Description**: Implement a complete Pomodoro cycle (25 min focus $\rightarrow$ 5 min short break $\rightarrow$ repeat 4x $\rightarrow$ 15 min long break) with automatic mode switching.
- **Tasks**:
  - [x] Add state machine for `FOCUS`, `SHORT_BREAK`, and `LONG_BREAK`.
  - [x] Add visual badge indicating current cycle (e.g., "🍅 Cycle 2 of 4").
  - [x] Prompt user when break starts and ends with custom colors.

---

### Issue 16: [Docs] Improve README with Comprehensive Setup Guide
- **Label**: `documentation`, `good first issue`
- **Description**: Improve README with project overview, UI screenshots, badges, local/Docker setup guide, API reference, and contributing guidelines.
- **Tasks**:
  - [x] Write project description at the top with live demo link.
  - [x] Add high-definition UI preview graphic (`docs/preview.svg`).
  - [x] Add comprehensive feature list and tech stack documentation.
  - [x] Add detailed local setup steps for Windows and macOS/Linux.
  - [x] Add Docker and Docker Compose run instructions.
  - [x] Add complete API table with all endpoints and examples.
  - [x] Add project structure layout and contributing guide.
  - [x] Add MIT license and status badges.

---

### Issue 17: [Feature] Task Search & Filter by Keyword or Priority Tag (#36)
- **Label**: `enhancement`, `ui/ux`, `good first issue`
- **Description**: Add real-time search input bar above the task list to let users filter tasks instantly by keywords or priority tags (#tag, high/med/low).
- **Tasks**:
  - [ ] Add a search input with a search icon above the task list.
  - [ ] Filter task cards in real-time on the `input` event.
  - [ ] Support priority filtering (e.g., typing `HIGH`, `MED`, or `LOW`).
  - [ ] Add a clear button inside or next to the search input.
  - [ ] Show a friendly empty state when no tasks match the filter.

---

### Issue 18: [Feature] Task Due Dates & Overdue Badges (#37)
- **Label**: `enhancement`, `database`, `good first issue`
- **Description**: Allow users to optionally set a due date for tasks when creating or editing them. Display color-coded badges indicating if a task is due today, in the future, or overdue.
- **Tasks**:
  - [ ] Add a `due_date` column to SQLite `tasks` table (`ALTER TABLE tasks ADD COLUMN due_date TEXT DEFAULT NULL`).
  - [ ] Update `POST /api/tasks` and `PUT /api/tasks/{id}` to accept and return `dueDate`.
  - [ ] Add optional HTML date picker in the task creation form.
  - [ ] Render due date pill badge on task items with relative indicator (e.g. "Overdue", "Today", "Oct 25").

---

### Issue 19: [Feature] Custom Wheel Color Palettes & Theme Customizer (#38)
- **Label**: `enhancement`, `ui/ux`, `good first issue`
- **Description**: Give users the ability to customize the visual appearance of the roulette wheel by choosing from multiple curated color palettes instead of only the default palette.
- **Tasks**:
  - [ ] Define palette objects with hex color arrays in JavaScript.
  - [ ] Add a "Wheel Color Theme" dropdown selector in the profile/settings modal.
  - [ ] Persist the user's selected palette in `localStorage` (`tr_wheel_palette`).
  - [ ] Dynamically redraw the canvas roulette wheel whenever the palette changes.

---

### Issue 20: [Feature] Ambient Background Sounds for Focus Timer (White Noise / Rain / Zen) (#39)
- **Label**: `enhancement`, `audio`, `good first issue`
- **Description**: Add optional relaxing ambient background soundscapes generated directly via the Web Audio API during focus sessions to improve concentration.
- **Tasks**:
  - [ ] Synthesize continuous noise buffers using Web Audio API AudioBufferSourceNode.
  - [ ] Add an ambient sound toggle & selector in the Focus Timer card.
  - [ ] Start audio automatically when focus timer starts; fade out when paused/stopped.
  - [ ] Tie ambient audio volume to the header master volume slider.

---

### Issue 21: [Feature] Task Notes & Expandable Subtasks / Checklist (#40)
- **Label**: `enhancement`, `ui/ux`, `good first issue`
- **Description**: Allow users to attach short notes or mini-checklist items to any task, making it easier to break complex goals into small steps before spinning the wheel.
- **Tasks**:
  - [ ] Add `notes` TEXT column to SQLite `tasks` table (`ALTER TABLE tasks ADD COLUMN notes TEXT DEFAULT ''`).
  - [ ] Update backend API (`POST`, `PUT`, `GET`) to include the notes field.
  - [ ] Add an expand/collapse arrow (▾/▴) on task cards to reveal notes.
  - [ ] Allow editing notes in-place.

---

### Issue 22: [Feature] Customizable Celebration Particles & Confetti Styles (#41)
- **Label**: `enhancement`, `ui/ux`, `good first issue`
- **Description**: Make the victory celebration even more satisfying when winning a wheel spin or finishing a focus session by adding multiple confetti particle modes.
- **Tasks**:
  - [ ] Expand the canvas particle engine to draw shapes (stars, circles, emoji glyphs).
  - [ ] Add celebration style setting in the settings modal.
  - [ ] Save preference in `localStorage` (`tr_celebration_style`).
  - [ ] Trigger mini particle burst when checking off a task as done.

---

### Issue 23: [Feature] Drag-and-Drop Task Reordering for Custom Priority (#42)
- **Label**: `enhancement`, `ui/ux`, `good first issue`
- **Description**: Allow users to manually reorder tasks in their task list by dragging and dropping them into their preferred sequence.
- **Tasks**:
  - [ ] Add an optional `position` integer column in SQLite `tasks` table.
  - [ ] Implement HTML5 Drag and Drop API events (`dragstart`, `dragover`, `drop`, `dragend`).
  - [ ] Add a drag handle icon (`⋮⋮`) to each task card.
  - [ ] Update task positions on drop and send order update to backend (`PUT /api/tasks/reorder`).

---

### Issue 24: [Feature] Daily Goal Tracker & Target Progress Bar (#43)
- **Label**: `enhancement`, `analytics`, `good first issue`
- **Description**: Add a daily goal completion tracker (e.g. "Goal: 5 tasks today") to encourage daily habit building and gamify productivity alongside streaks.
- **Tasks**:
  - [ ] Add daily goal setting input in the user profile modal.
  - [ ] Calculate progress towards today's goal from completed tasks count.
  - [ ] Render a progress bar or circular progress indicator in the daily streak bar.
  - [ ] Show congratulations toast and sound when hitting 100% of the daily goal.

---

### Issue 25: [Feature] Offline Support & Progressive Web App (PWA) Manifest (#44)
- **Label**: `enhancement`, `infrastructure`, `good first issue`
- **Description**: Convert Task Roulette into an installable Progressive Web App (PWA) so users can install it on their phones, tablets, or desktop systems and access the app offline.
- **Tasks**:
  - [ ] Create `static/manifest.json` with app metadata and standard icon sizes (192x192, 512x512).
  - [ ] Create a lightweight `static/sw.js` service worker caching essential app assets.
  - [ ] Register the service worker in `static/index.html`.
  - [ ] Handle `beforeinstallprompt` to show an install button for eligible browsers.

---

### Issue 26: [Feature] Fullscreen Zen Focus Mode for Timer (#45)
- **Label**: `enhancement`, `accessibility`, `good first issue`
- **Description**: Provide a distraction-free Fullscreen Zen Mode for the Focus Timer that hides all surrounding UI (task list, wheel, header) and displays only the active task and a countdown dial.
- **Tasks**:
  - [ ] Add Zen Mode button (⛶) in the Focus Timer card header.
  - [ ] Add full-screen CSS styles (`.zen-active`) with smooth transition and backdrop blur.
  - [ ] Bind keyboard shortcut (`F`) to toggle Zen Mode.
  - [ ] Ensure timer controls (Start / Pause / Reset) remain accessible in Zen Mode.

