# Tesseract Engine

Create an OCR engine for a given language and control parameters. This
can be used by the
[ocr](https://docs.ropensci.org/tesseract/reference/ocr.md) and
[ocr_data](https://docs.ropensci.org/tesseract/reference/ocr.md)
functions to recognize text.

## Usage

``` r
tesseract(
  language = "eng",
  datapath = NULL,
  configs = NULL,
  options = NULL,
  cache = TRUE
)

tesseract_params(filter = "")

tesseract_info()
```

## Arguments

- language:

  string with language for training data. Usually defaults to `eng`

- datapath:

  path with the training data for this language. Default uses the system
  library.

- configs:

  character vector with files, each containing one or more parameter
  values. These config files can exist in the current directory or one
  of the standard tesseract config files that live in the tessdata
  directory. See details.

- options:

  a named list with tesseract parameters. See details.

- cache:

  speed things up by caching engines

- filter:

  only list parameters containing a particular string

## Details

Tesseract control parameters can be set either via a named list in the
`options` parameter, or in a `config` file text file which contains the
parameter name followed by a space and then the value, one per line. Use
`tesseract_params()` to list or find parameters. Note that that some
parameters are only supported in certain versions of libtesseract, and
that invalid parameters can sometimes cause libtesseract to crash.

## See also

Other tesseract:
[`ocr()`](https://docs.ropensci.org/tesseract/reference/ocr.md),
[`tesseract_download()`](https://docs.ropensci.org/tesseract/reference/tessdata.md)

## Examples

``` r
tesseract_params('debug')
#> # A tibble: 61 × 3
#>    param                       default    desc                                  
#>  * <chr>                       <chr>      <chr>                                 
#>  1 textord_debug_block         0          Block to do debug on                  
#>  2 devanagari_split_debuglevel 0          Debug level for split shiro-rekha pro…
#>  3 textord_debug_tabfind       0          Debug tab finding                     
#>  4 textord_debug_bugs          0          Turn on output related to bugs in tab…
#>  5 textord_testregion_left     -1         Left edge of debug reporting rectangl…
#>  6 textord_testregion_top      2147483647 Top edge of debug reporting rectangle…
#>  7 textord_testregion_right    2147483647 Right edge of debug rectangle in Lept…
#>  8 textord_testregion_bottom   -1         Bottom edge of debug rectangle in Lep…
#>  9 textord_debug_pitch_test    0          Debug on fixed pitch test             
#> 10 textord_debug_pitch_metric  0          Write full metric stuff               
#> # ℹ 51 more rows
```
