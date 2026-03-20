# 🔍 File Type Identifier
### Security Utility v1.0 — Magic Number · Extension · Validation

A browser-based security tool that detects the **true type** of any file by reading its **magic bytes** (raw binary signature), rather than trusting the file extension alone. Upload any file — it instantly tells you whether the extension matches the actual format.

> **Detects:** PNG · JPG · EXE/PE · PDF · GIF · ZIP · and more

---

## 🚀 How It Works

Every file format has a unique binary signature in its first few bytes — called **magic bytes**. For example, every real JPEG starts with `FF D8`. This tool reads those bytes directly and compares them against the claimed extension.

| Result | Meaning |
|--------|---------|
| ✅ SAFE — MATCH | Extension matches the detected magic bytes |
| ⚠️ UNKNOWN | No recognized magic bytes — file may be renamed or plain text |
| ❌ MISMATCH | Extension doesn't match the actual file format |

---

## 📸 Demo

### Scenario 1 — Normal File (SAFE — MATCH)

A genuine JPEG image is uploaded. The tool reads the magic bytes `FF D8` and confirms the `.jpeg` extension is legitimate.

**Step 1: Upload interface**

![Upload interface](assets/01_upload_interface.png)

**Step 2: Select a file**

![File selection](assets/02_file_selection.png)

**Step 3: Result — SAFE — MATCH**

The extension `.jpeg` matches the detected type `JPG`. Magic bytes confirm the file is exactly what it claims to be.

![Safe match result](assets/03_safe_match.png)

---

### Scenario 2 — Renamed File (UNKNOWN)

A file is renamed from `A.txt` → `A.png` → `A.jpg` using the `ren` command in CMD. The extension changes, but the internal binary content stays the same. The tool catches it.

**Step 1: Rename via Command Prompt**

```cmd
C:\Users\Navee\Documents> ren "A.png" "A.jpg"
```

![CMD rename](assets/04_cmd_rename.png)

**Step 2: File properties & upload**

The file shows as `JPG File` in Windows Explorer, with a size of 0 bytes — no real image data inside.

![File properties and upload](assets/05_file_properties_upload.png)

**Step 3: Result — UNKNOWN**

No recognized magic bytes found. Extension `.jpg` cannot be verified — the tool flags it as `Unknown / Plain Text`.

![Unknown result](assets/06_unknown_result.png)

---

## 💡 Key Takeaway

> Renaming a file's extension **never** changes its actual binary content.  
> A file is what its bytes say it is — not what its name says.

---

## 🛠️ Usage

1. Open `file_type_identifier.html` in any browser
2. Drop a file onto the upload zone or click to browse
3. The tool instantly reads the first 16 bytes and displays the result

No server required — runs entirely in the browser.

---

## 📁 Repo Structure

```
file-type-identifier/
├── file_type_identifier.html   # Main app (single file, no dependencies)
├── assets/                     # Screenshots for README
│   ├── 01_upload_interface.png
│   ├── 02_file_selection.png
│   ├── 03_safe_match.png
│   ├── 04_cmd_rename.png
│   ├── 05_file_properties_upload.png
│   └── 06_unknown_result.png
└── README.md
```
