# PDF Compilation Instructions

**Note:** LaTeX (pdflatex) is not installed in the current environment. Use the following instructions to compile PDFs locally.

---

## Prerequisites

Install a LaTeX distribution:
- **macOS:** MacTeX (`brew install --cask mactex`)
- **Linux:** TeX Live (`sudo apt install texlive-full`)
- **Windows:** MiKTeX or TeX Live

---

## File Structure

```
manuscript-refinement/
├── caprazli-neural-scale.tex      # Original (reference)
├── caprazli-neural-scale-v1.tex   # Evidence & Hedging
├── caprazli-neural-scale-v2.tex   # CACM Calibration
├── caprazli-neural-scale-v3.tex   # Technical Rigor (RECOMMENDED)
├── references.bib                  # Original bibliography
├── references-v3.bib              # Updated bibliography (TiDAR removed)
└── ...
```

---

## Compilation Commands

### For v1 and v2 (use original references.bib)

```bash
cd manuscript-refinement

# Compile v1
pdflatex caprazli-neural-scale-v1.tex
bibtex caprazli-neural-scale-v1
pdflatex caprazli-neural-scale-v1.tex
pdflatex caprazli-neural-scale-v1.tex

# Compile v2
pdflatex caprazli-neural-scale-v2.tex
bibtex caprazli-neural-scale-v2
pdflatex caprazli-neural-scale-v2.tex
pdflatex caprazli-neural-scale-v2.tex
```

### For v3 (use references-v3.bib)

```bash
# First, update the bibliography reference in v3
# The file already references 'references' so either:
# Option A: Rename references-v3.bib to references.bib
cp references-v3.bib references.bib

# Option B: Or edit v3.tex to use references-v3
# Change: \bibliography{references}
# To:     \bibliography{references-v3}

# Then compile
pdflatex caprazli-neural-scale-v3.tex
bibtex caprazli-neural-scale-v3
pdflatex caprazli-neural-scale-v3.tex
pdflatex caprazli-neural-scale-v3.tex
```

---

## Troubleshooting

### Missing acmart.cls
The ACM article class may need to be installed:
```bash
# Most TeX distributions include it, but if not:
tlmgr install acmart
```

### Missing Packages
If compilation fails due to missing packages:
```bash
tlmgr install framed xcolor amsmath amssymb
```

### Font Issues
The template disables libertine fonts. If you still get font errors:
```bash
tlmgr install newtx libertine
```

---

## Expected Output

After successful compilation:
- `caprazli-neural-scale-v1.pdf`
- `caprazli-neural-scale-v2.pdf`
- `caprazli-neural-scale-v3.pdf`

---

## Recommended Submission

**Submit: `caprazli-neural-scale-v3.pdf`** compiled with `references-v3.bib`

This version includes:
- TiDAR error corrected
- Epistemic hedging appropriate for academic publication
- CACM audience background
- Formal mathematical specifications
- Explicit limitations and falsifiability criteria
