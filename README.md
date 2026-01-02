# FrontendLocalizationWebSite-pltSDK
## 🌐 Website Localization (Frontend)
A simple, hash-based localization system for static websites using vanilla JavaScript. It uses the URL hash (#en, #ru) to switch the language and reload the page to apply translations.

## 🚀 How It Works
1. `core.js` is the engine:

   1.1. Listens for language selection in the `<select>` element.
   
   1.2. On change, adds a hash (e.g., `index.html#ru`) to the URL and reloads the page.

   1.3. On page load, reads the hash from the URL and applies the corresponding translation to all elements on the page.
2. `lang.js` is an example page with connected scripts and marked-up text for translation.

## ⚙️ How to Use

### 1. Connecting Scripts in HTML
Ensure the scripts are included in the correct order at the end of the `<body>`:
```html
<script src="lang.js"></script>
<script src="core.js"></script>
```
### 2. Adding Translatable Elements to the Page
For any text that should be translated:
1. Add a CSS class to the element with the prefix `plt-` followed by a unique key.
2. This key must match the key in the `langArr` object within the `lang.js` file.

#### Example:
```html
<!-- Element with the key "helloWorld" -->
<h1 class="plt-helloWorld">Hello World!</h1>

<!-- Element with the key "button" -->
<button class="plt-button">Click</button>
```
### 3. Adding and Editing Translations in `lang.js`
Add new keys or edit existing ones in the langArr object.
Format: `"key": { "en": "English text", "ru": "Russian text" }`.

#### Example for the elements above:
```js
const langArr = {
    "title": {
        "en": "My Site",
        "ru": "Мой сайт"
    },
    "helloWorld": { // Key matches plt-helloWorld
        "en": "Hello World!",
        "ru": "Привет, мир!"
    },
    "button": { // Key matches plt-button
        "en": "Click",
        "ru": "Нажми"
    }
}
```
### 4. Adding a Language Selector
Place this `<select>` element where needed on the page (e.g., in the header). The `core.js` script will automatically connect to it via `id="select"`.
```html
<select id="select">
    <option value="en">EN</option>
    <option value="ru">RU</option>
</select>
```
## 🔧 Important Details
1. The selected language is saved in the URL hash (e.g., #ru). Visiting such a link directly will automatically apply the language.
2. If the hash is missing or contains a non-existent language code, the system will automatically redirect to the default language (`#en`).
3. All keys in `langArr` and CSS classes (`plt-key`) must be unique and match each other.
