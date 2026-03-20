# 🔍 HTML File Type Identifier

A lightweight, browser-based tool that detects and identifies file types by analyzing HTML file inputs — using magic bytes, MIME types, and file signatures rather than relying solely on file extensions.

---

## 📌 Overview

The **HTML File Type Identifier** is a client-side web utility that allows users to drag and drop (or select) any file and instantly receive detailed information about its true file type. It reads the file's binary signature (magic bytes) to accurately identify the format — even if the file extension has been changed or removed.

---

## ✨ Features

- 🧠 **Magic Byte Detection** — Reads raw binary headers to identify file formats
- 🏷️ **MIME Type Display** — Shows the browser-reported MIME type alongside the detected type
- 📂 **Extension Validation** — Flags mismatches between file extension and actual format
- 🖱️ **Drag & Drop Interface** — Simple, intuitive file input with drag-and-drop support
- ⚡ **100% Client-Side** — No file is ever uploaded to a server; all processing happens in the browser
- 🔒 **Privacy-Safe** — Files never leave the user's machine
- 📋 **Copy Results** — One-click copy of identification results
- 🌐 **Zero Dependencies** — Pure HTML, CSS, and vanilla JavaScript

---

## 🚀 Getting Started

### Prerequisites

No installation required. Just a modern web browser:

- Chrome 80+
- Firefox 75+
- Safari 13.1+
- Edge 80+

### Usage

1. **Clone or download** the repository:
   ```bash
   git clone https://github.com/your-username/html-file-type-identifier.git
   cd html-file-type-identifier
   ```

2. **Open** `index.html` in your browser:
   ```bash
   open index.html
   # or simply double-click the file
   ```

3. **Drop a file** onto the drop zone, or click **Browse** to select one.

4. View the **identification results** instantly — file type, MIME type, magic bytes, and extension match status.

---

## 🗂️ Project Structure

```
html-file-type-identifier/
├── index.html          # Main application entry point
├── css/
│   └── styles.css      # Styling and layout
├── js/
│   ├── identifier.js   # Core file type detection logic
│   ├── signatures.js   # Magic byte signature database
│   └── ui.js           # DOM interaction and display logic
├── README.md           # Project documentation
└── LICENSE             # License file
```

---

## 🧪 How It Works

### Magic Byte Detection

Every file format has a unique binary "signature" — a sequence of bytes at the start (or sometimes end) of the file. For example:

| File Type | Magic Bytes (Hex)         | ASCII      |
|-----------|---------------------------|------------|
| PNG       | `89 50 4E 47 0D 0A 1A 0A` | `‰PNG....` |
| JPEG      | `FF D8 FF`                | `ÿØÿ`      |
| PDF       | `25 50 44 46`             | `%PDF`      |
| ZIP       | `50 4B 03 04`             | `PK..`     |
| GIF       | `47 49 46 38`             | `GIF8`     |
| MP3       | `49 44 33`                | `ID3`      |

The identifier reads the first **N bytes** of the file using the [`FileReader`](https://developer.mozilla.org/en-US/docs/Web/API/FileReader) API and compares them against a built-in signature database.

### Detection Flow

```
User Drops File
      │
      ▼
Read File Header (first 512 bytes via FileReader API)
      │
      ▼
Compare against Signature Database
      │
      ├── Match Found → Return detected type + confidence
      │
      └── No Match → Fall back to MIME type / extension hint
      │
      ▼
Display Results (type, MIME, extension, confidence score)
```

---

## 📦 Supported File Types

The identifier currently recognizes **50+ file formats** across the following categories:

| Category       | Formats                                                         |
|----------------|-----------------------------------------------------------------|
| **Images**     | JPEG, PNG, GIF, WebP, BMP, TIFF, ICO, SVG, AVIF, HEIC         |
| **Documents**  | PDF, DOCX, XLSX, PPTX, ODT, RTF                                |
| **Archives**   | ZIP, RAR, 7Z, TAR, GZ, BZ2, XZ                                 |
| **Audio**      | MP3, WAV, FLAC, OGG, AAC, M4A                                  |
| **Video**      | MP4, MKV, AVI, MOV, WebM, FLV                                  |
| **Code/Text**  | HTML, XML, JSON, CSV (heuristic-based)                         |
| **Executables**| EXE, ELF, Mach-O, DLL                                          |
| **Fonts**      | TTF, OTF, WOFF, WOFF2                                          |

> Want to add support for a new format? See [Contributing](#-contributing).

---

## 🔧 Configuration

You can extend the signature database in `js/signatures.js`:

```javascript
{
  type: "FLAC",
  mimeType: "audio/flac",
  extension: ["flac"],
  signature: [0x66, 0x4C, 0x61, 0x43],  // "fLaC"
  offset: 0,
  description: "Free Lossless Audio Codec"
}
```

Each signature entry supports:

| Field         | Type       | Description                                   |
|---------------|------------|-----------------------------------------------|
| `type`        | `string`   | Human-readable file type name                 |
| `mimeType`    | `string`   | Standard MIME type                            |
| `extension`   | `string[]` | Common file extensions                        |
| `signature`   | `number[]` | Array of byte values (magic bytes)            |
| `offset`      | `number`   | Byte offset where signature begins (default 0)|
| `description` | `string`   | Optional description                          |

---

## 🛡️ Privacy & Security

- **No data leaves the browser.** The file is read locally using the Web File API.
- **No network requests are made** during file identification.
- **No cookies or local storage** are used.
- The tool is safe to use with sensitive or confidential files.

---

## 🤝 Contributing

Contributions are welcome! To add support for a new file type or fix a detection issue:

1. Fork the repository
2. Create a feature branch: `git checkout -b feat/add-xyz-support`
3. Add the signature to `js/signatures.js`
4. Test with real sample files
5. Submit a pull request with a brief description

Please follow the existing code style and include sample files in your PR when adding new signatures.

---

## 🐛 Known Limitations

- **Text-based formats** (HTML, JSON, CSV, XML) cannot be identified by magic bytes alone and rely on heuristic content scanning, which may be less reliable.
- **Encrypted files** (e.g., password-protected ZIP or PDF) may be identified by their outer container format only.
- **Very small files** (< 8 bytes) may not have enough data for reliable detection.
- **Exotic or proprietary formats** not in the signature database will fall back to MIME type or extension.

---

## 📄 License

This project is licensed under the **MIT License**. See [`LICENSE`](./LICENSE) for details.

---

## 🙏 Acknowledgements

- Inspired by the [Gary Kessler File Signatures Table](https://www.garykessler.net/library/file_sigs.html)
- Magic byte data sourced from [Wikipedia's List of file signatures](https://en.wikipedia.org/wiki/List_of_file_signatures)
- Built with vanilla web technologies — no frameworks required

---

*Made with ❤️ for developers, security researchers, and curious minds.*
