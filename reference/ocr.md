# Tesseract OCR

Extract text from an image. Requires that you have training data for the
language you are reading. Works best for images with high contrast,
little noise and horizontal text. See [tesseract
wiki](https://github.com/tesseract-ocr/tesseract/wiki/ImproveQuality)
and our package vignette for image preprocessing tips.

## Usage

``` r
ocr(image, engine = tesseract("eng"), HOCR = FALSE)

ocr_data(image, engine = tesseract("eng"))
```

## Arguments

- image:

  file path, url, or raw vector to image (png, tiff, jpeg, etc)

- engine:

  a tesseract engine created with
  [`tesseract()`](https://docs.ropensci.org/tesseract/reference/tesseract.md).
  Alternatively a language string which will be passed to
  [`tesseract()`](https://docs.ropensci.org/tesseract/reference/tesseract.md).

- HOCR:

  if `TRUE` return results as HOCR xml instead of plain text

## Details

The `ocr()` function returns plain text by default, or hOCR text if hOCR
is set to `TRUE`. The `ocr_data()` function returns a data frame with a
confidence rate and bounding box for each word in the text.

## References

[Tesseract: Improving
Quality](https://github.com/tesseract-ocr/tesseract/wiki/ImproveQuality)

## See also

Other tesseract:
[`tesseract()`](https://docs.ropensci.org/tesseract/reference/tesseract.md),
[`tesseract_download()`](https://docs.ropensci.org/tesseract/reference/tessdata.md)

## Examples

``` r
# \donttest{
text <- ocr("https://jeroen.github.io/images/testocr.png")
cat(text)
#> This is a lot of 12 point text to test the
#> ocr code and see if it works on all types
#> of file format.
#> 
#> The quick brown dog jumped over the
#> lazy fox. The quick brown dog jumped
#> over the lazy fox. The quick brown dog
#> jumped over the lazy fox. The quick
#> brown dog jumped over the lazy fox.

xml <- ocr("https://jeroen.github.io/images/testocr.png", HOCR = TRUE)
cat(xml)
#>   <div class='ocr_page' id='page_1' title='image "unknown"; bbox 0 0 640 480; ppageno 0; scan_res 300 300'>
#>    <div class='ocr_carea' id='block_1_1' title="bbox 36 92 618 361">
#>     <p class='ocr_par' id='par_1_1' lang='eng' title="bbox 36 92 618 184">
#>      <span class='ocr_line' id='line_1_1' title="bbox 36 92 580 122; baseline 0 -6; x_size 30; x_descenders 6; x_ascenders 6">
#>       <span class='ocrx_word' id='word_1_1' title='bbox 36 92 96 116; x_wconf 96'>This</span>
#>       <span class='ocrx_word' id='word_1_2' title='bbox 109 92 129 116; x_wconf 96'>is</span>
#>       <span class='ocrx_word' id='word_1_3' title='bbox 141 98 156 116; x_wconf 94'>a</span>
#>       <span class='ocrx_word' id='word_1_4' title='bbox 169 92 201 116; x_wconf 94'>lot</span>
#>       <span class='ocrx_word' id='word_1_5' title='bbox 212 92 240 116; x_wconf 96'>of</span>
#>       <span class='ocrx_word' id='word_1_6' title='bbox 251 92 282 116; x_wconf 96'>12</span>
#>       <span class='ocrx_word' id='word_1_7' title='bbox 296 92 364 122; x_wconf 96'>point</span>
#>       <span class='ocrx_word' id='word_1_8' title='bbox 374 93 427 116; x_wconf 96'>text</span>
#>       <span class='ocrx_word' id='word_1_9' title='bbox 437 93 463 116; x_wconf 96'>to</span>
#>       <span class='ocrx_word' id='word_1_10' title='bbox 474 93 526 116; x_wconf 96'>test</span>
#>       <span class='ocrx_word' id='word_1_11' title='bbox 536 92 580 116; x_wconf 96'>the</span>
#>      </span>
#>      <span class='ocr_line' id='line_1_2' title="bbox 36 126 618 157; baseline 0 -7; x_size 31; x_descenders 7; x_ascenders 6">
#>       <span class='ocrx_word' id='word_1_12' title='bbox 36 132 81 150; x_wconf 95'>ocr</span>
#>       <span class='ocrx_word' id='word_1_13' title='bbox 91 126 160 150; x_wconf 95'>code</span>
#>       <span class='ocrx_word' id='word_1_14' title='bbox 172 126 223 150; x_wconf 96'>and</span>
#>       <span class='ocrx_word' id='word_1_15' title='bbox 236 132 286 150; x_wconf 96'>see</span>
#>       <span class='ocrx_word' id='word_1_16' title='bbox 299 126 314 150; x_wconf 94'>if</span>
#>       <span class='ocrx_word' id='word_1_17' title='bbox 325 126 339 150; x_wconf 94'>it</span>
#>       <span class='ocrx_word' id='word_1_18' title='bbox 348 126 433 150; x_wconf 96'>works</span>
#>       <span class='ocrx_word' id='word_1_19' title='bbox 445 132 478 150; x_wconf 93'>on</span>
#>       <span class='ocrx_word' id='word_1_20' title='bbox 500 126 529 150; x_wconf 93'>all</span>
#>       <span class='ocrx_word' id='word_1_21' title='bbox 541 127 618 157; x_wconf 95'>types</span>
#>      </span>
#>      <span class='ocr_line' id='line_1_3' title="bbox 36 160 223 184; baseline 0 0; x_size 31.214842; x_descenders 7.2148418; x_ascenders 6">
#>       <span class='ocrx_word' id='word_1_22' title='bbox 36 160 64 184; x_wconf 96'>of</span>
#>       <span class='ocrx_word' id='word_1_23' title='bbox 72 160 113 184; x_wconf 95'>file</span>
#>       <span class='ocrx_word' id='word_1_24' title='bbox 123 160 223 184; x_wconf 95'>format.</span>
#>      </span>
#>     </p>
#> 
#>     <p class='ocr_par' id='par_1_2' lang='eng' title="bbox 36 194 597 361">
#>      <span class='ocr_line' id='line_1_4' title="bbox 36 194 585 225; baseline 0 -7; x_size 31; x_descenders 7; x_ascenders 6">
#>       <span class='ocrx_word' id='word_1_25' title='bbox 36 194 91 218; x_wconf 96'>The</span>
#>       <span class='ocrx_word' id='word_1_26' title='bbox 102 194 177 224; x_wconf 96'>quick</span>
#>       <span class='ocrx_word' id='word_1_27' title='bbox 189 194 274 218; x_wconf 96'>brown</span>
#>       <span class='ocrx_word' id='word_1_28' title='bbox 287 194 339 225; x_wconf 96'>dog</span>
#>       <span class='ocrx_word' id='word_1_29' title='bbox 348 194 456 225; x_wconf 96'>jumped</span>
#>       <span class='ocrx_word' id='word_1_30' title='bbox 468 200 531 218; x_wconf 96'>over</span>
#>       <span class='ocrx_word' id='word_1_31' title='bbox 540 194 585 218; x_wconf 96'>the</span>
#>      </span>
#>      <span class='ocr_line' id='line_1_5' title="bbox 37 228 585 259; baseline 0 -7; x_size 31; x_descenders 7; x_ascenders 6">
#>       <span class='ocrx_word' id='word_1_32' title='bbox 37 228 92 259; x_wconf 96'>lazy</span>
#>       <span class='ocrx_word' id='word_1_33' title='bbox 103 228 153 252; x_wconf 96'>fox.</span>
#>       <span class='ocrx_word' id='word_1_34' title='bbox 165 228 220 252; x_wconf 96'>The</span>
#>       <span class='ocrx_word' id='word_1_35' title='bbox 232 228 307 258; x_wconf 96'>quick</span>
#>       <span class='ocrx_word' id='word_1_36' title='bbox 319 228 404 252; x_wconf 96'>brown</span>
#>       <span class='ocrx_word' id='word_1_37' title='bbox 417 228 468 259; x_wconf 96'>dog</span>
#>       <span class='ocrx_word' id='word_1_38' title='bbox 478 228 585 259; x_wconf 95'>jumped</span>
#>      </span>
#>      <span class='ocr_line' id='line_1_6' title="bbox 36 262 597 293; baseline 0 -7; x_size 31; x_descenders 7; x_ascenders 6">
#>       <span class='ocrx_word' id='word_1_39' title='bbox 36 268 99 286; x_wconf 96'>over</span>
#>       <span class='ocrx_word' id='word_1_40' title='bbox 109 262 153 286; x_wconf 95'>the</span>
#>       <span class='ocrx_word' id='word_1_41' title='bbox 165 262 221 293; x_wconf 96'>lazy</span>
#>       <span class='ocrx_word' id='word_1_42' title='bbox 231 262 281 286; x_wconf 95'>fox.</span>
#>       <span class='ocrx_word' id='word_1_43' title='bbox 294 262 349 286; x_wconf 96'>The</span>
#>       <span class='ocrx_word' id='word_1_44' title='bbox 360 262 435 292; x_wconf 96'>quick</span>
#>       <span class='ocrx_word' id='word_1_45' title='bbox 447 262 532 286; x_wconf 96'>brown</span>
#>       <span class='ocrx_word' id='word_1_46' title='bbox 545 262 597 293; x_wconf 96'>dog</span>
#>      </span>
#>      <span class='ocr_line' id='line_1_7' title="bbox 43 296 561 327; baseline 0 -7; x_size 31; x_descenders 7; x_ascenders 6">
#>       <span class='ocrx_word' id='word_1_47' title='bbox 43 296 150 327; x_wconf 96'>jumped</span>
#>       <span class='ocrx_word' id='word_1_48' title='bbox 162 302 226 320; x_wconf 96'>over</span>
#>       <span class='ocrx_word' id='word_1_49' title='bbox 235 296 279 320; x_wconf 96'>the</span>
#>       <span class='ocrx_word' id='word_1_50' title='bbox 292 296 347 327; x_wconf 96'>lazy</span>
#>       <span class='ocrx_word' id='word_1_51' title='bbox 357 296 407 320; x_wconf 95'>fox.</span>
#>       <span class='ocrx_word' id='word_1_52' title='bbox 420 296 475 320; x_wconf 96'>The</span>
#>       <span class='ocrx_word' id='word_1_53' title='bbox 486 296 561 326; x_wconf 96'>quick</span>
#>      </span>
#>      <span class='ocr_line' id='line_1_8' title="bbox 37 330 561 361; baseline 0 -7; x_size 31; x_descenders 7; x_ascenders 6">
#>       <span class='ocrx_word' id='word_1_54' title='bbox 37 330 122 354; x_wconf 96'>brown</span>
#>       <span class='ocrx_word' id='word_1_55' title='bbox 135 330 187 361; x_wconf 96'>dog</span>
#>       <span class='ocrx_word' id='word_1_56' title='bbox 196 330 304 361; x_wconf 96'>jumped</span>
#>       <span class='ocrx_word' id='word_1_57' title='bbox 316 336 379 354; x_wconf 96'>over</span>
#>       <span class='ocrx_word' id='word_1_58' title='bbox 388 330 433 354; x_wconf 96'>the</span>
#>       <span class='ocrx_word' id='word_1_59' title='bbox 445 330 500 361; x_wconf 95'>lazy</span>
#>       <span class='ocrx_word' id='word_1_60' title='bbox 511 330 561 354; x_wconf 96'>fox.</span>
#>      </span>
#>     </p>
#>    </div>
#>   </div>

df <- ocr_data("https://jeroen.github.io/images/testocr.png")
print(df)
#> # A tibble: 60 × 3
#>    word  confidence bbox          
#>    <chr>      <dbl> <chr>         
#>  1 This        96.8 36,92,96,116  
#>  2 is          96.9 109,92,129,116
#>  3 a           95.0 141,98,156,116
#>  4 lot         95.0 169,92,201,116
#>  5 of          96.4 212,92,240,116
#>  6 12          96.4 251,92,282,116
#>  7 point       96.3 296,92,364,122
#>  8 text        96.2 374,93,427,116
#>  9 to          97.0 437,93,463,116
#> 10 test        97.0 474,93,526,116
#> # ℹ 50 more rows

# Full roundtrip test: render PDF to image and OCR it back to text
curl::curl_download("https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf", "R-intro.pdf")
orig <- pdftools::pdf_text("R-intro.pdf")[1]

# Render pdf to png image
img_file <- pdftools::pdf_convert("R-intro.pdf", format = 'tiff', pages = 1, dpi = 400)
#> Converting page 1 to R-intro_1.tiff... done!
unlink("R-intro.pdf")

# Extract text from png image
text <- ocr(img_file)
unlink(img_file)
cat(text)
#> An Introduction to R
#> Notes on R: A Programming Environment for Data Analysis and Graphics
#> Version 4.6.1 (2026-06-24)
#> W.N. Venables, D. M. Smith
#> and the R Core Team
# }

engine <- tesseract(options = list(tessedit_char_whitelist = "0123456789"))
```
