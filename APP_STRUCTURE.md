# BLOCKADORO Application Structure Documentation

## Overview
BLOCKADORO is a personal proof-of-work timer application that tracks Bitcoin block mining sessions. It features dual timing modes (block-based and minute-based) with real-time Bitcoin data integration.

---

## 🏗️ Application Sections

### 1. **Header Section** (`<header>`)
- **Purpose**: Brand identity and application title
- **Elements**:
  - Brand logo (orange orb)
  - "BLOCKADORO" title
  - Tagline: "A personal proof-of-work timer"

### 2. **Session Timer Section** (`<section class="panel timer-panel">`)
- **Purpose**: Main timer interface and controls
- **Key Elements**:
  - Session Timer title (centered)
  - Large timer display (`timer-time`)
  - Start/Reset action buttons
  - Mode selector (Block-based vs Minute-based)
  - Block/Minute input controls with increment/decrement buttons
  - Estimated session duration display
  - Block statistics (time since last block, durations)

### 3. **Data Cards Section** (`<section class="cards">`)
- **Purpose**: Optional data displays (toggleable)
- **Cards**:
  - **Current Time Card** (`card-time`): Shows current time in selected timezone
  - **Bitcoin Block Height Card** (`card-block`): Shows current Bitcoin block height
  - **Bitcoin Price Card** (`card-price`): Shows current BTC price in USD

### 4. **Settings Section** (`<section class="panel">`)
- **Purpose**: User preferences and configuration
- **Controls**:
  - Toggle switches for showing/hiding data cards
  - Timezone selector dropdown

### 5. **Footer Section**
- **Purpose**: Credits and developer tools
- **Elements**:
  - Data source credits (mempool.space, CoinGecko)
  - Developer toggle button for testing success messages

### 6. **Overlay Section** (`#block-mined-overlay`)
- **Purpose**: Full-screen notifications for block mining events
- **Usage**: Shows "Block Mined!" or completion messages

---

## 🎮 Controllers & UI Elements

### Timer Controls
- `timer-start-pause` - Start/Pause button
- `timer-reset` - Reset button
- `timing-mode-select` - Mode dropdown (Block-based/Minute-based)
- `blocks-input` - Number input for blocks to mine (1-5)
- `minutes-input` - Number input for minutes to work (10-180)
- `blocks-increment` / `blocks-decrement` - Block count buttons
- `minutes-increment` / `minutes-decrement` - Minute count buttons

### Data Card Toggles
- `cb-time` - Toggle for Current Time card
- `cb-block` - Toggle for Block Height card
- `cb-price` - Toggle for BTC Price card

### Settings Controls
- `tz-select` - Timezone selector dropdown

### Display Elements
- `timer-time` - Main timer display (large orange text)
- `session-complete` - Success banner (hidden by default)
- `session-complete-text` - Success message text
- `timer-meta` - Estimated session duration
- `since-last-block` - Time since last block
- `last-block` - Last block duration
- `avg-block` - Average block duration

---

## ⚙️ Core Functions

### Timer Management Functions

#### `startTimer()`
- **Purpose**: Starts the timer session
- **Actions**:
  - Sets `blockTimerState.isRunning = true`
  - Disables mode selector and relevant input controls
  - Initializes session watcher
  - Starts tick interval

#### `pauseTimer(setPausedLabel = true)`
- **Purpose**: Pauses the timer session
- **Actions**:
  - Sets `blockTimerState.isRunning = false`
  - Re-enables all controls
  - Stops tick interval
  - Ends session watcher

#### `resetTimer()`
- **Purpose**: Resets timer to initial state
- **Actions**:
  - Calls `pauseTimer()`
  - Resets elapsed time to 0
  - Recalculates target time
  - Updates display

#### `scheduleTick()`
- **Purpose**: Sets up timer tick interval (250ms)
- **Actions**:
  - Updates elapsed time
  - Calls `renderTimer()`
  - Checks for minute-based completion

### Input Validation Functions

#### `getBlocksCount()`
- **Purpose**: Validates and returns block count
- **Range**: 1-5 blocks
- **Returns**: Validated integer

#### `getMinutesCount()`
- **Purpose**: Validates and returns minute count
- **Range**: 10-180 minutes
- **Returns**: Validated integer

### Display Functions

#### `renderTimer()`
- **Purpose**: Updates timer display
- **Actions**:
  - Formats elapsed time
  - Updates timer text
  - Calls `updateTargetLabel()`

#### `formatDuration(ms)`
- **Purpose**: Formats milliseconds to MM:SS or HH:MM:SS
- **Returns**: Formatted time string

#### `updateTargetLabel()`
- **Purpose**: Updates estimated session duration display
- **Actions**:
  - Shows/hides based on timing mode
  - Calculates and displays estimated duration

#### `updateSinceLastBlockLabel()`
- **Purpose**: Updates "time since last block" display
- **Actions**:
  - Calculates time since last known block
  - Updates display text

### Session Management Functions

#### `beginSessionWatcher()`
- **Purpose**: Starts block monitoring for active sessions
- **Actions**:
  - Sets up polling interval (15 seconds)
  - Initializes session state
  - Only active for block-based timing

#### `endSessionWatcher()`
- **Purpose**: Stops block monitoring
- **Actions**:
  - Clears polling interval
  - Resets session state

#### `pollTipHeightForSession()`
- **Purpose**: Polls Bitcoin network for new blocks
- **Actions**:
  - Fetches current block height
  - Detects new blocks
  - Updates session progress
  - Triggers completion events

### Data Fetching Functions

#### `fetchBlockHeightOnce()`
- **Purpose**: Fetches current Bitcoin block height
- **Source**: mempool.space API
- **Actions**:
  - Updates block height display
  - Detects new blocks
  - Updates timestamps

#### `fetchPriceOnce()`
- **Purpose**: Fetches current Bitcoin price
- **Source**: CoinGecko API
- **Actions**:
  - Updates price display
  - Updates metadata

#### `fetchLastBlockTime()`
- **Purpose**: Fetches detailed block information
- **Actions**:
  - Gets block timestamps
  - Updates average block duration
  - Updates last block duration

### Utility Functions

#### `computeEffectiveTargetMs()`
- **Purpose**: Calculates target session duration
- **Logic**:
  - Block-based: Calculates based on blocks and current block progress
  - Minute-based: Converts minutes to milliseconds

#### `getResolvedTimezone(selection)`
- **Purpose**: Resolves timezone selection to actual timezone
- **Returns**: Valid timezone string

#### `formatTimeInSelectedTimezone(dateObj)`
- **Purpose**: Formats time in selected timezone
- **Returns**: Formatted time string

#### `showOverlayMessage(message, durationMs, vibratePattern)`
- **Purpose**: Shows full-screen overlay message
- **Actions**:
  - Displays message
  - Triggers vibration (if supported)
  - Auto-hides after duration

### Button State Management Functions

#### `updateBlocksButtonsDisabled()`
- **Purpose**: Enables/disables block increment/decrement buttons
- **Logic**: Disables at min/max values (1-5)

#### `updateMinutesButtonsDisabled()`
- **Purpose**: Enables/disables minute increment/decrement buttons
- **Logic**: Disables at min/max values (10-180)

### Preference Management Functions

#### `loadInitialPreferences()`
- **Purpose**: Loads saved user preferences on startup
- **Actions**:
  - Loads from localStorage
  - Sets default values
  - Configures UI state

#### `savePreferences()`
- **Purpose**: Saves current user preferences
- **Actions**:
  - Saves to localStorage
  - Persists all user settings

---

## 🔄 State Management

### Global State Objects

#### `blockTimerState`
```javascript
{
  isRunning: false,        // Timer running state
  startEpochMs: null,      // Session start timestamp
  elapsedMs: 0,           // Elapsed time in milliseconds
  targetMs: TEN_MINUTES_MS, // Target duration
  tickIntervalId: null     // Tick interval reference
}
```

#### `sessionState`
```javascript
{
  isActive: false,         // Session active state
  targetBlocks: 0,         // Target blocks for session
  startHeight: null,       // Starting block height
  lastSeenHeight: null,    // Last seen block height
  blocksMined: 0,         // Blocks mined in session
  pollIntervalId: null     // Polling interval reference
}
```

### Interval Management
- `timeIntervalId` - Clock update interval (1 second)
- `blockIntervalId` - Block height polling interval (30 seconds)
- `priceIntervalId` - Price polling interval (60 seconds)
- `lastBlockPollIntervalId` - Block detail polling interval (30 seconds)

---

## 🎨 CSS Classes & Styling

### Key CSS Classes
- `.timer-time` - Large timer display styling
- `.success-banner` - Completion message styling
- `.blocks-input` - Number input styling (hides browser spinners)
- `.btn` / `.btn-secondary` / `.btn-icon` - Button styling variants
- `.card` - Data card container styling
- `.hidden` - Utility class for hiding elements
- `.panel` - Section container styling

### CSS Variables
- `--bitcoin-orange: #f2a900` - Primary accent color
- `--bg-0` / `--bg-1` - Background colors
- `--text` - Primary text color
- `--muted` - Secondary text color
- `--card` - Card background color
- `--accent-dim` - Dimmed accent color

---

## 🔌 Event Listeners

### Timer Events
- `timer-start-pause` click → `startTimer()` / `pauseTimer()`
- `timer-reset` click → `resetTimer()`
- `timing-mode-select` change → Mode switching logic
- `blocks-input` / `minutes-input` change → Input validation and updates

### Button Events
- `blocks-increment` / `blocks-decrement` click → Value adjustment
- `minutes-increment` / `minutes-decrement` click → Value adjustment

### Settings Events
- `tz-select` change → Timezone updates
- `cb-time` / `cb-block` / `cb-price` change → Card visibility toggles

### Developer Events
- `dev-toggle-success` click → Success banner testing

---

## 📱 Responsive Design

### Breakpoints
- **Mobile**: Default layout (single column)
- **Desktop** (640px+): Multi-column layout for controls

### Responsive Elements
- Timer display: `clamp(48px, 8vw, 96px)` font size
- Clock display: `clamp(38px, 7vw, 80px)` font size
- Overlay text: `clamp(28px, 5.6vw, 64px)` font size

---

## 🔧 Developer Tools

### Success Banner Toggle
- **Element**: `dev-toggle-success` button
- **Purpose**: Test success message display
- **Function**: Toggles `session-complete` visibility

### Console Debugging
- All major functions include error handling with try/catch blocks
- Failed API calls display error messages in metadata
- Timer state can be inspected via `blockTimerState` object

---

## 📋 Usage Examples

### Starting a Block-Based Session
1. Select "Block-based" mode
2. Set desired number of blocks (1-5)
3. Click "Start" button
4. Timer runs until target blocks are mined

### Starting a Minute-Based Session
1. Select "Minute-based" mode
2. Set desired minutes (10-180)
3. Click "Start" button
4. Timer runs for specified duration

### Monitoring Progress
- Timer display shows elapsed time
- Block statistics update in real-time
- Overlay notifications for new blocks
- Success banner on completion

---

*This documentation covers BLOCKADORO version 0.2. For updates, refer to the latest version.*
