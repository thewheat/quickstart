# ePub

## Markdown to epub 

- Using [pandoc](https://pandoc.org/)

### Standard conversion 
```
pandoc input.md -o output.epub 
```

### Remove title page
```
pandoc input.md -o output.epub --epub-title-page=false
```

### Custom styles
- Create `.css` file
```
echo "" > style.css
```
- To remove all styles, leave file empty, otherwise customize CSS accordingly
- View default pandoc epub styles
```
pandoc --print-default-data-file epub.css
```
- Use `.css` file in `--css` 
```
pandoc input.md -o output.epub --css=style.css
```
