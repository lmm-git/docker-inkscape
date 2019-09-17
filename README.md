# docker-inkscape

A simple docker container to generate PDFs or bitmap graphics from SVGs. Especially useful in combination with CI/CD processes.

## Example

To generate PDFs for all SVGs in a directory, execute this bash command:

```bash
find images/*.svg | xargs -i bash -c 'path="{}"; inkscape -z --export-pdf=${path::-3}pdf {}'
```

A complete yaml file for GitLab CI could look like

```yaml
images:
  stage: preprocess
  image: lmmdock/inkscape
  script:
    - find images/*.svg | xargs -i bash -c 'path="{}"; inkscape -z --export-pdf=${path::-3}pdf {}'
  artifacts:
    paths:
      - images
    expire_in: 1 week
```
