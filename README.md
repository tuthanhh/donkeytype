# DonkeyType

A simple typing speed test app inspired by [Monkeytype](https://monkeytype.com), built with Vue 3.

## Features

- Random word generation for typing practice
- Real-time feedback on correct/incorrect keystrokes
- Keyboard navigation (Tab to restart)
- Responsive, accessible UI
- Sticky header and info area

## Tech Stack

- [Vue 3](https://vuejs.org/) (Composition API)
- [Vite](https://vitejs.dev/) for development/build
- [Pinia](https://pinia.vuejs.org/) for state management
- [Vue Router](https://router.vuejs.org/) for routing

## Getting Started
(Will update later)
1. **Install dependencies:**
   ```bash
   npm install
   ```
2. **Run the development server:**
   ```bash
   npm run dev
   ```
3. **Open your browser:**
   Visit [http://localhost:5173](http://localhost:5173)

## Usage

- Click the typing area to focus and start typing.
- Press <kbd>Tab</kbd> to get a new set of words.
- Your progress and accuracy are shown in real time.

## Project Structure

- `src/components/TypingArea.vue` — Main typing interface
- `src/components/Header.vue` — Sticky header
- `src/views/HomeView.vue` — Main view
- `src/App.vue` — App layout

## License

MIT
