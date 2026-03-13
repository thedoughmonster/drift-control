# Publishing Notes

This repository is a maintainer-facing publication root for the public drift-control handbook.

The current publishable artifact set in this root is:

- `README.md`: handbook landing page and Docsify homepage content
- `core-model.md`: system model, drift loop, and evidence standard
- `minimum-viable-implementation.md`: baseline minimum controls and complexity-triggered additions
- `enforcement-model.md`: layered enforcement explanation, legend, and control matrix
- `implementation-guide.md`: adoption sequence and operating patterns
- `reference-implementation-example.md`: optional appendix with one concrete implementation example
- `_sidebar.md`: Docsify navigation
- `index.html`: Docsify shell entrypoint
- `.nojekyll`: GitHub Pages compatibility marker

Publishing guidance:

- publish the repository root as a static site
- keep filenames and relative links stable when adding new handbook pages
- keep maintainer notes limited to this public artifact set and its packaging behavior
