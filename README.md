# Logic Gate Synthesizer v3.0

A web-based tool to convert truth tables into optimized logic circuits using Boolean algebra and advanced optimization techniques.

## ✨ Features

### 🎨 User Interface
- **Dark Mode Toggle** - 🌙 button in header (Ctrl+D)
- **Tabbed Interface** - 5 organized tabs for different workflows
- **Mobile Responsive** - Works on phones, tablets, and desktops
- **Keyboard Shortcuts** - Professional keyboard support
- **Real-time Updates** - Instant feedback on all interactions

### 🔧 Core Functionality
- **Truth Table Input** - Click cells to cycle through values (0 → 1 → X)
- **Don't Care (X) Values** - Support for undefined output states
- **Extended Variables** - Support 2-6 variables (was 2-4)
- **Boolean Expression Input** - Enter expressions directly
- **Quick Fill Buttons** - All 0s, All 1s, All X for fast input

### 🧠 Optimization
- **Quine-McCluskey Algorithm** - Boolean expression minimization
- **Don't Care Optimization** - Leverages X values for better reduction
- **Dual Circuit Generation** - Shows both naive and optimized versions
- **Metrics Comparison** - Gate count, cost, and delay analysis
- **Step-by-Step Minimization** - Learn the optimization process

### 📊 Visualization
- **Karnaugh Map (K-Map)** - Visual representation of truth table
- **Interactive Circuits** - Draggable nodes showing logic gates
- **Signal Visualization** - Color-coded nodes (red=0, green=1)
- **Real-time Simulation** - Toggle inputs and see output changes

### 💾 Export Options
- **CSV Export** - Metrics in spreadsheet format
- **JSON Export** - Complete design data
- **Clipboard Copy** - Copy all data with one click
- **Screenshot Guide** - Instructions for saving circuit images

---

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- Python 3.7+
- Git

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/Aayu2810/logic-gate-synthesizer.git
cd logic-gate-synthesizer
```

2. **Install Frontend Dependencies**
```bash
cd frontend
npm install
```

3. **Install Backend Dependencies**
```bash
cd backend
pip install flask flask-cors sympy
```

### Running the Application

1. **Start Backend Server** (Terminal 1)
```bash
cd backend
python app.py
```
Backend will run on: `http://127.0.0.1:5000`

2. **Start Frontend Server** (Terminal 2)
```bash
cd frontend
npm start
```
Frontend will open at: `http://localhost:3000`

---

## 📖 Usage Guide

### Basic Workflow

1. **Input Tab** (📊)
   - Select number of variables (2-6)
   - Choose input mode:
     - **Truth Table**: Click cells to set output values
     - **Expression**: Enter Boolean expression (e.g., `(A & B) | (~C)`)
   - Use quick fill buttons: All 0s, All 1s, All X
   - Click **⚡ Synthesize Circuit**

2. **K-Map Tab** (🗺️)
   - Visual representation of truth table
   - Helps understand minimization groups
   - Shows X value handling

3. **Analysis Tab** (📈)
   - **Boolean Expressions**: Original and optimized forms
   - **Metrics Table**:
     - Gate Count (Naive vs Optimized)
     - Hardware Cost
     - Circuit Delay (ns)
     - Gates Saved
   - **Minimization Steps**: Algorithm explanation

4. **Circuit Tab** (🔌)
   - **Simulation Controls**: Toggle inputs (A, B, C, etc.)
   - **Naive Circuit**: Non-optimized implementation
   - **Optimized Circuit**: Best-case implementation
   - Nodes show current signal values

5. **Export Tab** (💾)
   - **Copy All Data**: Copy expressions and metrics
   - **Download CSV**: Metrics for spreadsheet analysis
   - **Download JSON**: Complete design data
   - **Screenshot Help**: Instructions for saving images

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| Ctrl+D | Toggle Dark Mode |
| Ctrl+Z | Undo |
| Ctrl+Y | Redo |

### Truth Table Values

- **0** - Output is 0 (false)
- **1** - Output is 1 (true)  
- **X** - Don't care (undefined, optimizable)

Click cells to cycle through values.

---

## 🏗️ Project Structure

```
logic-gate-synthesizer/
├── frontend/
│   ├── src/
│   │   ├── App.js              # Main React component
│   │   ├── App.css             # Styling (light & dark modes)
│   │   ├── CircuitDiagram.js   # Circuit visualization
│   │   ├── KMap.js             # Karnaugh map display
│   │   └── index.js            # Entry point
│   ├── public/
│   ├── package.json
│   └── node_modules/
├── backend/
│   ├── app.py                  # Flask server
│   ├── parser/
│   │   └── truth_table_parser.py
│   ├── simulator/
│   │   └── logic_simulator.py
│   ├── optimizer/
│   │   └── cost_function.py
│   ├── simplifier/
│   │   ├── boolean_laws.py
│   │   ├── quine_mccluskey.py
│   │   └── implicant_to_expression.py
│   └── visualization/
│       └── circuit_generator.py
└── README.md
```

---

## 🔌 API Endpoints

### POST `/generate`
Generate optimized circuit from truth table.

**Request:**
```json
{
  "variables": ["A", "B", "C"],
  "table": [0, 1, "X", 1, 0, 1, 1, 0]
}
```

**Response:**
```json
{
  "original_sop": "A'B'C' + A'BC + AB'C + ABC",
  "simplified": "AB + AC + BC",
  "naive_circuit": {...},
  "optimized_circuit": {...},
  "analytics": {
    "naive": {"gate_count": 5, "cost": 12, "total_delay_ns": 8.5},
    "optimized": {"gate_count": 3, "cost": 7, "total_delay_ns": 5.2},
    "saved_gates": 2
  },
  "step_by_step": [...]
}
```

### POST `/reverse`
Convert Boolean expression to truth table.

**Request:**
```json
{
  "expression": "(A & B) | (~C)",
  "variables": ["A", "B", "C"]
}
```

**Response:**
```json
{
  "table": [1, 1, 0, 1, 0, 1, 0, 1],
  "variables": ["A", "B", "C"]
}
```

---

## 🎨 Customization

### Dark Mode
- Automatically saved to localStorage
- Uses CSS variables for easy theming
- Edit `App.css` to customize colors

### Adding More Variables
Modify in `App.js`:
```javascript
{[2, 3, 4, 5, 6, 7, 8].map(n => <option key={n} value={n}>{n}</option>)}
```

---

## 🐛 Troubleshooting

### "Backend not reachable" Error
```bash
# Make sure backend is running
cd backend
python app.py
# Should show: Running on http://127.0.0.1:5000
```

### Circuits Not Generating
1. Check browser console (F12)
2. Make sure truth table has at least one output = 1
3. Click "⚡ Synthesize Circuit" button
4. Wait 2-3 seconds for generation

### npm install fails
```bash
cd frontend
npm install --legacy-peer-deps
```

### Python dependencies missing
```bash
pip install flask flask-cors sympy
```

---

## 📊 Examples

### Example 1: 2-Variable AND Gate
- Set Variables: 2
- Fill Truth Table: [0, 0, 0, 1]
- Synthesize → Output: `A & B`

### Example 2: 3-Variable OR with Don't Care
- Set Variables: 3
- Fill Truth Table: [0, 1, X, 1, X, 1, 1, 1]
- Synthesize → Optimized with minimal gates

### Example 3: From Expression
- Mode: Expression
- Expression: `(A & B) | (C & D)`
- Generates truth table and circuit automatically

---

## 🚀 New Features in v3.0

✅ Dark mode with localStorage persistence  
✅ 5-tab tabbed interface  
✅ Don't Care (X) value support  
✅ Extended variable support (2-6)  
✅ Undo/Redo functionality  
✅ Keyboard shortcuts  
✅ Mobile responsive design  
✅ Multiple export formats  
✅ Interactive circuit visualization  
✅ Real-time simulation  

---

## 🔮 Planned Features

- [ ] Timing diagram visualization
- [ ] Critical path highlighting
- [ ] VHDL/Verilog export
- [ ] Espresso algorithm integration
- [ ] Test vector generation
- [ ] Circuit comparison mode
- [ ] PDF report generation
- [ ] 3D circuit viewer

---

## 📝 License

This project is licensed under the MIT License.

---

## 👥 Contributors

- **Original Author**: Friend's Project
- **v3.0 Enhancements**: Dark Mode, Tabbed UI, X Values Support, Export Features

---

## 📧 Support

For issues, bugs, or feature requests, please open an issue on GitHub.

---

## 🎓 Educational Resources

- [Boolean Algebra Basics](https://www.electronics-tutorials.ws/boolean/bool_1.html)
- [Karnaugh Maps Explained](https://www.electronics-tutorials.ws/boolean/bool_5.html)
- [Quine-McCluskey Algorithm](https://en.wikipedia.org/wiki/Quine–McCluskey_algorithm)
- [Digital Logic Design](https://www.electronics-tutorials.ws/logic/logic_1.html)

---

## 📈 Performance

| Component | Time |
|-----------|------|
| 2-4 variables | < 500ms |
| 5-6 variables | < 2000ms |
| Circuit rendering | < 1000ms |
| Export to CSV/JSON | < 500ms |

---

**Last Updated**: May 2026  
**Version**: 3.0  
**Status**: Stable ✅
