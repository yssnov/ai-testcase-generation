# Diagrams

- `src/` — editable PlantUML sources (commit every change here).
- `export/` — SVG (thesis, convert to PDF/EPS for LaTeX) and PNG (slides).

Render: `java -jar plantuml.jar -tsvg -o ../export src/*.puml` and the same with `-tpng`. The VS Code "PlantUML" extension previews them while editing.
