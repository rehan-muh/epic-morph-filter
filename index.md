---
layout: default
title: Greek Morphology + Ending Filter
---

# Greek Morphology + Ending Filter

A lightweight browser tool for:
- **sequential morphology filtering** (`pos`, `person`, `number`, `tense`, `mood`, `voice`, `gender`, `case`)
- **Greek ending filtering** (e.g. `οις`, `οισι`, `οισιν`)
- **accent-insensitive matching**
- optional **binary indicator column**
- CSV **download** of the filtered output

> Everything runs client-side in your browser. No server/database needed.

---

## 1. Load CSV

<div class="card">
  <label for="csvFile"><strong>CSV file</strong></label>
  <input id="csvFile" type="file" accept=".csv,text/csv" />
  <div class="help">Expected columns include morphology fields such as <code>pos</code>, <code>person</code>, <code>number</code>, <code>tense</code>, <code>mood</code>, <code>voice</code>, <code>gender</code>, <code>case</code> (any subset is fine).</div>
  <div id="loadStatus" class="status muted">No file loaded yet.</div>
</div>

---

## 2. Morphology filter (sequential)

<div class="card">
  <label class="inline">
    <input type="checkbox" id="autoLockSingletons" checked />
    Auto-lock forced values (e.g. person = `-`)
  </label>

  <div id="morphControls" class="grid-2"></div>

  <div class="btn-row">
    <button id="btnMorph" class="btn btn-primary" disabled>1) Create morph-filtered dataframe</button>
    <button id="btnReset" class="btn btn-warn" disabled>Reset selections</button>
  </div>
</div>

---

## 3. Ending filter

<div class="card">
  <div class="field">
    <label for="formCol"><strong>Form column</strong></label>
    <select id="formCol" disabled></select>
  </div>

  <div class="field">
    <label for="endings"><strong>Endings</strong> (comma-separated)</label>
    <input id="endings" type="text" value="οις, οισι, οισιν" />
  </div>

  <div class="field">
    <label><strong>Match mode</strong></label>
    <div class="inline-group">
      <label class="inline"><input type="radio" name="matchMode" value="endswith" checked /> endswith</label>
      <label class="inline"><input type="radio" name="matchMode" value="equals" /> equals</label>
      <label class="inline"><input type="radio" name="matchMode" value="contains" /> contains</label>
    </div>
  </div>

  <div class="inline-group">
    <label class="inline"><input id="accentInsensitive" type="checkbox" checked /> accent-insensitive</label>
    <label class="inline"><input id="lowercaseCompare" type="checkbox" checked /> lowercase compare</label>
  </div>

  <div class="inline-group">
    <label class="inline"><input id="addBinary" type="checkbox" /> add binary column?</label>
    <input id="binaryName" type="text" value="ending_match_binary" placeholder="binary column name" />
  </div>

  <div class="field">
    <label for="binaryPositive"><strong>Positive endings</strong> (optional subset)</label>
    <input id="binaryPositive" type="text" value="" placeholder="blank = all selected endings" />
  </div>

  <div class="btn-row">
    <button id="btnEndings" class="btn btn-primary" disabled>2) Filter by endings</button>
  </div>
</div>

---

## 4. Download filtered CSV

<div class="card">
  <div class="field">
    <label for="baseName"><strong>Base filename</strong></label>
    <input id="baseName" type="text" value="filtered_output" />
  </div>

  <div class="btn-row">
    <button id="btnDownload" class="btn btn-success" disabled>3) Download current dataframe (.csv)</button>
  </div>

  <div class="help">
    The website cannot write directly to Google Drive or arbitrary local folders (unlike Colab), but it can generate a CSV download.
  </div>
</div>

---

## Status / Preview

<div class="card">
  <pre id="statusBox" class="status">Load a CSV to begin.</pre>
</div>

<div class="card">
  <div class="preview-header">
    <strong>Preview (first rows)</strong>
    <span id="previewMeta" class="muted"></span>
  </div>
  <div id="tableWrap" class="table-wrap"></div>
</div>
