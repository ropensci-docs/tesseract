# Tesseract Training Data

Helper function to download training data from the official
[tessdata](https://tesseract-ocr.github.io/tessdoc/Data-Files)
repository. On Linux, the fast training data can be installed directly
with [yum](https://src.fedoraproject.org/rpms/tesseract) or
[apt-get](https://packages.debian.org/search?suite=stable&section=all&arch=any&searchon=names&keywords=tesseract-ocr-).

## Usage

``` r
tesseract_download(
  lang,
  datapath = NULL,
  model = c("fast", "best"),
  progress = interactive()
)
```

## Arguments

- lang:

  three letter code for language, see
  [tessdata](https://github.com/tesseract-ocr/tessdata) repository.

- datapath:

  destination directory where to download store the file

- model:

  either `fast` or `best` is currently supported. The latter downloads
  more accurate (but slower) trained models for Tesseract 4.0 or higher

- progress:

  print progress while downloading

## Details

Tesseract uses training data to perform OCR. Most systems default to
English training data. To improve OCR performance for other languages
you can to install the training data from your distribution. For example
to install the spanish training data:

- [tesseract-ocr-spa](https://packages.debian.org/testing/tesseract-ocr-spa)
  (Debian, Ubuntu)

- `tesseract-langpack-spa` (Fedora, EPEL)

On Windows and MacOS you can install languages using the
tesseract_download function which downloads training data directly from
[github](https://github.com/tesseract-ocr/tessdata) and stores it in a
the path on disk given by the `TESSDATA_PREFIX` variable.

## References

[tesseract wiki: training
data](https://tesseract-ocr.github.io/tessdoc/Data-Files)

## See also

Other tesseract:
[`ocr()`](https://docs.ropensci.org/tesseract/reference/ocr.md),
[`tesseract()`](https://docs.ropensci.org/tesseract/reference/tesseract.md)

## Examples

``` r
if (FALSE) { # \dontrun{
if(is.na(match("fra", tesseract_info()$available)))
  tesseract_download("fra", model = 'best')
french <- tesseract("fra")
text <- ocr("https://jeroen.github.io/images/french_text.png", engine = french)
cat(text)
} # }
```
