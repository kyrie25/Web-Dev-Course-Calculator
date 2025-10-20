# Windows 11 Calculator Clone

A modern web-based calculator that replicates the Basic Mode functionality of the Windows 11 Calculator app, built with Vue 3, Vite, and TailwindCSS.

## Features

### ✨ Core Functionality

- **Standard Arithmetic Operations**: Addition (+), Subtraction (-), Multiplication (×), Division (÷)
- **Advanced Operations**:
  - Square (x²)
  - Square Root (²√)
  - Reciprocal (1/x)
  - Percentage (%)
  - Sign Toggle (±)

### 🧠 Memory Functions

- **MC**: Memory Clear
- **MR**: Memory Recall
- **M+**: Memory Add
- **M-**: Memory Subtract
- **MS**: Memory Store

### 🎨 Interface Features

- **Windows 11 Fluent Design**: Authentic glassmorphism effects and styling
- **Light/Dark Mode Toggle**: Seamless theme switching with Windows 11 color schemes
- **Responsive Design**: Optimized for various screen sizes
- **Error Handling**: Proper handling of division by zero and invalid operations

### ⌨️ Input Methods

- **Clear Functions**:
  - C (Clear All)
  - CE (Clear Entry)
  - ⌫ (Backspace)
- **Decimal Point Support**
- **Keyboard Support**

## Technologies Used

- **Vue 3** - Progressive JavaScript framework with Composition API
- **Vite** - Next-generation frontend tooling
- **TailwindCSS v4** - Utility-first CSS framework
- **PostCSS** - CSS transformations
- **Yarn** - Package manager

## Getting Started

### Prerequisites

- Node.js (v16 or higher)
- Yarn package manager

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/kyrie25/Web-Dev-Course-Calculator.git
   cd Web-Dev-Course-Calculator
   ```

2. **Install dependencies**

   ```bash
   yarn install
   ```

3. **Start development server**

   ```bash
   yarn dev
   ```

4. **Open browser**
   Navigate to `http://localhost:5173/`

### Build for Production

```bash
# Build the project
yarn build

# Preview production build
yarn preview
```

## Usage

### Basic Operations

1. Click number buttons to input values
2. Click operation buttons (+, -, ×, ÷) to perform calculations
3. Click = to see the result
4. Use C to clear all or CE to clear current entry
5. Use ⌫ to delete the last digit

### Advanced Functions

- **Percentage**: Enter a number and click %
- **Square**: Enter a number and click x²
- **Square Root**: Enter a number and click ²√
- **Reciprocal**: Enter a number and click 1/x
- **Sign Toggle**: Click ± to change number sign

### Memory Operations

1. **Store**: Enter a number and click MS to store in memory
2. **Recall**: Click MR to recall stored value
3. **Add**: Enter a number and click M+ to add to memory
4. **Subtract**: Enter a number and click M- to subtract from memory
5. **Clear**: Click MC to clear memory

### Theme Toggle

Click the 🌙/☀️ button in the top right to switch between light and dark modes.

## Project Structure

```
src/
├── components/
│   ├── Calculator.vue    # Main calculator logic and state
│   ├── Display.vue       # Calculator display component
│   └── Keypad.vue       # Button layout and input handling
├── App.vue              # Root component
├── main.js              # Application entry point
└── style.css            # Global styles and theme definitions
```

## Technical Details

### Component Architecture

- **Calculator.vue**: Manages all calculator state, operations, and business logic
- **Display.vue**: Renders current value and calculation history
- **Keypad.vue**: Handles button layout and user input events

### Styling Approach

- Pure CSS with TailwindCSS utilities for rapid development
- CSS custom properties for theme variables
- Glassmorphism effects using backdrop-filter and rgba colors
- Responsive design with CSS Grid and Flexbox

### State Management

- Vue 3 Composition API with reactive refs
- Local component state for calculator operations
- Memory storage using JavaScript variables
- Theme state with localStorage persistence (planned)

## Browser Support

- Chrome/Edge 88+
- Firefox 87+
- Safari 14+

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is open source and available under the [MIT License](LICENSE).

## Acknowledgments

- Design inspiration from Windows 11 Calculator
- Vue.js team for the excellent framework
- TailwindCSS team for the utility-first approach
