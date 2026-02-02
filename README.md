# Synchronized Online Friction Estimation and Adaptive Grasp Control for Robust Gentle Grasp

[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](http://creativecommons.org/licenses/by-sa/4.0/)

**Authors:** Zhenwei Niu, Xiaoyi Chen, Jiayu Hu, Zhaoyang Liu, Xiaozhu Ju*, Jian Tang  
**Affiliation:** X-Humanoid

This repository hosts the **project website** for our paper on gentle robotic grasping with real-time friction estimation and adaptive grasp control.

---

## Abstract

We introduce a unified framework for gentle robotic grasping that synergistically couples real-time friction estimation with adaptive grasp control. We propose a new particle filter-based method for real-time estimation of the friction coefficient using vision-based tactile sensors. This estimate is seamlessly integrated into a reactive controller that dynamically modulates grasp force to maintain a stable grip. The two processes operate synchronously in a closed-loop: the controller uses the current best estimate to adjust the force, while new tactile feedback from this action continuously refines the estimation. The reliability and efficiency of the complete framework are validated through extensive robotic experiments.

---

## Links

| Resource | Link |
|----------|------|
| **Paper (arXiv)** | [Add your arXiv link when available] |
| **Code** | [https://github.com/Ethan-nzw/SofeagcGrasp](https://github.com/Ethan-nzw/SofeagcGrasp) |
| **Project page** | [https://ethan-nzw.github.io/SofeagcGrasp/](https://ethan-nzw.github.io/SofeagcGrasp/) *(after enabling GitHub Pages)* |

---

## Project structure (website)

```
.
├── index.html              # Main entry (original template)
├── index_1.html            # Paper content (your edits)
├── index_improved.html     # Refined version (recommended for deployment)
├── static/
│   ├── css/                # Bulma, carousel, custom styles
│   ├── js/                 # Carousel, BibTeX copy, scroll-to-top
│   ├── images/             # Figures, favicon
│   ├── videos/             # Teaser and experiment videos
│   └── pdfs/               # Paper PDF (optional)
├── DEPLOY_TO_GITHUB.md     # Instructions to push to GitHub
└── README.md               # This file
```

---

## Viewing the website locally

1. Clone the repo:
   ```bash
   git clone https://github.com/Ethan-nzw/SofeagcGrasp.git
   cd SofeagcGrasp
   ```
2. Open in a browser:
   - **Recommended:** Open `index_improved.html` in your browser (double-click or `file:///path/to/index_improved.html`).
   - Or run a simple server, e.g.:
     ```bash
     python3 -m http.server 8000
     ```
     Then visit `http://localhost:8000/index_improved.html`.

---

## Deploying to GitHub Pages

1. Push this project to [SofeagcGrasp](https://github.com/Ethan-nzw/SofeagcGrasp) (see **DEPLOY_TO_GITHUB.md** for steps).
2. On GitHub: **Settings → Pages → Source**: Deploy from branch **master** (or **main**), root.
3. Your site will be live at **https://ethan-nzw.github.io/SofeagcGrasp/**.

To use the improved page as the default, rename `index_improved.html` to `index.html` before or after deploying.

---

## BibTeX

```bibtex
@article{SofeagcGrasp2025,
  title={Synchronized Online Friction Estimation and Adaptive Grasp Control for Robust Gentle Grasp},
  author={Niu, Zhenwei and Chen, Xiaoyi and Hu, Jiayu and Liu, Zhaoyang and Ju, Xiaozhu and Tang, Jian},
  journal={Conference/Journal Name},
  year={2025},
  url={https://github.com/Ethan-nzw/SofeagcGrasp}
}
```

*(Update `journal` and `url` when the paper is published.)*

---

## Acknowledgments

This project page is built using the [Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template), which was adopted from the [Nerfies](https://nerfies.github.io/) project page. We thank the authors for making their template available.

---

## License

This website is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
