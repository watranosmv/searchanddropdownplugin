# PDWS Language Aware Redirect

A lightweight JavaScript enhancement for WordPress **Page Dropdown / Printer Dropdown–style plugins** that ensures users are redirected to the **correct language-prefixed URL** when multilingual plugins like **GTranslate** are active.

This script preserves the current language context (e.g. `/fr`, `/de`, `/zh-cn`) when a user selects an option from a dropdown and is redirected to another page.

---

## 🚀 Features

* Automatically detects language prefixes from the current URL
* Supports:

  * 2–3 letter language codes (`/fr`, `/de`, `/urd`)
  * Hyphenated codes (`/zh-cn`, `/pt-br`)
* Preserves language prefix during redirects
* Prevents redirects to wrong/default language
* Works seamlessly with **GTranslate** and similar URL-based language plugins
* Falls back to `/register?model=MODEL_NAME` if a dropdown option has no mapped URL
* Lightweight, dependency-free (uses jQuery already present in WordPress)

---

## 📦 Files Included

```
/pdws-language-aware-redirect.js   # Core language-aware redirect logic
/index.php                        # WordPress plugin loader (if bundled as a plugin)
```

---

## 🧠 How It Works

1. Detects the current language prefix from the browser URL
2. Listens for changes on the dropdown with ID:

   ```
   #pdws-page-dropdown
   ```
3. When a user selects an option:

   * Finds the mapped URL
   * Injects the detected language prefix if missing
   * Redirects the user to the correct translated page

If no URL exists for the selected option, the user is redirected to:

```
/register?model=Selected+Model+Name
```

(with the language prefix preserved)

---

## 🛠️ Usage

### 1️⃣ Include the Script

Enqueue or include the JavaScript file in your plugin or theme:

```php
wp_enqueue_script(
    'pdws-language-aware-redirect',
    plugin_dir_url(__FILE__) . 'pdws-language-aware-redirect.js',
    array('jquery'),
    '1.0.0',
    true
);
```

---

### 2️⃣ HTML Requirements

Your dropdown **must** use the following ID:

```html
<select id="pdws-page-dropdown">
    <option value="">Select a model</option>
    <option value="model1">Any Model 1</option>
</select>
```

Optional redirect message:

```html
<div id="redirect-message" style="display:none;">Redirecting…</div>
```

---

### 3️⃣ Initialize the Redirect Logic

After Select2 (or normal dropdown) initialization, call:

```js
pdwsEnableLanguageAwareRedirect(modelLinks);
```

Where `modelLinks` is an object mapping dropdown values to URLs:

```js
var modelLinks = {
    "model1": "/example-link",
    "model2": "/example-link-2"
};
```

---

## 🌍 Supported URL Structures

✅ Supported:

```
/fr/page-name
/de/page-name
/zh-cn/page-name
```

❌ Ignored prefixes (not treated as languages):

```
/wp-admin
/wp-content
/wp-json
/admin
/register
/login
/search
```

---

## 🔐 Compatibility

* WordPress: ✅
* GTranslate: ✅
* Polylang (URL mode): ✅
* WPML (URL mode): ✅
* Select2 dropdowns: ✅

---

## 🧩 Use Cases

* Printer model dropdowns
* Multilingual product selectors
* Knowledge base language-aware navigation
* SEO-safe redirects without breaking translations

---

## ✍️ Author

**Akmal Yousuf**

---

## 📄 License

MIT License

You are free to use, modify, and distribute this script in personal or commercial projects.

---

## ⭐ Contributing

Pull requests and improvements are welcome. If you use this in a production site, consider starring the repository to support the project.

---

## 📬 Support

If you encounter issues with specific language plugins or URL structures, feel free to open an issue on GitHub.

---

**Language-aware redirects done right.**

Currently live at [ij.start.canon](https://ij.start-canon.com)
