# VS Code Extensions for Capturing Evaluation Results

**You're right - there used to be VS Code extensions for this!**

---

## 📸 Screenshot/Paste Extensions

### 1. **Paste Image** (Most Popular)
- **Extension ID**: `mushan.vscode-paste-image`
- **What it does**: Paste screenshots directly into markdown files
- **How to use**:
  1. Take screenshot (Win+Shift+S / Cmd+Shift+4)
  2. In VS Code markdown file, press `Ctrl+Alt+V` (or Cmd+Option+V)
  3. Image automatically saved and embedded!
- **Perfect for**: Capturing evaluation results and embedding in `evals/results/` markdown files

### 2. **Markdown Image** 
- **Extension ID**: `bierner.markdown-image`
- **What it does**: Similar to Paste Image, embeds screenshots in markdown
- **Features**: Auto-saves images, generates markdown links

### 3. **Markdown Paste**
- **Extension ID**: `telesoho.vscode-markdown-paste-image`
- **What it does**: Paste images into markdown with auto-naming
- **Features**: Can auto-name based on date/time

---

## 🎯 Recommended Setup for Evaluation Results

### Best Option: **Paste Image** Extension

**Install:**
```bash
code --install-extension mushan.vscode-paste-image
```

**Or in VS Code:**
1. Open Extensions (Ctrl+Shift+X)
2. Search "Paste Image"
3. Install `mushan.vscode-paste-image`

**Configure for `evals/results/` folder:**
Add to VS Code settings (`.vscode/settings.json`):
```json
{
  "pasteImage.path": "${projectRoot}/evals/results/screenshots",
  "pasteImage.basePath": "${projectRoot}",
  "pasteImage.prefix": "/evals/results/screenshots/"
}
```

**Workflow:**
1. Get evaluation results (e.g., 0.1 percentile from Vertex AI)
2. Take screenshot (Win+Shift+S)
3. Open `evals/results/YYYY-MM-DD-VertexAI-Results.md`
4. Press `Ctrl+Alt+V` → Image auto-saved and embedded!
5. Fill in scores from screenshot

---

## 🔧 Other Useful VS Code Extensions

### 4. **Markdown All in One**
- **Extension ID**: `yzhang.markdown-all-in-one`
- **What it does**: Enhanced markdown editing
- **Useful for**: Writing evaluation result summaries

### 5. **Markdown Preview Enhanced**
- **Extension ID**: `shd101wyy.markdown-preview-enhanced`
- **What it does**: Better markdown preview with image support
- **Useful for**: Viewing evaluation results with screenshots

### 6. **File Utils**
- **Extension ID**: `sleistner.vscode-fileutils`
- **What it does**: File operations from command palette
- **Useful for**: Quick file creation in `evals/results/`

---

## 💡 Quick Workflow with Paste Image

**When you get evaluation results:**

1. **Take screenshot** (Win+Shift+S / Cmd+Shift+4)
2. **Open VS Code** → `evals/results/` folder
3. **Create new file**: `YYYY-MM-DD-[Platform]-[Model]-Results.md`
4. **Paste screenshot**: `Ctrl+Alt+V` (or Cmd+Option+V)
5. **Fill template** with scores while screenshot is visible
6. **Done!** - Screenshot saved + documented

**Never lose validation stamps again!**

---

## 🚀 Setup Instructions

### Install Paste Image:
```bash
# In VS Code terminal or command line
code --install-extension mushan.vscode-paste-image
```

### Configure for evals folder:
Create `.vscode/settings.json` in project root:
```json
{
  "pasteImage.path": "${projectRoot}/evals/results/screenshots",
  "pasteImage.basePath": "${projectRoot}",
  "pasteImage.prefix": "/evals/results/screenshots/",
  "pasteImage.insertPattern": "![${imageFileName}](${imageFilePath})"
}
```

### Test it:
1. Take any screenshot
2. Open a markdown file in `evals/results/`
3. Press `Ctrl+Alt+V`
4. Image should appear and be saved!

---

**This is probably the extension you remember!** `Paste Image` is the most popular one for embedding screenshots in markdown files.

