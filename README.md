# 💱 Currency Converter

A clean, responsive currency converter built with **React 19**, **Vite** and **Tailwind CSS v4**. Choose a source and target currency, enter an amount, and get the converted value using live exchange rates fetched from a free currency API.

---

## ✨ Features

- 🔄 Convert between all currencies supported by the exchange-rate API
- 🧮 Default pair of **USD → INR**, changeable from either dropdown
- ↔️ **Swap** button that flips the currencies *and* the amounts in one click
- ⌨️ Press **Enter** or click the **Convert** button to calculate (the form submits on either)
- 🔒 The "To" amount field is read-only, so the result can't be typed over
- ⚡ Exchange rates are fetched through a **custom React hook** (`useCurrencyInfo`)
- 🧩 A reusable **`InputBox`** component powers both the "From" and "To" fields
- 🌫️ Glassmorphism-style card (blur + translucent background) over a full-screen background image
- 📱 Responsive layout built entirely with Tailwind utility classes

---

## 🛠️ Tech Stack

| Category        | Tool                                                          |
| --------------- | ------------------------------------------------------------- |
| UI library      | [React 19](https://react.dev/)                                |
| Build tool      | [Vite](https://vitejs.dev/) with `@vitejs/plugin-react`       |
| Styling         | [Tailwind CSS v4](https://tailwindcss.com/) via `@tailwindcss/vite` |
| Language        | JavaScript (ES modules) / JSX                                 |
| Linting         | ESLint with `react-hooks` and `react-refresh` plugins         |
| Data source     | [fawazahmed0 Currency API](https://github.com/fawazahmed0/exchange-api) (free, served via jsDelivr CDN) |
| Package manager | npm                                                           |

---

## 🧠 Concepts Practised

- Building a **custom hook** (`useCurrencyInfo`) that wraps `useEffect` + `useState` for data fetching
- Managing form state with `useState` (amount, from, to, converted amount)
- Re-fetching data whenever the selected currency changes (dependency array in `useEffect`)
- Creating **reusable, prop-driven components** with sensible defaults
- Using `useId` to link `<label>` and `<input>` for accessibility
- Handling form submission with `onSubmit` and `preventDefault`
- Barrel exports (`components/index.js`) for cleaner imports
- Styling with Tailwind CSS v4 (`@import "tailwindcss"`) and Vite plugin setup

---

## 📁 Project Structure

```
currency-converter/
├── public/
├── src/
│   ├── components/
│   │   ├── InputBox.jsx          # Reusable amount input + currency dropdown
│   │   └── index.js              # Barrel file exporting InputBox
│   ├── hooks/
│   │   └── useCurrencyInfo.js    # Custom hook that fetches exchange rates
│   ├── App.jsx                   # Main UI, state and conversion logic
│   ├── App.css                   # Tailwind import
│   ├── index.css                 # Tailwind import (global styles)
│   └── main.jsx                  # App entry point
├── index.html
├── package.json
├── vite.config.js
└── .gitignore
```

---

## ⚙️ How It Works

1. **State:** `App.jsx` holds `amount`, `from` (default `usd`), `to` (default `inr`) and `convertedAmount`.
2. **Fetching rates:** `useCurrencyInfo(from)` calls the currency API for the selected "from" currency and returns an object of rates, e.g. `{ inr: 83.1, eur: 0.92, ... }`.
3. **Dropdown options:** the currency list is built from `Object.keys(currencyInfo)` and passed to both `InputBox` components.
4. **Converting:** on submit, `convertedAmount = amount × currencyInfo[to]`.
5. **Swapping:** the `swap` function exchanges `from` ↔ `to` and `amount` ↔ `convertedAmount`.

```js
// src/hooks/useCurrencyInfo.js
fetch(`https://cdn.jsdelivr.net/npm/@fawazahmed0/currency-api@latest/v1/currencies/${currency}.json`)
  .then((res) => res.json())
  .then((res) => setData(res[currency]))
```

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (a recent LTS version, v20.19+ or v22.12+, is recommended for current Vite releases)
- npm (comes with Node.js)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/Sayan161005/Currency-Converter.git

# 2. Move into the project folder
cd Currency-Converter

# 3. Install dependencies
npm install

# 4. Start the development server
npm run dev
```

Open the local URL shown in the terminal (usually `http://localhost:5173`) in your browser.

### Available Scripts

| Command           | Description                          |
| ----------------- | ------------------------------------ |
| `npm run dev`     | Start the development server         |
| `npm run build`   | Create an optimised production build |
| `npm run preview` | Preview the production build locally |
| `npm run lint`    | Run ESLint on the project            |

---

## 🌐 API

Exchange rates come from the free, open-source **fawazahmed0 Currency API**, delivered through the jsDelivr CDN. **No API key is required.**

```
GET https://cdn.jsdelivr.net/npm/@fawazahmed0/currency-api@latest/v1/currencies/{currency}.json
```

The response contains the rates of every supported currency relative to the one requested (for example `usd`), which is why the app re-fetches whenever the "From" currency changes.

---

## 🔮 Future Improvements

- [ ] Add loading and error states for failed or slow network requests
- [ ] Show full currency names and flags next to the currency codes
- [ ] Convert automatically as the user types (no button click needed)
- [ ] Round the converted result to a fixed number of decimal places
- [ ] Add a dark mode toggle
- [ ] Remember the last selected currencies with `localStorage`
- [ ] Show a historical rate chart

---

## 🤝 Contributing

Suggestions and improvements are welcome!

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m "Add your feature"`
4. Push the branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 👤 Author

**SAYAN SAHA**

- GitHub: [@Sayan161005](https://github.com/Sayan161005)

⭐ If you found this project helpful, consider giving it a star!
