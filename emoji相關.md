# R 官方套件

## Emoji 套件

* [Emojifont](https://cran.r-project.org/web/packages/emojifont/emojifont.pdf)
* [emo](https://github.com/hadley/emo) Easily insert emoji into R and RMarkdown

## 相關說明與記錄

1. R >= 3.4.0
2. 需要安裝之相關套件 ggplot2, proto, showtext, sysfonts, utils
3. [showtext](https://cran.r-project.org/web/packages/showtext/index.html): Using Fonts More Easily in R Graphs
4. [hexSticker](https://github.com/GuangchuangYu/hexSticker) 產生六角形貼紙


# Emoji 相關知識

1. [Emoji-Cheat-Sheet](https://www.webfx.com/tools/emoji-cheat-sheet/)
2. [用 JavaScript 玩轉 Emoji 表情圖示原來這麼簡單](https://blog.miniasp.com/post/2019/01/08/Understanding-Emoji-Unicode-and-JavaScript#continue)
3. [Unicode: Emoji, accents, and international text](https://cran.r-project.org/web/packages/utf8/vignettes/utf8.html)
4. [Unicdoe Emoji 12.0 版資料表](http://www.unicode.org/Public/emoji/12.0/emoji-data.txt)

## RStudio 1.2 版 Preview

[RStudio 1.2 版 Preview](https://www.rstudio.com/products/rstudio/download/preview/)

## 產生 ASCII Table

```
# =============================================================================
# ASCII 範例
# ASCII Table: http://www.asciitable.com/
# 範例程式來源: https://cran.r-project.org/web/packages/utf8/vignettes/utf8.html
# 程式修改與解說: Daniel
# =============================================================================
# ASCII 為 0 ~ 127 的編碼 2^7 = 128
# 原範例是16進位表示
ASCII_range <- 0:127
ASCIITable_ROW <- 8
ASCIITable_COL <- 16
ASCII_dimnames <- list(0:7, c(0:9, LETTERS[1:6]))
# 產生 ASCII 資料
codes <- matrix(ASCII_range, nrow = ASCIITable_ROW, ncol = ASCIITable_COL, 
                byrow = TRUE,
                dimnames = ASCII_dimnames)
# intToUtf8 在 BASE 套件中，可以做這方面的轉換
ascii <- apply(codes, c(1, 2), intToUtf8)
ascii
# > ascii
# 0      1      2      3      4      5      6      7      8      9      A      B      C      D      E      F     
# 0 ""     "\001" "\002" "\003" "\004" "\005" "\006" "\a"   "\b"   "\t"   "\n"   "\v"   "\f"   "\r"   "\016" "\017"
# 1 "\020" "\021" "\022" "\023" "\024" "\025" "\026" "\027" "\030" "\031" "\032" "\033" "\034" "\035" "\036" "\037"
# 2 " "    "!"    "\""   "#"    "$"    "%"    "&"    "'"    "("    ")"    "*"    "+"    ","    "-"    "."    "/"   
# 3 "0"    "1"    "2"    "3"    "4"    "5"    "6"    "7"    "8"    "9"    ":"    ";"    "<"    "="    ">"    "?"   
# 4 "@"    "A"    "B"    "C"    "D"    "E"    "F"    "G"    "H"    "I"    "J"    "K"    "L"    "M"    "N"    "O"   
# 5 "P"    "Q"    "R"    "S"    "T"    "U"    "V"    "W"    "X"    "Y"    "Z"    "["    "\\"   "]"    "^"    "_"   
# 6 "`"    "a"    "b"    "c"    "d"    "e"    "f"    "g"    "h"    "i"    "j"    "k"    "l"    "m"    "n"    "o"   
# 7 "p"    "q"    "r"    "s"    "t"    "u"    "v"    "w"    "x"    "y"    "z"    "{"    "|"    "}"    "~"    "\177"

# 處理控制碼
# 處理第一列非鍵盤控制字元
ascii["0", c(0:6, "E", "F")] <- ""
# 處理第二列非鍵盤控制字元
ascii["1",] <- ""
# 將最後 127 位置的 DEL 字元設定為空值(不可見字元)
ascii["7", "F"] <- ""
# 列印時不使用引號
utf8_print(ascii, quote = FALSE)
```
