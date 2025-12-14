# **Gmail Rich Text Formatter**

A lightweight, browser-based tool designed to sanitize and format rich text specifically for Gmail's compose window.

Gmail's visual editor has legacy idiosyncrasies—it prefers `<div>` tags over `<p>` tags for line breaks, uses `<font>` tags for styling instead of CSS spans, and often breaks formatting when pasting content from modern web apps (like Notion, Google Docs, or ChatGPT). This tool acts as a bridge to ensure your pasted emails look professional and consistent.

## **Features**

* **Paragraph Correction:** Automatically converts `<p>` tags (which cause double spacing in Gmail) into `<div>` tags.  
* **Heading Mapping:** Intelligently maps `<h1>` and `<h2>` tags to Gmail's "Huge" and "Large" size attributes, without forcing bold styling.  
* **List Flattening:** Removes complex nesting inside bullet points (`<ul>`/`<ol>`) to ensure lists render cleanly.  
* **Legacy Tag Support:** Converts modern CSS styles (like `font-size`, `text-decoration: underline`) into legacy HTML tags (`<font size="...">`, `<u>`) that Gmail respects.  
* **Attribute Stripping:** Removes `class`, `id`, `data-testid`, and `dir="ltr"` attributes to prevent clutter.  
* **Smart Cleaning:** Aggressively strips `<span>` tags while preserving essential formatting like **Bold** and *Italic* nested inside them.

## **How to Use**

1. **Open:** Open `index.html` in any web browser.  
2. **Paste:** Paste your rich text content (from Word, a website, or an LLM) into the editor.  
3. **Format:** Click the **Clean & Format** button. The text will shift slightly as it is restructured.  
4. **Copy:** Click **Copy for Gmail**.  
5. **Paste:** Go to Gmail and paste (`Ctrl+V` / `Cmd+V`) into your email body.

## **Technical Transformations**

The tool performs the following DOM manipulations using JavaScript:

| Source Element | Transformed To | Reason |
| :---- | :---- | :---- |
| `<p>Text</p>` | `<div>Text</div>` | Prevents unremovable double-spacing in Gmail. |
| `<h1>Heading</h1>` | `<div><font size="6">Heading</font></div>` | Gmail does not use semantic H1 tags; it uses text size "Huge". |
| `<h2>Heading</h2>` | `<div><font size="4">Heading</font></div>` | Maps to Gmail's text size "Large". |
| `<li><p>Item</p></li>` | `<li>Item</li>` | Flattens lists to prevent bullets from misaligning. |
| `<span style="font-weight:bold">` | `<b>...</b>` | Ensures bold text is preserved even when spans are stripped. |
| `text-decoration: underline` | `<u>...</u>` | Gmail prefers legacy tags over CSS text-decoration. |
| `<span>` | *Stripped* | Removes wrapper noise while keeping inner text/formatting. |

## **Installation**

This is a single-file application. No server, Node.js, or build process is required.

1. Download the `index.html` file.  
2. Double-click it to run it locally in your browser.

