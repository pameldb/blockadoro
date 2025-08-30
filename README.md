# BLOCKADORO
A personal proof-of-work timer that connects your productivity sessions to the Bitcoin network.

## Features

### 🕒 **Dual Timing Modes**
- **Block-based timing**: Set sessions by number of blocks to mine (1-10 blocks)
- **Minute-based timing**: Set sessions by duration (10-180 minutes in 10-minute increments)
- Easy mode switching with dropdown selector
- Automatic session completion detection for both modes

### ⏱️ **Timer Controls**
- Start/Pause/Reset functionality
- Real-time session progress tracking
- Estimated session duration display (block-based mode)
- Session completion celebrations with custom messages
- Input controls disabled during active sessions

### 📊 **Bitcoin Integration**
- Real-time Bitcoin block height tracking
- Live Bitcoin price monitoring
- Block mining notifications with haptic feedback
- Average block duration statistics (last 10 blocks)
- Time since last block tracking

### 🎨 **User Interface**
- Modern Bitcoin-themed design with orange accents
- Responsive layout for desktop and mobile
- Configurable timezone support
- Toggle controls for block height, price, and time displays
- Clean, intuitive controls with proper spacing and alignment

### 📱 **Mobile Experience**
- Touch-friendly interface
- Haptic feedback on mobile devices
- Responsive design that works on all screen sizes
- Optimized for both portrait and landscape orientations

## Data Sources
- **Block height**: [mempool.space](https://mempool.space/)
- **Bitcoin price**: [CoinGecko](https://www.coingecko.com/)

## Version History

### v0.2 (Current)
- ✨ **NEW**: Dual timing modes (block-based vs minute-based)
- ✨ **NEW**: Enhanced UI with better spacing and alignment
- ✨ **NEW**: Comprehensive application documentation
- ✨ **NEW**: Increased max blocks from 5 to 10
- ✨ **NEW**: 10-minute increments for minute-based timing
- ✨ **NEW**: Improved session completion messages
- ✨ **NEW**: Better button state management
- ✨ **NEW**: Version backup system (v0.1, v0.2)

### v0.1
- Initial release with block-based timing
- Basic Bitcoin integration
- Core timer functionality

## Getting Started

1. **Choose your timing mode**:
   - **Block-based**: Set how many blocks you want to mine (1-10)
   - **Minute-based**: Set how long you want to work (10-180 minutes)

2. **Start your session**: Click "Start" to begin tracking

3. **Stay focused**: The timer will track your progress and notify you when blocks are mined

4. **Complete your session**: Get a congratulations message when you reach your goal!

## Technical Details

- **Frontend**: Pure HTML/CSS/JavaScript (no frameworks)
- **APIs**: RESTful APIs for Bitcoin data
- **Storage**: Local browser storage for preferences
- **Compatibility**: Modern browsers with ES6+ support

## Development

For detailed technical documentation, see [APP_STRUCTURE.md](APP_STRUCTURE.md) which provides a comprehensive reference for all application sections, controllers, and functions.
