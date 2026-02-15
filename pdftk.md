# pdftk

https://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/

## Combine files

```
pdftk $FILE1 $FILE2 $FILE3 ...  cat output merged.pdf

```
```
pdftk $(ls -v *.pdf) cat output merged.pdf
```

