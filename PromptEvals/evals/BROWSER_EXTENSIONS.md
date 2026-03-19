# Browser Extensions for Auto-Capturing Evaluation Results

**You're right - there should be extensions for this!** Here are options:

---

## 🔧 Existing Extensions That Could Help

### 1. **Nimbus Screenshot** (Chrome/Edge)
- **What**: Auto-screenshot on page changes
- **URL**: https://chrome.google.com/webstore/detail/nimbus-screenshot
- **Features**: 
  - Auto-capture on URL patterns
  - Can detect when results appear
  - Auto-save to folder
- **Use case**: Set to auto-capture when visiting Vertex AI Studio results pages

### 2. **Awesome Screenshot** (Chrome/Edge)
- **What**: Screenshot tool with automation
- **URL**: https://chrome.google.com/webstore/detail/awesome-screenshot
- **Features**:
  - Scheduled screenshots
  - Auto-save
  - Can trigger on page elements

### 3. **Full Page Screen Capture** (Chrome)
- **What**: Auto-capture full pages
- **URL**: https://chrome.google.com/webstore/detail/full-page-screen-capture
- **Features**:
  - One-click full page capture
  - Auto-save options

### 4. **FireShot** (Chrome/Edge/Firefox)
- **What**: Advanced screenshot tool
- **URL**: https://chrome.google.com/webstore/detail/fireshot
- **Features**:
  - Auto-capture on page load
  - Can detect specific elements
  - Batch capture

---

## 🤖 Automation Extensions

### 5. **Auto Screenshot** (Chrome)
- **What**: Automatically captures screenshots
- **Features**:
  - Set URL patterns to auto-capture
  - Time-based captures
  - Auto-save to folder

### 6. **Page Monitor** (Chrome)
- **What**: Monitors pages for changes
- **URL**: https://chrome.google.com/webstore/detail/page-monitor
- **Use case**: Could trigger screenshot when results appear

---

## 💡 Custom Solution Ideas

### Option 1: Browser Extension with URL Detection
Create extension that:
- Detects when you're on evaluation results pages
- Auto-screenshots when results appear
- Saves to `evals/results/` folder
- Names files automatically

### Option 2: Raycast Extension
Since you use Raycast:
- Create Raycast extension that monitors clipboard
- When you copy results, auto-saves
- Could integrate with screenshot tools

### Option 3: Keyboard Shortcut Automation
- Use tools like **AutoHotkey** (Windows) or **Keyboard Maestro** (Mac)
- Set shortcut (e.g., Ctrl+Shift+S) to:
  - Take screenshot
  - Save to `evals/results/` with timestamp
  - Open template file

---

## 🎯 Recommended Setup

### Quick Win: Nimbus Screenshot
1. Install Nimbus Screenshot
2. Set up auto-capture for:
   - `console.cloud.google.com/vertex-ai/*`
   - `platform.openai.com/eval/*`
3. Auto-save to `evals/results/screenshots/`

### Better: Custom Extension
Create simple extension that:
- Detects evaluation result pages
- Auto-captures when results appear
- Extracts scores/text
- Saves screenshot + data to `evals/results/`

---

## 🚀 What We Should Build

**Custom Extension: "Eval Stamp Capturer"**

Features:
- ✅ Detects evaluation platforms (Vertex AI, OpenAI Evals, etc.)
- ✅ Auto-screenshots when results appear
- ✅ Extracts scores/text automatically
- ✅ Saves to `evals/results/` with proper naming
- ✅ Fills out RESULTS_TEMPLATE.md automatically
- ✅ Never lose validation stamps again!

**Would solve the problem completely!**

---

## 📝 For Now: Manual But Fast

Until extension exists:
1. **Set up Nimbus Screenshot** with auto-capture
2. **Use keyboard shortcut** (Windows: Win+Shift+S, Mac: Cmd+Shift+4)
3. **Save immediately** to `evals/results/`
4. **Fill template** while it's fresh in memory

---

*You're absolutely right - there should be an extension for this! Let's build one or find the best existing solution.*

