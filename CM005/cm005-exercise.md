---
title: 'cm005: `dplyr` Exercise'
output:
  html_document:
    keep_md: true
  
---

**Optional, but recommended startup**:

Change the file output to both html and md _documents_ (not notebook).

# Intro to `dplyr` syntax

1. Load the `gapminder` and `tidyverse` packages. Hint: `suppressPackageStartupMessages()`!
    - This loads `dplyr`, too.
2. `knit` the document. 


```r
#Load gapminder and tidyverse
library(gapminder)
library(tidyverse)
```

```
## -- Attaching packages ---------------------------------------- tidyverse 1.2.1 --
```

```
## v ggplot2 3.0.0     v purrr   0.2.5
## v tibble  1.4.2     v dplyr   0.7.6
## v tidyr   0.8.1     v stringr 1.3.1
## v readr   1.1.1     v forcats 0.3.0
```

```
## -- Conflicts ------------------------------------------- tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```


## `select()`
`select()` takes your data frame

1. Make a data frame containing the columns `year`, `lifeExp`, `country` from the gapminder data, in that order.

2. Select all variables, from `country` to `lifeExp`. 

3. Select all variables, except `lifeExp`.

4. Put `continent` first. Hint: use the `everything()` function.

5. Rename `continent` to `cont`.


```r
#Make a data frame (year, lifeExp, country)
data.frame(gapminder$year, gapminder$lifeExp, gapminder$country) #my way
```

```
##      gapminder.year gapminder.lifeExp        gapminder.country
## 1              1952          28.80100              Afghanistan
## 2              1957          30.33200              Afghanistan
## 3              1962          31.99700              Afghanistan
## 4              1967          34.02000              Afghanistan
## 5              1972          36.08800              Afghanistan
## 6              1977          38.43800              Afghanistan
## 7              1982          39.85400              Afghanistan
## 8              1987          40.82200              Afghanistan
## 9              1992          41.67400              Afghanistan
## 10             1997          41.76300              Afghanistan
## 11             2002          42.12900              Afghanistan
## 12             2007          43.82800              Afghanistan
## 13             1952          55.23000                  Albania
## 14             1957          59.28000                  Albania
## 15             1962          64.82000                  Albania
## 16             1967          66.22000                  Albania
## 17             1972          67.69000                  Albania
## 18             1977          68.93000                  Albania
## 19             1982          70.42000                  Albania
## 20             1987          72.00000                  Albania
## 21             1992          71.58100                  Albania
## 22             1997          72.95000                  Albania
## 23             2002          75.65100                  Albania
## 24             2007          76.42300                  Albania
## 25             1952          43.07700                  Algeria
## 26             1957          45.68500                  Algeria
## 27             1962          48.30300                  Algeria
## 28             1967          51.40700                  Algeria
## 29             1972          54.51800                  Algeria
## 30             1977          58.01400                  Algeria
## 31             1982          61.36800                  Algeria
## 32             1987          65.79900                  Algeria
## 33             1992          67.74400                  Algeria
## 34             1997          69.15200                  Algeria
## 35             2002          70.99400                  Algeria
## 36             2007          72.30100                  Algeria
## 37             1952          30.01500                   Angola
## 38             1957          31.99900                   Angola
## 39             1962          34.00000                   Angola
## 40             1967          35.98500                   Angola
## 41             1972          37.92800                   Angola
## 42             1977          39.48300                   Angola
## 43             1982          39.94200                   Angola
## 44             1987          39.90600                   Angola
## 45             1992          40.64700                   Angola
## 46             1997          40.96300                   Angola
## 47             2002          41.00300                   Angola
## 48             2007          42.73100                   Angola
## 49             1952          62.48500                Argentina
## 50             1957          64.39900                Argentina
## 51             1962          65.14200                Argentina
## 52             1967          65.63400                Argentina
## 53             1972          67.06500                Argentina
## 54             1977          68.48100                Argentina
## 55             1982          69.94200                Argentina
## 56             1987          70.77400                Argentina
## 57             1992          71.86800                Argentina
## 58             1997          73.27500                Argentina
## 59             2002          74.34000                Argentina
## 60             2007          75.32000                Argentina
## 61             1952          69.12000                Australia
## 62             1957          70.33000                Australia
## 63             1962          70.93000                Australia
## 64             1967          71.10000                Australia
## 65             1972          71.93000                Australia
## 66             1977          73.49000                Australia
## 67             1982          74.74000                Australia
## 68             1987          76.32000                Australia
## 69             1992          77.56000                Australia
## 70             1997          78.83000                Australia
## 71             2002          80.37000                Australia
## 72             2007          81.23500                Australia
## 73             1952          66.80000                  Austria
## 74             1957          67.48000                  Austria
## 75             1962          69.54000                  Austria
## 76             1967          70.14000                  Austria
## 77             1972          70.63000                  Austria
## 78             1977          72.17000                  Austria
## 79             1982          73.18000                  Austria
## 80             1987          74.94000                  Austria
## 81             1992          76.04000                  Austria
## 82             1997          77.51000                  Austria
## 83             2002          78.98000                  Austria
## 84             2007          79.82900                  Austria
## 85             1952          50.93900                  Bahrain
## 86             1957          53.83200                  Bahrain
## 87             1962          56.92300                  Bahrain
## 88             1967          59.92300                  Bahrain
## 89             1972          63.30000                  Bahrain
## 90             1977          65.59300                  Bahrain
## 91             1982          69.05200                  Bahrain
## 92             1987          70.75000                  Bahrain
## 93             1992          72.60100                  Bahrain
## 94             1997          73.92500                  Bahrain
## 95             2002          74.79500                  Bahrain
## 96             2007          75.63500                  Bahrain
## 97             1952          37.48400               Bangladesh
## 98             1957          39.34800               Bangladesh
## 99             1962          41.21600               Bangladesh
## 100            1967          43.45300               Bangladesh
## 101            1972          45.25200               Bangladesh
## 102            1977          46.92300               Bangladesh
## 103            1982          50.00900               Bangladesh
## 104            1987          52.81900               Bangladesh
## 105            1992          56.01800               Bangladesh
## 106            1997          59.41200               Bangladesh
## 107            2002          62.01300               Bangladesh
## 108            2007          64.06200               Bangladesh
## 109            1952          68.00000                  Belgium
## 110            1957          69.24000                  Belgium
## 111            1962          70.25000                  Belgium
## 112            1967          70.94000                  Belgium
## 113            1972          71.44000                  Belgium
## 114            1977          72.80000                  Belgium
## 115            1982          73.93000                  Belgium
## 116            1987          75.35000                  Belgium
## 117            1992          76.46000                  Belgium
## 118            1997          77.53000                  Belgium
## 119            2002          78.32000                  Belgium
## 120            2007          79.44100                  Belgium
## 121            1952          38.22300                    Benin
## 122            1957          40.35800                    Benin
## 123            1962          42.61800                    Benin
## 124            1967          44.88500                    Benin
## 125            1972          47.01400                    Benin
## 126            1977          49.19000                    Benin
## 127            1982          50.90400                    Benin
## 128            1987          52.33700                    Benin
## 129            1992          53.91900                    Benin
## 130            1997          54.77700                    Benin
## 131            2002          54.40600                    Benin
## 132            2007          56.72800                    Benin
## 133            1952          40.41400                  Bolivia
## 134            1957          41.89000                  Bolivia
## 135            1962          43.42800                  Bolivia
## 136            1967          45.03200                  Bolivia
## 137            1972          46.71400                  Bolivia
## 138            1977          50.02300                  Bolivia
## 139            1982          53.85900                  Bolivia
## 140            1987          57.25100                  Bolivia
## 141            1992          59.95700                  Bolivia
## 142            1997          62.05000                  Bolivia
## 143            2002          63.88300                  Bolivia
## 144            2007          65.55400                  Bolivia
## 145            1952          53.82000   Bosnia and Herzegovina
## 146            1957          58.45000   Bosnia and Herzegovina
## 147            1962          61.93000   Bosnia and Herzegovina
## 148            1967          64.79000   Bosnia and Herzegovina
## 149            1972          67.45000   Bosnia and Herzegovina
## 150            1977          69.86000   Bosnia and Herzegovina
## 151            1982          70.69000   Bosnia and Herzegovina
## 152            1987          71.14000   Bosnia and Herzegovina
## 153            1992          72.17800   Bosnia and Herzegovina
## 154            1997          73.24400   Bosnia and Herzegovina
## 155            2002          74.09000   Bosnia and Herzegovina
## 156            2007          74.85200   Bosnia and Herzegovina
## 157            1952          47.62200                 Botswana
## 158            1957          49.61800                 Botswana
## 159            1962          51.52000                 Botswana
## 160            1967          53.29800                 Botswana
## 161            1972          56.02400                 Botswana
## 162            1977          59.31900                 Botswana
## 163            1982          61.48400                 Botswana
## 164            1987          63.62200                 Botswana
## 165            1992          62.74500                 Botswana
## 166            1997          52.55600                 Botswana
## 167            2002          46.63400                 Botswana
## 168            2007          50.72800                 Botswana
## 169            1952          50.91700                   Brazil
## 170            1957          53.28500                   Brazil
## 171            1962          55.66500                   Brazil
## 172            1967          57.63200                   Brazil
## 173            1972          59.50400                   Brazil
## 174            1977          61.48900                   Brazil
## 175            1982          63.33600                   Brazil
## 176            1987          65.20500                   Brazil
## 177            1992          67.05700                   Brazil
## 178            1997          69.38800                   Brazil
## 179            2002          71.00600                   Brazil
## 180            2007          72.39000                   Brazil
## 181            1952          59.60000                 Bulgaria
## 182            1957          66.61000                 Bulgaria
## 183            1962          69.51000                 Bulgaria
## 184            1967          70.42000                 Bulgaria
## 185            1972          70.90000                 Bulgaria
## 186            1977          70.81000                 Bulgaria
## 187            1982          71.08000                 Bulgaria
## 188            1987          71.34000                 Bulgaria
## 189            1992          71.19000                 Bulgaria
## 190            1997          70.32000                 Bulgaria
## 191            2002          72.14000                 Bulgaria
## 192            2007          73.00500                 Bulgaria
## 193            1952          31.97500             Burkina Faso
## 194            1957          34.90600             Burkina Faso
## 195            1962          37.81400             Burkina Faso
## 196            1967          40.69700             Burkina Faso
## 197            1972          43.59100             Burkina Faso
## 198            1977          46.13700             Burkina Faso
## 199            1982          48.12200             Burkina Faso
## 200            1987          49.55700             Burkina Faso
## 201            1992          50.26000             Burkina Faso
## 202            1997          50.32400             Burkina Faso
## 203            2002          50.65000             Burkina Faso
## 204            2007          52.29500             Burkina Faso
## 205            1952          39.03100                  Burundi
## 206            1957          40.53300                  Burundi
## 207            1962          42.04500                  Burundi
## 208            1967          43.54800                  Burundi
## 209            1972          44.05700                  Burundi
## 210            1977          45.91000                  Burundi
## 211            1982          47.47100                  Burundi
## 212            1987          48.21100                  Burundi
## 213            1992          44.73600                  Burundi
## 214            1997          45.32600                  Burundi
## 215            2002          47.36000                  Burundi
## 216            2007          49.58000                  Burundi
## 217            1952          39.41700                 Cambodia
## 218            1957          41.36600                 Cambodia
## 219            1962          43.41500                 Cambodia
## 220            1967          45.41500                 Cambodia
## 221            1972          40.31700                 Cambodia
## 222            1977          31.22000                 Cambodia
## 223            1982          50.95700                 Cambodia
## 224            1987          53.91400                 Cambodia
## 225            1992          55.80300                 Cambodia
## 226            1997          56.53400                 Cambodia
## 227            2002          56.75200                 Cambodia
## 228            2007          59.72300                 Cambodia
## 229            1952          38.52300                 Cameroon
## 230            1957          40.42800                 Cameroon
## 231            1962          42.64300                 Cameroon
## 232            1967          44.79900                 Cameroon
## 233            1972          47.04900                 Cameroon
## 234            1977          49.35500                 Cameroon
## 235            1982          52.96100                 Cameroon
## 236            1987          54.98500                 Cameroon
## 237            1992          54.31400                 Cameroon
## 238            1997          52.19900                 Cameroon
## 239            2002          49.85600                 Cameroon
## 240            2007          50.43000                 Cameroon
## 241            1952          68.75000                   Canada
## 242            1957          69.96000                   Canada
## 243            1962          71.30000                   Canada
## 244            1967          72.13000                   Canada
## 245            1972          72.88000                   Canada
## 246            1977          74.21000                   Canada
## 247            1982          75.76000                   Canada
## 248            1987          76.86000                   Canada
## 249            1992          77.95000                   Canada
## 250            1997          78.61000                   Canada
## 251            2002          79.77000                   Canada
## 252            2007          80.65300                   Canada
## 253            1952          35.46300 Central African Republic
## 254            1957          37.46400 Central African Republic
## 255            1962          39.47500 Central African Republic
## 256            1967          41.47800 Central African Republic
## 257            1972          43.45700 Central African Republic
## 258            1977          46.77500 Central African Republic
## 259            1982          48.29500 Central African Republic
## 260            1987          50.48500 Central African Republic
## 261            1992          49.39600 Central African Republic
## 262            1997          46.06600 Central African Republic
## 263            2002          43.30800 Central African Republic
## 264            2007          44.74100 Central African Republic
## 265            1952          38.09200                     Chad
## 266            1957          39.88100                     Chad
## 267            1962          41.71600                     Chad
## 268            1967          43.60100                     Chad
## 269            1972          45.56900                     Chad
## 270            1977          47.38300                     Chad
## 271            1982          49.51700                     Chad
## 272            1987          51.05100                     Chad
## 273            1992          51.72400                     Chad
## 274            1997          51.57300                     Chad
## 275            2002          50.52500                     Chad
## 276            2007          50.65100                     Chad
## 277            1952          54.74500                    Chile
## 278            1957          56.07400                    Chile
## 279            1962          57.92400                    Chile
## 280            1967          60.52300                    Chile
## 281            1972          63.44100                    Chile
## 282            1977          67.05200                    Chile
## 283            1982          70.56500                    Chile
## 284            1987          72.49200                    Chile
## 285            1992          74.12600                    Chile
## 286            1997          75.81600                    Chile
## 287            2002          77.86000                    Chile
## 288            2007          78.55300                    Chile
## 289            1952          44.00000                    China
## 290            1957          50.54896                    China
## 291            1962          44.50136                    China
## 292            1967          58.38112                    China
## 293            1972          63.11888                    China
## 294            1977          63.96736                    China
## 295            1982          65.52500                    China
## 296            1987          67.27400                    China
## 297            1992          68.69000                    China
## 298            1997          70.42600                    China
## 299            2002          72.02800                    China
## 300            2007          72.96100                    China
## 301            1952          50.64300                 Colombia
## 302            1957          55.11800                 Colombia
## 303            1962          57.86300                 Colombia
## 304            1967          59.96300                 Colombia
## 305            1972          61.62300                 Colombia
## 306            1977          63.83700                 Colombia
## 307            1982          66.65300                 Colombia
## 308            1987          67.76800                 Colombia
## 309            1992          68.42100                 Colombia
## 310            1997          70.31300                 Colombia
## 311            2002          71.68200                 Colombia
## 312            2007          72.88900                 Colombia
## 313            1952          40.71500                  Comoros
## 314            1957          42.46000                  Comoros
## 315            1962          44.46700                  Comoros
## 316            1967          46.47200                  Comoros
## 317            1972          48.94400                  Comoros
## 318            1977          50.93900                  Comoros
## 319            1982          52.93300                  Comoros
## 320            1987          54.92600                  Comoros
## 321            1992          57.93900                  Comoros
## 322            1997          60.66000                  Comoros
## 323            2002          62.97400                  Comoros
## 324            2007          65.15200                  Comoros
## 325            1952          39.14300         Congo, Dem. Rep.
## 326            1957          40.65200         Congo, Dem. Rep.
## 327            1962          42.12200         Congo, Dem. Rep.
## 328            1967          44.05600         Congo, Dem. Rep.
## 329            1972          45.98900         Congo, Dem. Rep.
## 330            1977          47.80400         Congo, Dem. Rep.
## 331            1982          47.78400         Congo, Dem. Rep.
## 332            1987          47.41200         Congo, Dem. Rep.
## 333            1992          45.54800         Congo, Dem. Rep.
## 334            1997          42.58700         Congo, Dem. Rep.
## 335            2002          44.96600         Congo, Dem. Rep.
## 336            2007          46.46200         Congo, Dem. Rep.
## 337            1952          42.11100              Congo, Rep.
## 338            1957          45.05300              Congo, Rep.
## 339            1962          48.43500              Congo, Rep.
## 340            1967          52.04000              Congo, Rep.
## 341            1972          54.90700              Congo, Rep.
## 342            1977          55.62500              Congo, Rep.
## 343            1982          56.69500              Congo, Rep.
## 344            1987          57.47000              Congo, Rep.
## 345            1992          56.43300              Congo, Rep.
## 346            1997          52.96200              Congo, Rep.
## 347            2002          52.97000              Congo, Rep.
## 348            2007          55.32200              Congo, Rep.
## 349            1952          57.20600               Costa Rica
## 350            1957          60.02600               Costa Rica
## 351            1962          62.84200               Costa Rica
## 352            1967          65.42400               Costa Rica
## 353            1972          67.84900               Costa Rica
## 354            1977          70.75000               Costa Rica
## 355            1982          73.45000               Costa Rica
## 356            1987          74.75200               Costa Rica
## 357            1992          75.71300               Costa Rica
## 358            1997          77.26000               Costa Rica
## 359            2002          78.12300               Costa Rica
## 360            2007          78.78200               Costa Rica
## 361            1952          40.47700            Cote d'Ivoire
## 362            1957          42.46900            Cote d'Ivoire
## 363            1962          44.93000            Cote d'Ivoire
## 364            1967          47.35000            Cote d'Ivoire
## 365            1972          49.80100            Cote d'Ivoire
## 366            1977          52.37400            Cote d'Ivoire
## 367            1982          53.98300            Cote d'Ivoire
## 368            1987          54.65500            Cote d'Ivoire
## 369            1992          52.04400            Cote d'Ivoire
## 370            1997          47.99100            Cote d'Ivoire
## 371            2002          46.83200            Cote d'Ivoire
## 372            2007          48.32800            Cote d'Ivoire
## 373            1952          61.21000                  Croatia
## 374            1957          64.77000                  Croatia
## 375            1962          67.13000                  Croatia
## 376            1967          68.50000                  Croatia
## 377            1972          69.61000                  Croatia
## 378            1977          70.64000                  Croatia
## 379            1982          70.46000                  Croatia
## 380            1987          71.52000                  Croatia
## 381            1992          72.52700                  Croatia
## 382            1997          73.68000                  Croatia
## 383            2002          74.87600                  Croatia
## 384            2007          75.74800                  Croatia
## 385            1952          59.42100                     Cuba
## 386            1957          62.32500                     Cuba
## 387            1962          65.24600                     Cuba
## 388            1967          68.29000                     Cuba
## 389            1972          70.72300                     Cuba
## 390            1977          72.64900                     Cuba
## 391            1982          73.71700                     Cuba
## 392            1987          74.17400                     Cuba
## 393            1992          74.41400                     Cuba
## 394            1997          76.15100                     Cuba
## 395            2002          77.15800                     Cuba
## 396            2007          78.27300                     Cuba
## 397            1952          66.87000           Czech Republic
## 398            1957          69.03000           Czech Republic
## 399            1962          69.90000           Czech Republic
## 400            1967          70.38000           Czech Republic
## 401            1972          70.29000           Czech Republic
## 402            1977          70.71000           Czech Republic
## 403            1982          70.96000           Czech Republic
## 404            1987          71.58000           Czech Republic
## 405            1992          72.40000           Czech Republic
## 406            1997          74.01000           Czech Republic
## 407            2002          75.51000           Czech Republic
## 408            2007          76.48600           Czech Republic
## 409            1952          70.78000                  Denmark
## 410            1957          71.81000                  Denmark
## 411            1962          72.35000                  Denmark
## 412            1967          72.96000                  Denmark
## 413            1972          73.47000                  Denmark
## 414            1977          74.69000                  Denmark
## 415            1982          74.63000                  Denmark
## 416            1987          74.80000                  Denmark
## 417            1992          75.33000                  Denmark
## 418            1997          76.11000                  Denmark
## 419            2002          77.18000                  Denmark
## 420            2007          78.33200                  Denmark
## 421            1952          34.81200                 Djibouti
## 422            1957          37.32800                 Djibouti
## 423            1962          39.69300                 Djibouti
## 424            1967          42.07400                 Djibouti
## 425            1972          44.36600                 Djibouti
## 426            1977          46.51900                 Djibouti
## 427            1982          48.81200                 Djibouti
## 428            1987          50.04000                 Djibouti
## 429            1992          51.60400                 Djibouti
## 430            1997          53.15700                 Djibouti
## 431            2002          53.37300                 Djibouti
## 432            2007          54.79100                 Djibouti
## 433            1952          45.92800       Dominican Republic
## 434            1957          49.82800       Dominican Republic
## 435            1962          53.45900       Dominican Republic
## 436            1967          56.75100       Dominican Republic
## 437            1972          59.63100       Dominican Republic
## 438            1977          61.78800       Dominican Republic
## 439            1982          63.72700       Dominican Republic
## 440            1987          66.04600       Dominican Republic
## 441            1992          68.45700       Dominican Republic
## 442            1997          69.95700       Dominican Republic
## 443            2002          70.84700       Dominican Republic
## 444            2007          72.23500       Dominican Republic
## 445            1952          48.35700                  Ecuador
## 446            1957          51.35600                  Ecuador
## 447            1962          54.64000                  Ecuador
## 448            1967          56.67800                  Ecuador
## 449            1972          58.79600                  Ecuador
## 450            1977          61.31000                  Ecuador
## 451            1982          64.34200                  Ecuador
## 452            1987          67.23100                  Ecuador
## 453            1992          69.61300                  Ecuador
## 454            1997          72.31200                  Ecuador
## 455            2002          74.17300                  Ecuador
## 456            2007          74.99400                  Ecuador
## 457            1952          41.89300                    Egypt
## 458            1957          44.44400                    Egypt
## 459            1962          46.99200                    Egypt
## 460            1967          49.29300                    Egypt
## 461            1972          51.13700                    Egypt
## 462            1977          53.31900                    Egypt
## 463            1982          56.00600                    Egypt
## 464            1987          59.79700                    Egypt
## 465            1992          63.67400                    Egypt
## 466            1997          67.21700                    Egypt
## 467            2002          69.80600                    Egypt
## 468            2007          71.33800                    Egypt
## 469            1952          45.26200              El Salvador
## 470            1957          48.57000              El Salvador
## 471            1962          52.30700              El Salvador
## 472            1967          55.85500              El Salvador
## 473            1972          58.20700              El Salvador
## 474            1977          56.69600              El Salvador
## 475            1982          56.60400              El Salvador
## 476            1987          63.15400              El Salvador
## 477            1992          66.79800              El Salvador
## 478            1997          69.53500              El Salvador
## 479            2002          70.73400              El Salvador
## 480            2007          71.87800              El Salvador
## 481            1952          34.48200        Equatorial Guinea
## 482            1957          35.98300        Equatorial Guinea
## 483            1962          37.48500        Equatorial Guinea
## 484            1967          38.98700        Equatorial Guinea
## 485            1972          40.51600        Equatorial Guinea
## 486            1977          42.02400        Equatorial Guinea
## 487            1982          43.66200        Equatorial Guinea
## 488            1987          45.66400        Equatorial Guinea
## 489            1992          47.54500        Equatorial Guinea
## 490            1997          48.24500        Equatorial Guinea
## 491            2002          49.34800        Equatorial Guinea
## 492            2007          51.57900        Equatorial Guinea
## 493            1952          35.92800                  Eritrea
## 494            1957          38.04700                  Eritrea
## 495            1962          40.15800                  Eritrea
## 496            1967          42.18900                  Eritrea
## 497            1972          44.14200                  Eritrea
## 498            1977          44.53500                  Eritrea
## 499            1982          43.89000                  Eritrea
## 500            1987          46.45300                  Eritrea
## 501            1992          49.99100                  Eritrea
## 502            1997          53.37800                  Eritrea
## 503            2002          55.24000                  Eritrea
## 504            2007          58.04000                  Eritrea
## 505            1952          34.07800                 Ethiopia
## 506            1957          36.66700                 Ethiopia
## 507            1962          40.05900                 Ethiopia
## 508            1967          42.11500                 Ethiopia
## 509            1972          43.51500                 Ethiopia
## 510            1977          44.51000                 Ethiopia
## 511            1982          44.91600                 Ethiopia
## 512            1987          46.68400                 Ethiopia
## 513            1992          48.09100                 Ethiopia
## 514            1997          49.40200                 Ethiopia
## 515            2002          50.72500                 Ethiopia
## 516            2007          52.94700                 Ethiopia
## 517            1952          66.55000                  Finland
## 518            1957          67.49000                  Finland
## 519            1962          68.75000                  Finland
## 520            1967          69.83000                  Finland
## 521            1972          70.87000                  Finland
## 522            1977          72.52000                  Finland
## 523            1982          74.55000                  Finland
## 524            1987          74.83000                  Finland
## 525            1992          75.70000                  Finland
## 526            1997          77.13000                  Finland
## 527            2002          78.37000                  Finland
## 528            2007          79.31300                  Finland
## 529            1952          67.41000                   France
## 530            1957          68.93000                   France
## 531            1962          70.51000                   France
## 532            1967          71.55000                   France
## 533            1972          72.38000                   France
## 534            1977          73.83000                   France
## 535            1982          74.89000                   France
## 536            1987          76.34000                   France
## 537            1992          77.46000                   France
## 538            1997          78.64000                   France
## 539            2002          79.59000                   France
## 540            2007          80.65700                   France
## 541            1952          37.00300                    Gabon
## 542            1957          38.99900                    Gabon
## 543            1962          40.48900                    Gabon
## 544            1967          44.59800                    Gabon
## 545            1972          48.69000                    Gabon
## 546            1977          52.79000                    Gabon
## 547            1982          56.56400                    Gabon
## 548            1987          60.19000                    Gabon
## 549            1992          61.36600                    Gabon
## 550            1997          60.46100                    Gabon
## 551            2002          56.76100                    Gabon
## 552            2007          56.73500                    Gabon
## 553            1952          30.00000                   Gambia
## 554            1957          32.06500                   Gambia
## 555            1962          33.89600                   Gambia
## 556            1967          35.85700                   Gambia
## 557            1972          38.30800                   Gambia
## 558            1977          41.84200                   Gambia
## 559            1982          45.58000                   Gambia
## 560            1987          49.26500                   Gambia
## 561            1992          52.64400                   Gambia
## 562            1997          55.86100                   Gambia
## 563            2002          58.04100                   Gambia
## 564            2007          59.44800                   Gambia
## 565            1952          67.50000                  Germany
## 566            1957          69.10000                  Germany
## 567            1962          70.30000                  Germany
## 568            1967          70.80000                  Germany
## 569            1972          71.00000                  Germany
## 570            1977          72.50000                  Germany
## 571            1982          73.80000                  Germany
## 572            1987          74.84700                  Germany
## 573            1992          76.07000                  Germany
## 574            1997          77.34000                  Germany
## 575            2002          78.67000                  Germany
## 576            2007          79.40600                  Germany
## 577            1952          43.14900                    Ghana
## 578            1957          44.77900                    Ghana
## 579            1962          46.45200                    Ghana
## 580            1967          48.07200                    Ghana
## 581            1972          49.87500                    Ghana
## 582            1977          51.75600                    Ghana
## 583            1982          53.74400                    Ghana
## 584            1987          55.72900                    Ghana
## 585            1992          57.50100                    Ghana
## 586            1997          58.55600                    Ghana
## 587            2002          58.45300                    Ghana
## 588            2007          60.02200                    Ghana
## 589            1952          65.86000                   Greece
## 590            1957          67.86000                   Greece
## 591            1962          69.51000                   Greece
## 592            1967          71.00000                   Greece
## 593            1972          72.34000                   Greece
## 594            1977          73.68000                   Greece
## 595            1982          75.24000                   Greece
## 596            1987          76.67000                   Greece
## 597            1992          77.03000                   Greece
## 598            1997          77.86900                   Greece
## 599            2002          78.25600                   Greece
## 600            2007          79.48300                   Greece
## 601            1952          42.02300                Guatemala
## 602            1957          44.14200                Guatemala
## 603            1962          46.95400                Guatemala
## 604            1967          50.01600                Guatemala
## 605            1972          53.73800                Guatemala
## 606            1977          56.02900                Guatemala
## 607            1982          58.13700                Guatemala
## 608            1987          60.78200                Guatemala
## 609            1992          63.37300                Guatemala
## 610            1997          66.32200                Guatemala
## 611            2002          68.97800                Guatemala
## 612            2007          70.25900                Guatemala
## 613            1952          33.60900                   Guinea
## 614            1957          34.55800                   Guinea
## 615            1962          35.75300                   Guinea
## 616            1967          37.19700                   Guinea
## 617            1972          38.84200                   Guinea
## 618            1977          40.76200                   Guinea
## 619            1982          42.89100                   Guinea
## 620            1987          45.55200                   Guinea
## 621            1992          48.57600                   Guinea
## 622            1997          51.45500                   Guinea
## 623            2002          53.67600                   Guinea
## 624            2007          56.00700                   Guinea
## 625            1952          32.50000            Guinea-Bissau
## 626            1957          33.48900            Guinea-Bissau
## 627            1962          34.48800            Guinea-Bissau
## 628            1967          35.49200            Guinea-Bissau
## 629            1972          36.48600            Guinea-Bissau
## 630            1977          37.46500            Guinea-Bissau
## 631            1982          39.32700            Guinea-Bissau
## 632            1987          41.24500            Guinea-Bissau
## 633            1992          43.26600            Guinea-Bissau
## 634            1997          44.87300            Guinea-Bissau
## 635            2002          45.50400            Guinea-Bissau
## 636            2007          46.38800            Guinea-Bissau
## 637            1952          37.57900                    Haiti
## 638            1957          40.69600                    Haiti
## 639            1962          43.59000                    Haiti
## 640            1967          46.24300                    Haiti
## 641            1972          48.04200                    Haiti
## 642            1977          49.92300                    Haiti
## 643            1982          51.46100                    Haiti
## 644            1987          53.63600                    Haiti
## 645            1992          55.08900                    Haiti
## 646            1997          56.67100                    Haiti
## 647            2002          58.13700                    Haiti
## 648            2007          60.91600                    Haiti
## 649            1952          41.91200                 Honduras
## 650            1957          44.66500                 Honduras
## 651            1962          48.04100                 Honduras
## 652            1967          50.92400                 Honduras
## 653            1972          53.88400                 Honduras
## 654            1977          57.40200                 Honduras
## 655            1982          60.90900                 Honduras
## 656            1987          64.49200                 Honduras
## 657            1992          66.39900                 Honduras
## 658            1997          67.65900                 Honduras
## 659            2002          68.56500                 Honduras
## 660            2007          70.19800                 Honduras
## 661            1952          60.96000         Hong Kong, China
## 662            1957          64.75000         Hong Kong, China
## 663            1962          67.65000         Hong Kong, China
## 664            1967          70.00000         Hong Kong, China
## 665            1972          72.00000         Hong Kong, China
## 666            1977          73.60000         Hong Kong, China
## 667            1982          75.45000         Hong Kong, China
## 668            1987          76.20000         Hong Kong, China
## 669            1992          77.60100         Hong Kong, China
## 670            1997          80.00000         Hong Kong, China
## 671            2002          81.49500         Hong Kong, China
## 672            2007          82.20800         Hong Kong, China
## 673            1952          64.03000                  Hungary
## 674            1957          66.41000                  Hungary
## 675            1962          67.96000                  Hungary
## 676            1967          69.50000                  Hungary
## 677            1972          69.76000                  Hungary
## 678            1977          69.95000                  Hungary
## 679            1982          69.39000                  Hungary
## 680            1987          69.58000                  Hungary
## 681            1992          69.17000                  Hungary
## 682            1997          71.04000                  Hungary
## 683            2002          72.59000                  Hungary
## 684            2007          73.33800                  Hungary
## 685            1952          72.49000                  Iceland
## 686            1957          73.47000                  Iceland
## 687            1962          73.68000                  Iceland
## 688            1967          73.73000                  Iceland
## 689            1972          74.46000                  Iceland
## 690            1977          76.11000                  Iceland
## 691            1982          76.99000                  Iceland
## 692            1987          77.23000                  Iceland
## 693            1992          78.77000                  Iceland
## 694            1997          78.95000                  Iceland
## 695            2002          80.50000                  Iceland
## 696            2007          81.75700                  Iceland
## 697            1952          37.37300                    India
## 698            1957          40.24900                    India
## 699            1962          43.60500                    India
## 700            1967          47.19300                    India
## 701            1972          50.65100                    India
## 702            1977          54.20800                    India
## 703            1982          56.59600                    India
## 704            1987          58.55300                    India
## 705            1992          60.22300                    India
## 706            1997          61.76500                    India
## 707            2002          62.87900                    India
## 708            2007          64.69800                    India
## 709            1952          37.46800                Indonesia
## 710            1957          39.91800                Indonesia
## 711            1962          42.51800                Indonesia
## 712            1967          45.96400                Indonesia
## 713            1972          49.20300                Indonesia
## 714            1977          52.70200                Indonesia
## 715            1982          56.15900                Indonesia
## 716            1987          60.13700                Indonesia
## 717            1992          62.68100                Indonesia
## 718            1997          66.04100                Indonesia
## 719            2002          68.58800                Indonesia
## 720            2007          70.65000                Indonesia
## 721            1952          44.86900                     Iran
## 722            1957          47.18100                     Iran
## 723            1962          49.32500                     Iran
## 724            1967          52.46900                     Iran
## 725            1972          55.23400                     Iran
## 726            1977          57.70200                     Iran
## 727            1982          59.62000                     Iran
## 728            1987          63.04000                     Iran
## 729            1992          65.74200                     Iran
## 730            1997          68.04200                     Iran
## 731            2002          69.45100                     Iran
## 732            2007          70.96400                     Iran
## 733            1952          45.32000                     Iraq
## 734            1957          48.43700                     Iraq
## 735            1962          51.45700                     Iraq
## 736            1967          54.45900                     Iraq
## 737            1972          56.95000                     Iraq
## 738            1977          60.41300                     Iraq
## 739            1982          62.03800                     Iraq
## 740            1987          65.04400                     Iraq
## 741            1992          59.46100                     Iraq
## 742            1997          58.81100                     Iraq
## 743            2002          57.04600                     Iraq
## 744            2007          59.54500                     Iraq
## 745            1952          66.91000                  Ireland
## 746            1957          68.90000                  Ireland
## 747            1962          70.29000                  Ireland
## 748            1967          71.08000                  Ireland
## 749            1972          71.28000                  Ireland
## 750            1977          72.03000                  Ireland
## 751            1982          73.10000                  Ireland
## 752            1987          74.36000                  Ireland
## 753            1992          75.46700                  Ireland
## 754            1997          76.12200                  Ireland
## 755            2002          77.78300                  Ireland
## 756            2007          78.88500                  Ireland
## 757            1952          65.39000                   Israel
## 758            1957          67.84000                   Israel
## 759            1962          69.39000                   Israel
## 760            1967          70.75000                   Israel
## 761            1972          71.63000                   Israel
## 762            1977          73.06000                   Israel
## 763            1982          74.45000                   Israel
## 764            1987          75.60000                   Israel
## 765            1992          76.93000                   Israel
## 766            1997          78.26900                   Israel
## 767            2002          79.69600                   Israel
## 768            2007          80.74500                   Israel
## 769            1952          65.94000                    Italy
## 770            1957          67.81000                    Italy
## 771            1962          69.24000                    Italy
## 772            1967          71.06000                    Italy
## 773            1972          72.19000                    Italy
## 774            1977          73.48000                    Italy
## 775            1982          74.98000                    Italy
## 776            1987          76.42000                    Italy
## 777            1992          77.44000                    Italy
## 778            1997          78.82000                    Italy
## 779            2002          80.24000                    Italy
## 780            2007          80.54600                    Italy
## 781            1952          58.53000                  Jamaica
## 782            1957          62.61000                  Jamaica
## 783            1962          65.61000                  Jamaica
## 784            1967          67.51000                  Jamaica
## 785            1972          69.00000                  Jamaica
## 786            1977          70.11000                  Jamaica
## 787            1982          71.21000                  Jamaica
## 788            1987          71.77000                  Jamaica
## 789            1992          71.76600                  Jamaica
## 790            1997          72.26200                  Jamaica
## 791            2002          72.04700                  Jamaica
## 792            2007          72.56700                  Jamaica
## 793            1952          63.03000                    Japan
## 794            1957          65.50000                    Japan
## 795            1962          68.73000                    Japan
## 796            1967          71.43000                    Japan
## 797            1972          73.42000                    Japan
## 798            1977          75.38000                    Japan
## 799            1982          77.11000                    Japan
## 800            1987          78.67000                    Japan
## 801            1992          79.36000                    Japan
## 802            1997          80.69000                    Japan
## 803            2002          82.00000                    Japan
## 804            2007          82.60300                    Japan
## 805            1952          43.15800                   Jordan
## 806            1957          45.66900                   Jordan
## 807            1962          48.12600                   Jordan
## 808            1967          51.62900                   Jordan
## 809            1972          56.52800                   Jordan
## 810            1977          61.13400                   Jordan
## 811            1982          63.73900                   Jordan
## 812            1987          65.86900                   Jordan
## 813            1992          68.01500                   Jordan
## 814            1997          69.77200                   Jordan
## 815            2002          71.26300                   Jordan
## 816            2007          72.53500                   Jordan
## 817            1952          42.27000                    Kenya
## 818            1957          44.68600                    Kenya
## 819            1962          47.94900                    Kenya
## 820            1967          50.65400                    Kenya
## 821            1972          53.55900                    Kenya
## 822            1977          56.15500                    Kenya
## 823            1982          58.76600                    Kenya
## 824            1987          59.33900                    Kenya
## 825            1992          59.28500                    Kenya
## 826            1997          54.40700                    Kenya
## 827            2002          50.99200                    Kenya
## 828            2007          54.11000                    Kenya
## 829            1952          50.05600         Korea, Dem. Rep.
## 830            1957          54.08100         Korea, Dem. Rep.
## 831            1962          56.65600         Korea, Dem. Rep.
## 832            1967          59.94200         Korea, Dem. Rep.
## 833            1972          63.98300         Korea, Dem. Rep.
## 834            1977          67.15900         Korea, Dem. Rep.
## 835            1982          69.10000         Korea, Dem. Rep.
## 836            1987          70.64700         Korea, Dem. Rep.
## 837            1992          69.97800         Korea, Dem. Rep.
## 838            1997          67.72700         Korea, Dem. Rep.
## 839            2002          66.66200         Korea, Dem. Rep.
## 840            2007          67.29700         Korea, Dem. Rep.
## 841            1952          47.45300              Korea, Rep.
## 842            1957          52.68100              Korea, Rep.
## 843            1962          55.29200              Korea, Rep.
## 844            1967          57.71600              Korea, Rep.
## 845            1972          62.61200              Korea, Rep.
## 846            1977          64.76600              Korea, Rep.
## 847            1982          67.12300              Korea, Rep.
## 848            1987          69.81000              Korea, Rep.
## 849            1992          72.24400              Korea, Rep.
## 850            1997          74.64700              Korea, Rep.
## 851            2002          77.04500              Korea, Rep.
## 852            2007          78.62300              Korea, Rep.
## 853            1952          55.56500                   Kuwait
## 854            1957          58.03300                   Kuwait
## 855            1962          60.47000                   Kuwait
## 856            1967          64.62400                   Kuwait
## 857            1972          67.71200                   Kuwait
## 858            1977          69.34300                   Kuwait
## 859            1982          71.30900                   Kuwait
## 860            1987          74.17400                   Kuwait
## 861            1992          75.19000                   Kuwait
## 862            1997          76.15600                   Kuwait
## 863            2002          76.90400                   Kuwait
## 864            2007          77.58800                   Kuwait
## 865            1952          55.92800                  Lebanon
## 866            1957          59.48900                  Lebanon
## 867            1962          62.09400                  Lebanon
## 868            1967          63.87000                  Lebanon
## 869            1972          65.42100                  Lebanon
## 870            1977          66.09900                  Lebanon
## 871            1982          66.98300                  Lebanon
## 872            1987          67.92600                  Lebanon
## 873            1992          69.29200                  Lebanon
## 874            1997          70.26500                  Lebanon
## 875            2002          71.02800                  Lebanon
## 876            2007          71.99300                  Lebanon
## 877            1952          42.13800                  Lesotho
## 878            1957          45.04700                  Lesotho
## 879            1962          47.74700                  Lesotho
## 880            1967          48.49200                  Lesotho
## 881            1972          49.76700                  Lesotho
## 882            1977          52.20800                  Lesotho
## 883            1982          55.07800                  Lesotho
## 884            1987          57.18000                  Lesotho
## 885            1992          59.68500                  Lesotho
## 886            1997          55.55800                  Lesotho
## 887            2002          44.59300                  Lesotho
## 888            2007          42.59200                  Lesotho
## 889            1952          38.48000                  Liberia
## 890            1957          39.48600                  Liberia
## 891            1962          40.50200                  Liberia
## 892            1967          41.53600                  Liberia
## 893            1972          42.61400                  Liberia
## 894            1977          43.76400                  Liberia
## 895            1982          44.85200                  Liberia
## 896            1987          46.02700                  Liberia
## 897            1992          40.80200                  Liberia
## 898            1997          42.22100                  Liberia
## 899            2002          43.75300                  Liberia
## 900            2007          45.67800                  Liberia
## 901            1952          42.72300                    Libya
## 902            1957          45.28900                    Libya
## 903            1962          47.80800                    Libya
## 904            1967          50.22700                    Libya
## 905            1972          52.77300                    Libya
## 906            1977          57.44200                    Libya
## 907            1982          62.15500                    Libya
## 908            1987          66.23400                    Libya
## 909            1992          68.75500                    Libya
## 910            1997          71.55500                    Libya
## 911            2002          72.73700                    Libya
## 912            2007          73.95200                    Libya
## 913            1952          36.68100               Madagascar
## 914            1957          38.86500               Madagascar
## 915            1962          40.84800               Madagascar
## 916            1967          42.88100               Madagascar
## 917            1972          44.85100               Madagascar
## 918            1977          46.88100               Madagascar
## 919            1982          48.96900               Madagascar
## 920            1987          49.35000               Madagascar
## 921            1992          52.21400               Madagascar
## 922            1997          54.97800               Madagascar
## 923            2002          57.28600               Madagascar
## 924            2007          59.44300               Madagascar
## 925            1952          36.25600                   Malawi
## 926            1957          37.20700                   Malawi
## 927            1962          38.41000                   Malawi
## 928            1967          39.48700                   Malawi
## 929            1972          41.76600                   Malawi
## 930            1977          43.76700                   Malawi
## 931            1982          45.64200                   Malawi
## 932            1987          47.45700                   Malawi
## 933            1992          49.42000                   Malawi
## 934            1997          47.49500                   Malawi
## 935            2002          45.00900                   Malawi
## 936            2007          48.30300                   Malawi
## 937            1952          48.46300                 Malaysia
## 938            1957          52.10200                 Malaysia
## 939            1962          55.73700                 Malaysia
## 940            1967          59.37100                 Malaysia
## 941            1972          63.01000                 Malaysia
## 942            1977          65.25600                 Malaysia
## 943            1982          68.00000                 Malaysia
## 944            1987          69.50000                 Malaysia
## 945            1992          70.69300                 Malaysia
## 946            1997          71.93800                 Malaysia
## 947            2002          73.04400                 Malaysia
## 948            2007          74.24100                 Malaysia
## 949            1952          33.68500                     Mali
## 950            1957          35.30700                     Mali
## 951            1962          36.93600                     Mali
## 952            1967          38.48700                     Mali
## 953            1972          39.97700                     Mali
## 954            1977          41.71400                     Mali
## 955            1982          43.91600                     Mali
## 956            1987          46.36400                     Mali
## 957            1992          48.38800                     Mali
## 958            1997          49.90300                     Mali
## 959            2002          51.81800                     Mali
## 960            2007          54.46700                     Mali
## 961            1952          40.54300               Mauritania
## 962            1957          42.33800               Mauritania
## 963            1962          44.24800               Mauritania
## 964            1967          46.28900               Mauritania
## 965            1972          48.43700               Mauritania
## 966            1977          50.85200               Mauritania
## 967            1982          53.59900               Mauritania
## 968            1987          56.14500               Mauritania
## 969            1992          58.33300               Mauritania
## 970            1997          60.43000               Mauritania
## 971            2002          62.24700               Mauritania
## 972            2007          64.16400               Mauritania
## 973            1952          50.98600                Mauritius
## 974            1957          58.08900                Mauritius
## 975            1962          60.24600                Mauritius
## 976            1967          61.55700                Mauritius
## 977            1972          62.94400                Mauritius
## 978            1977          64.93000                Mauritius
## 979            1982          66.71100                Mauritius
## 980            1987          68.74000                Mauritius
## 981            1992          69.74500                Mauritius
## 982            1997          70.73600                Mauritius
## 983            2002          71.95400                Mauritius
## 984            2007          72.80100                Mauritius
## 985            1952          50.78900                   Mexico
## 986            1957          55.19000                   Mexico
## 987            1962          58.29900                   Mexico
## 988            1967          60.11000                   Mexico
## 989            1972          62.36100                   Mexico
## 990            1977          65.03200                   Mexico
## 991            1982          67.40500                   Mexico
## 992            1987          69.49800                   Mexico
## 993            1992          71.45500                   Mexico
## 994            1997          73.67000                   Mexico
## 995            2002          74.90200                   Mexico
## 996            2007          76.19500                   Mexico
## 997            1952          42.24400                 Mongolia
## 998            1957          45.24800                 Mongolia
## 999            1962          48.25100                 Mongolia
## 1000           1967          51.25300                 Mongolia
## 1001           1972          53.75400                 Mongolia
## 1002           1977          55.49100                 Mongolia
## 1003           1982          57.48900                 Mongolia
## 1004           1987          60.22200                 Mongolia
## 1005           1992          61.27100                 Mongolia
## 1006           1997          63.62500                 Mongolia
## 1007           2002          65.03300                 Mongolia
## 1008           2007          66.80300                 Mongolia
## 1009           1952          59.16400               Montenegro
## 1010           1957          61.44800               Montenegro
## 1011           1962          63.72800               Montenegro
## 1012           1967          67.17800               Montenegro
## 1013           1972          70.63600               Montenegro
## 1014           1977          73.06600               Montenegro
## 1015           1982          74.10100               Montenegro
## 1016           1987          74.86500               Montenegro
## 1017           1992          75.43500               Montenegro
## 1018           1997          75.44500               Montenegro
## 1019           2002          73.98100               Montenegro
## 1020           2007          74.54300               Montenegro
## 1021           1952          42.87300                  Morocco
## 1022           1957          45.42300                  Morocco
## 1023           1962          47.92400                  Morocco
## 1024           1967          50.33500                  Morocco
## 1025           1972          52.86200                  Morocco
## 1026           1977          55.73000                  Morocco
## 1027           1982          59.65000                  Morocco
## 1028           1987          62.67700                  Morocco
## 1029           1992          65.39300                  Morocco
## 1030           1997          67.66000                  Morocco
## 1031           2002          69.61500                  Morocco
## 1032           2007          71.16400                  Morocco
## 1033           1952          31.28600               Mozambique
## 1034           1957          33.77900               Mozambique
## 1035           1962          36.16100               Mozambique
## 1036           1967          38.11300               Mozambique
## 1037           1972          40.32800               Mozambique
## 1038           1977          42.49500               Mozambique
## 1039           1982          42.79500               Mozambique
## 1040           1987          42.86100               Mozambique
## 1041           1992          44.28400               Mozambique
## 1042           1997          46.34400               Mozambique
## 1043           2002          44.02600               Mozambique
## 1044           2007          42.08200               Mozambique
## 1045           1952          36.31900                  Myanmar
## 1046           1957          41.90500                  Myanmar
## 1047           1962          45.10800                  Myanmar
## 1048           1967          49.37900                  Myanmar
## 1049           1972          53.07000                  Myanmar
## 1050           1977          56.05900                  Myanmar
## 1051           1982          58.05600                  Myanmar
## 1052           1987          58.33900                  Myanmar
## 1053           1992          59.32000                  Myanmar
## 1054           1997          60.32800                  Myanmar
## 1055           2002          59.90800                  Myanmar
## 1056           2007          62.06900                  Myanmar
## 1057           1952          41.72500                  Namibia
## 1058           1957          45.22600                  Namibia
## 1059           1962          48.38600                  Namibia
## 1060           1967          51.15900                  Namibia
## 1061           1972          53.86700                  Namibia
## 1062           1977          56.43700                  Namibia
## 1063           1982          58.96800                  Namibia
## 1064           1987          60.83500                  Namibia
## 1065           1992          61.99900                  Namibia
## 1066           1997          58.90900                  Namibia
## 1067           2002          51.47900                  Namibia
## 1068           2007          52.90600                  Namibia
## 1069           1952          36.15700                    Nepal
## 1070           1957          37.68600                    Nepal
## 1071           1962          39.39300                    Nepal
## 1072           1967          41.47200                    Nepal
## 1073           1972          43.97100                    Nepal
## 1074           1977          46.74800                    Nepal
## 1075           1982          49.59400                    Nepal
## 1076           1987          52.53700                    Nepal
## 1077           1992          55.72700                    Nepal
## 1078           1997          59.42600                    Nepal
## 1079           2002          61.34000                    Nepal
## 1080           2007          63.78500                    Nepal
## 1081           1952          72.13000              Netherlands
## 1082           1957          72.99000              Netherlands
## 1083           1962          73.23000              Netherlands
## 1084           1967          73.82000              Netherlands
## 1085           1972          73.75000              Netherlands
## 1086           1977          75.24000              Netherlands
## 1087           1982          76.05000              Netherlands
## 1088           1987          76.83000              Netherlands
## 1089           1992          77.42000              Netherlands
## 1090           1997          78.03000              Netherlands
## 1091           2002          78.53000              Netherlands
## 1092           2007          79.76200              Netherlands
## 1093           1952          69.39000              New Zealand
## 1094           1957          70.26000              New Zealand
## 1095           1962          71.24000              New Zealand
## 1096           1967          71.52000              New Zealand
## 1097           1972          71.89000              New Zealand
## 1098           1977          72.22000              New Zealand
## 1099           1982          73.84000              New Zealand
## 1100           1987          74.32000              New Zealand
## 1101           1992          76.33000              New Zealand
## 1102           1997          77.55000              New Zealand
## 1103           2002          79.11000              New Zealand
## 1104           2007          80.20400              New Zealand
## 1105           1952          42.31400                Nicaragua
## 1106           1957          45.43200                Nicaragua
## 1107           1962          48.63200                Nicaragua
## 1108           1967          51.88400                Nicaragua
## 1109           1972          55.15100                Nicaragua
## 1110           1977          57.47000                Nicaragua
## 1111           1982          59.29800                Nicaragua
## 1112           1987          62.00800                Nicaragua
## 1113           1992          65.84300                Nicaragua
## 1114           1997          68.42600                Nicaragua
## 1115           2002          70.83600                Nicaragua
## 1116           2007          72.89900                Nicaragua
## 1117           1952          37.44400                    Niger
## 1118           1957          38.59800                    Niger
## 1119           1962          39.48700                    Niger
## 1120           1967          40.11800                    Niger
## 1121           1972          40.54600                    Niger
## 1122           1977          41.29100                    Niger
## 1123           1982          42.59800                    Niger
## 1124           1987          44.55500                    Niger
## 1125           1992          47.39100                    Niger
## 1126           1997          51.31300                    Niger
## 1127           2002          54.49600                    Niger
## 1128           2007          56.86700                    Niger
## 1129           1952          36.32400                  Nigeria
## 1130           1957          37.80200                  Nigeria
## 1131           1962          39.36000                  Nigeria
## 1132           1967          41.04000                  Nigeria
## 1133           1972          42.82100                  Nigeria
## 1134           1977          44.51400                  Nigeria
## 1135           1982          45.82600                  Nigeria
## 1136           1987          46.88600                  Nigeria
## 1137           1992          47.47200                  Nigeria
## 1138           1997          47.46400                  Nigeria
## 1139           2002          46.60800                  Nigeria
## 1140           2007          46.85900                  Nigeria
## 1141           1952          72.67000                   Norway
## 1142           1957          73.44000                   Norway
## 1143           1962          73.47000                   Norway
## 1144           1967          74.08000                   Norway
## 1145           1972          74.34000                   Norway
## 1146           1977          75.37000                   Norway
## 1147           1982          75.97000                   Norway
## 1148           1987          75.89000                   Norway
## 1149           1992          77.32000                   Norway
## 1150           1997          78.32000                   Norway
## 1151           2002          79.05000                   Norway
## 1152           2007          80.19600                   Norway
## 1153           1952          37.57800                     Oman
## 1154           1957          40.08000                     Oman
## 1155           1962          43.16500                     Oman
## 1156           1967          46.98800                     Oman
## 1157           1972          52.14300                     Oman
## 1158           1977          57.36700                     Oman
## 1159           1982          62.72800                     Oman
## 1160           1987          67.73400                     Oman
## 1161           1992          71.19700                     Oman
## 1162           1997          72.49900                     Oman
## 1163           2002          74.19300                     Oman
## 1164           2007          75.64000                     Oman
## 1165           1952          43.43600                 Pakistan
## 1166           1957          45.55700                 Pakistan
## 1167           1962          47.67000                 Pakistan
## 1168           1967          49.80000                 Pakistan
## 1169           1972          51.92900                 Pakistan
## 1170           1977          54.04300                 Pakistan
## 1171           1982          56.15800                 Pakistan
## 1172           1987          58.24500                 Pakistan
## 1173           1992          60.83800                 Pakistan
## 1174           1997          61.81800                 Pakistan
## 1175           2002          63.61000                 Pakistan
## 1176           2007          65.48300                 Pakistan
## 1177           1952          55.19100                   Panama
## 1178           1957          59.20100                   Panama
## 1179           1962          61.81700                   Panama
## 1180           1967          64.07100                   Panama
## 1181           1972          66.21600                   Panama
## 1182           1977          68.68100                   Panama
## 1183           1982          70.47200                   Panama
## 1184           1987          71.52300                   Panama
## 1185           1992          72.46200                   Panama
## 1186           1997          73.73800                   Panama
## 1187           2002          74.71200                   Panama
## 1188           2007          75.53700                   Panama
## 1189           1952          62.64900                 Paraguay
## 1190           1957          63.19600                 Paraguay
## 1191           1962          64.36100                 Paraguay
## 1192           1967          64.95100                 Paraguay
## 1193           1972          65.81500                 Paraguay
## 1194           1977          66.35300                 Paraguay
## 1195           1982          66.87400                 Paraguay
## 1196           1987          67.37800                 Paraguay
## 1197           1992          68.22500                 Paraguay
## 1198           1997          69.40000                 Paraguay
## 1199           2002          70.75500                 Paraguay
## 1200           2007          71.75200                 Paraguay
## 1201           1952          43.90200                     Peru
## 1202           1957          46.26300                     Peru
## 1203           1962          49.09600                     Peru
## 1204           1967          51.44500                     Peru
## 1205           1972          55.44800                     Peru
## 1206           1977          58.44700                     Peru
## 1207           1982          61.40600                     Peru
## 1208           1987          64.13400                     Peru
## 1209           1992          66.45800                     Peru
## 1210           1997          68.38600                     Peru
## 1211           2002          69.90600                     Peru
## 1212           2007          71.42100                     Peru
## 1213           1952          47.75200              Philippines
## 1214           1957          51.33400              Philippines
## 1215           1962          54.75700              Philippines
## 1216           1967          56.39300              Philippines
## 1217           1972          58.06500              Philippines
## 1218           1977          60.06000              Philippines
## 1219           1982          62.08200              Philippines
## 1220           1987          64.15100              Philippines
## 1221           1992          66.45800              Philippines
## 1222           1997          68.56400              Philippines
## 1223           2002          70.30300              Philippines
## 1224           2007          71.68800              Philippines
## 1225           1952          61.31000                   Poland
## 1226           1957          65.77000                   Poland
## 1227           1962          67.64000                   Poland
## 1228           1967          69.61000                   Poland
## 1229           1972          70.85000                   Poland
## 1230           1977          70.67000                   Poland
## 1231           1982          71.32000                   Poland
## 1232           1987          70.98000                   Poland
## 1233           1992          70.99000                   Poland
## 1234           1997          72.75000                   Poland
## 1235           2002          74.67000                   Poland
## 1236           2007          75.56300                   Poland
## 1237           1952          59.82000                 Portugal
## 1238           1957          61.51000                 Portugal
## 1239           1962          64.39000                 Portugal
## 1240           1967          66.60000                 Portugal
## 1241           1972          69.26000                 Portugal
## 1242           1977          70.41000                 Portugal
## 1243           1982          72.77000                 Portugal
## 1244           1987          74.06000                 Portugal
## 1245           1992          74.86000                 Portugal
## 1246           1997          75.97000                 Portugal
## 1247           2002          77.29000                 Portugal
## 1248           2007          78.09800                 Portugal
## 1249           1952          64.28000              Puerto Rico
## 1250           1957          68.54000              Puerto Rico
## 1251           1962          69.62000              Puerto Rico
## 1252           1967          71.10000              Puerto Rico
## 1253           1972          72.16000              Puerto Rico
## 1254           1977          73.44000              Puerto Rico
## 1255           1982          73.75000              Puerto Rico
## 1256           1987          74.63000              Puerto Rico
## 1257           1992          73.91100              Puerto Rico
## 1258           1997          74.91700              Puerto Rico
## 1259           2002          77.77800              Puerto Rico
## 1260           2007          78.74600              Puerto Rico
## 1261           1952          52.72400                  Reunion
## 1262           1957          55.09000                  Reunion
## 1263           1962          57.66600                  Reunion
## 1264           1967          60.54200                  Reunion
## 1265           1972          64.27400                  Reunion
## 1266           1977          67.06400                  Reunion
## 1267           1982          69.88500                  Reunion
## 1268           1987          71.91300                  Reunion
## 1269           1992          73.61500                  Reunion
## 1270           1997          74.77200                  Reunion
## 1271           2002          75.74400                  Reunion
## 1272           2007          76.44200                  Reunion
## 1273           1952          61.05000                  Romania
## 1274           1957          64.10000                  Romania
## 1275           1962          66.80000                  Romania
## 1276           1967          66.80000                  Romania
## 1277           1972          69.21000                  Romania
## 1278           1977          69.46000                  Romania
## 1279           1982          69.66000                  Romania
## 1280           1987          69.53000                  Romania
## 1281           1992          69.36000                  Romania
## 1282           1997          69.72000                  Romania
## 1283           2002          71.32200                  Romania
## 1284           2007          72.47600                  Romania
## 1285           1952          40.00000                   Rwanda
## 1286           1957          41.50000                   Rwanda
## 1287           1962          43.00000                   Rwanda
## 1288           1967          44.10000                   Rwanda
## 1289           1972          44.60000                   Rwanda
## 1290           1977          45.00000                   Rwanda
## 1291           1982          46.21800                   Rwanda
## 1292           1987          44.02000                   Rwanda
## 1293           1992          23.59900                   Rwanda
## 1294           1997          36.08700                   Rwanda
## 1295           2002          43.41300                   Rwanda
## 1296           2007          46.24200                   Rwanda
## 1297           1952          46.47100    Sao Tome and Principe
## 1298           1957          48.94500    Sao Tome and Principe
## 1299           1962          51.89300    Sao Tome and Principe
## 1300           1967          54.42500    Sao Tome and Principe
## 1301           1972          56.48000    Sao Tome and Principe
## 1302           1977          58.55000    Sao Tome and Principe
## 1303           1982          60.35100    Sao Tome and Principe
## 1304           1987          61.72800    Sao Tome and Principe
## 1305           1992          62.74200    Sao Tome and Principe
## 1306           1997          63.30600    Sao Tome and Principe
## 1307           2002          64.33700    Sao Tome and Principe
## 1308           2007          65.52800    Sao Tome and Principe
## 1309           1952          39.87500             Saudi Arabia
## 1310           1957          42.86800             Saudi Arabia
## 1311           1962          45.91400             Saudi Arabia
## 1312           1967          49.90100             Saudi Arabia
## 1313           1972          53.88600             Saudi Arabia
## 1314           1977          58.69000             Saudi Arabia
## 1315           1982          63.01200             Saudi Arabia
## 1316           1987          66.29500             Saudi Arabia
## 1317           1992          68.76800             Saudi Arabia
## 1318           1997          70.53300             Saudi Arabia
## 1319           2002          71.62600             Saudi Arabia
## 1320           2007          72.77700             Saudi Arabia
## 1321           1952          37.27800                  Senegal
## 1322           1957          39.32900                  Senegal
## 1323           1962          41.45400                  Senegal
## 1324           1967          43.56300                  Senegal
## 1325           1972          45.81500                  Senegal
## 1326           1977          48.87900                  Senegal
## 1327           1982          52.37900                  Senegal
## 1328           1987          55.76900                  Senegal
## 1329           1992          58.19600                  Senegal
## 1330           1997          60.18700                  Senegal
## 1331           2002          61.60000                  Senegal
## 1332           2007          63.06200                  Senegal
## 1333           1952          57.99600                   Serbia
## 1334           1957          61.68500                   Serbia
## 1335           1962          64.53100                   Serbia
## 1336           1967          66.91400                   Serbia
## 1337           1972          68.70000                   Serbia
## 1338           1977          70.30000                   Serbia
## 1339           1982          70.16200                   Serbia
## 1340           1987          71.21800                   Serbia
## 1341           1992          71.65900                   Serbia
## 1342           1997          72.23200                   Serbia
## 1343           2002          73.21300                   Serbia
## 1344           2007          74.00200                   Serbia
## 1345           1952          30.33100             Sierra Leone
## 1346           1957          31.57000             Sierra Leone
## 1347           1962          32.76700             Sierra Leone
## 1348           1967          34.11300             Sierra Leone
## 1349           1972          35.40000             Sierra Leone
## 1350           1977          36.78800             Sierra Leone
## 1351           1982          38.44500             Sierra Leone
## 1352           1987          40.00600             Sierra Leone
## 1353           1992          38.33300             Sierra Leone
## 1354           1997          39.89700             Sierra Leone
## 1355           2002          41.01200             Sierra Leone
## 1356           2007          42.56800             Sierra Leone
## 1357           1952          60.39600                Singapore
## 1358           1957          63.17900                Singapore
## 1359           1962          65.79800                Singapore
## 1360           1967          67.94600                Singapore
## 1361           1972          69.52100                Singapore
## 1362           1977          70.79500                Singapore
## 1363           1982          71.76000                Singapore
## 1364           1987          73.56000                Singapore
## 1365           1992          75.78800                Singapore
## 1366           1997          77.15800                Singapore
## 1367           2002          78.77000                Singapore
## 1368           2007          79.97200                Singapore
## 1369           1952          64.36000          Slovak Republic
## 1370           1957          67.45000          Slovak Republic
## 1371           1962          70.33000          Slovak Republic
## 1372           1967          70.98000          Slovak Republic
## 1373           1972          70.35000          Slovak Republic
## 1374           1977          70.45000          Slovak Republic
## 1375           1982          70.80000          Slovak Republic
## 1376           1987          71.08000          Slovak Republic
## 1377           1992          71.38000          Slovak Republic
## 1378           1997          72.71000          Slovak Republic
## 1379           2002          73.80000          Slovak Republic
## 1380           2007          74.66300          Slovak Republic
## 1381           1952          65.57000                 Slovenia
## 1382           1957          67.85000                 Slovenia
## 1383           1962          69.15000                 Slovenia
## 1384           1967          69.18000                 Slovenia
## 1385           1972          69.82000                 Slovenia
## 1386           1977          70.97000                 Slovenia
## 1387           1982          71.06300                 Slovenia
## 1388           1987          72.25000                 Slovenia
## 1389           1992          73.64000                 Slovenia
## 1390           1997          75.13000                 Slovenia
## 1391           2002          76.66000                 Slovenia
## 1392           2007          77.92600                 Slovenia
## 1393           1952          32.97800                  Somalia
## 1394           1957          34.97700                  Somalia
## 1395           1962          36.98100                  Somalia
## 1396           1967          38.97700                  Somalia
## 1397           1972          40.97300                  Somalia
## 1398           1977          41.97400                  Somalia
## 1399           1982          42.95500                  Somalia
## 1400           1987          44.50100                  Somalia
## 1401           1992          39.65800                  Somalia
## 1402           1997          43.79500                  Somalia
## 1403           2002          45.93600                  Somalia
## 1404           2007          48.15900                  Somalia
## 1405           1952          45.00900             South Africa
## 1406           1957          47.98500             South Africa
## 1407           1962          49.95100             South Africa
## 1408           1967          51.92700             South Africa
## 1409           1972          53.69600             South Africa
## 1410           1977          55.52700             South Africa
## 1411           1982          58.16100             South Africa
## 1412           1987          60.83400             South Africa
## 1413           1992          61.88800             South Africa
## 1414           1997          60.23600             South Africa
## 1415           2002          53.36500             South Africa
## 1416           2007          49.33900             South Africa
## 1417           1952          64.94000                    Spain
## 1418           1957          66.66000                    Spain
## 1419           1962          69.69000                    Spain
## 1420           1967          71.44000                    Spain
## 1421           1972          73.06000                    Spain
## 1422           1977          74.39000                    Spain
## 1423           1982          76.30000                    Spain
## 1424           1987          76.90000                    Spain
## 1425           1992          77.57000                    Spain
## 1426           1997          78.77000                    Spain
## 1427           2002          79.78000                    Spain
## 1428           2007          80.94100                    Spain
## 1429           1952          57.59300                Sri Lanka
## 1430           1957          61.45600                Sri Lanka
## 1431           1962          62.19200                Sri Lanka
## 1432           1967          64.26600                Sri Lanka
## 1433           1972          65.04200                Sri Lanka
## 1434           1977          65.94900                Sri Lanka
## 1435           1982          68.75700                Sri Lanka
## 1436           1987          69.01100                Sri Lanka
## 1437           1992          70.37900                Sri Lanka
## 1438           1997          70.45700                Sri Lanka
## 1439           2002          70.81500                Sri Lanka
## 1440           2007          72.39600                Sri Lanka
## 1441           1952          38.63500                    Sudan
## 1442           1957          39.62400                    Sudan
## 1443           1962          40.87000                    Sudan
## 1444           1967          42.85800                    Sudan
## 1445           1972          45.08300                    Sudan
## 1446           1977          47.80000                    Sudan
## 1447           1982          50.33800                    Sudan
## 1448           1987          51.74400                    Sudan
## 1449           1992          53.55600                    Sudan
## 1450           1997          55.37300                    Sudan
## 1451           2002          56.36900                    Sudan
## 1452           2007          58.55600                    Sudan
## 1453           1952          41.40700                Swaziland
## 1454           1957          43.42400                Swaziland
## 1455           1962          44.99200                Swaziland
## 1456           1967          46.63300                Swaziland
## 1457           1972          49.55200                Swaziland
## 1458           1977          52.53700                Swaziland
## 1459           1982          55.56100                Swaziland
## 1460           1987          57.67800                Swaziland
## 1461           1992          58.47400                Swaziland
## 1462           1997          54.28900                Swaziland
## 1463           2002          43.86900                Swaziland
## 1464           2007          39.61300                Swaziland
## 1465           1952          71.86000                   Sweden
## 1466           1957          72.49000                   Sweden
## 1467           1962          73.37000                   Sweden
## 1468           1967          74.16000                   Sweden
## 1469           1972          74.72000                   Sweden
## 1470           1977          75.44000                   Sweden
## 1471           1982          76.42000                   Sweden
## 1472           1987          77.19000                   Sweden
## 1473           1992          78.16000                   Sweden
## 1474           1997          79.39000                   Sweden
## 1475           2002          80.04000                   Sweden
## 1476           2007          80.88400                   Sweden
## 1477           1952          69.62000              Switzerland
## 1478           1957          70.56000              Switzerland
## 1479           1962          71.32000              Switzerland
## 1480           1967          72.77000              Switzerland
## 1481           1972          73.78000              Switzerland
## 1482           1977          75.39000              Switzerland
## 1483           1982          76.21000              Switzerland
## 1484           1987          77.41000              Switzerland
## 1485           1992          78.03000              Switzerland
## 1486           1997          79.37000              Switzerland
## 1487           2002          80.62000              Switzerland
## 1488           2007          81.70100              Switzerland
## 1489           1952          45.88300                    Syria
## 1490           1957          48.28400                    Syria
## 1491           1962          50.30500                    Syria
## 1492           1967          53.65500                    Syria
## 1493           1972          57.29600                    Syria
## 1494           1977          61.19500                    Syria
## 1495           1982          64.59000                    Syria
## 1496           1987          66.97400                    Syria
## 1497           1992          69.24900                    Syria
## 1498           1997          71.52700                    Syria
## 1499           2002          73.05300                    Syria
## 1500           2007          74.14300                    Syria
## 1501           1952          58.50000                   Taiwan
## 1502           1957          62.40000                   Taiwan
## 1503           1962          65.20000                   Taiwan
## 1504           1967          67.50000                   Taiwan
## 1505           1972          69.39000                   Taiwan
## 1506           1977          70.59000                   Taiwan
## 1507           1982          72.16000                   Taiwan
## 1508           1987          73.40000                   Taiwan
## 1509           1992          74.26000                   Taiwan
## 1510           1997          75.25000                   Taiwan
## 1511           2002          76.99000                   Taiwan
## 1512           2007          78.40000                   Taiwan
## 1513           1952          41.21500                 Tanzania
## 1514           1957          42.97400                 Tanzania
## 1515           1962          44.24600                 Tanzania
## 1516           1967          45.75700                 Tanzania
## 1517           1972          47.62000                 Tanzania
## 1518           1977          49.91900                 Tanzania
## 1519           1982          50.60800                 Tanzania
## 1520           1987          51.53500                 Tanzania
## 1521           1992          50.44000                 Tanzania
## 1522           1997          48.46600                 Tanzania
## 1523           2002          49.65100                 Tanzania
## 1524           2007          52.51700                 Tanzania
## 1525           1952          50.84800                 Thailand
## 1526           1957          53.63000                 Thailand
## 1527           1962          56.06100                 Thailand
## 1528           1967          58.28500                 Thailand
## 1529           1972          60.40500                 Thailand
## 1530           1977          62.49400                 Thailand
## 1531           1982          64.59700                 Thailand
## 1532           1987          66.08400                 Thailand
## 1533           1992          67.29800                 Thailand
## 1534           1997          67.52100                 Thailand
## 1535           2002          68.56400                 Thailand
## 1536           2007          70.61600                 Thailand
## 1537           1952          38.59600                     Togo
## 1538           1957          41.20800                     Togo
## 1539           1962          43.92200                     Togo
## 1540           1967          46.76900                     Togo
## 1541           1972          49.75900                     Togo
## 1542           1977          52.88700                     Togo
## 1543           1982          55.47100                     Togo
## 1544           1987          56.94100                     Togo
## 1545           1992          58.06100                     Togo
## 1546           1997          58.39000                     Togo
## 1547           2002          57.56100                     Togo
## 1548           2007          58.42000                     Togo
## 1549           1952          59.10000      Trinidad and Tobago
## 1550           1957          61.80000      Trinidad and Tobago
## 1551           1962          64.90000      Trinidad and Tobago
## 1552           1967          65.40000      Trinidad and Tobago
## 1553           1972          65.90000      Trinidad and Tobago
## 1554           1977          68.30000      Trinidad and Tobago
## 1555           1982          68.83200      Trinidad and Tobago
## 1556           1987          69.58200      Trinidad and Tobago
## 1557           1992          69.86200      Trinidad and Tobago
## 1558           1997          69.46500      Trinidad and Tobago
## 1559           2002          68.97600      Trinidad and Tobago
## 1560           2007          69.81900      Trinidad and Tobago
## 1561           1952          44.60000                  Tunisia
## 1562           1957          47.10000                  Tunisia
## 1563           1962          49.57900                  Tunisia
## 1564           1967          52.05300                  Tunisia
## 1565           1972          55.60200                  Tunisia
## 1566           1977          59.83700                  Tunisia
## 1567           1982          64.04800                  Tunisia
## 1568           1987          66.89400                  Tunisia
## 1569           1992          70.00100                  Tunisia
## 1570           1997          71.97300                  Tunisia
## 1571           2002          73.04200                  Tunisia
## 1572           2007          73.92300                  Tunisia
## 1573           1952          43.58500                   Turkey
## 1574           1957          48.07900                   Turkey
## 1575           1962          52.09800                   Turkey
## 1576           1967          54.33600                   Turkey
## 1577           1972          57.00500                   Turkey
## 1578           1977          59.50700                   Turkey
## 1579           1982          61.03600                   Turkey
## 1580           1987          63.10800                   Turkey
## 1581           1992          66.14600                   Turkey
## 1582           1997          68.83500                   Turkey
## 1583           2002          70.84500                   Turkey
## 1584           2007          71.77700                   Turkey
## 1585           1952          39.97800                   Uganda
## 1586           1957          42.57100                   Uganda
## 1587           1962          45.34400                   Uganda
## 1588           1967          48.05100                   Uganda
## 1589           1972          51.01600                   Uganda
## 1590           1977          50.35000                   Uganda
## 1591           1982          49.84900                   Uganda
## 1592           1987          51.50900                   Uganda
## 1593           1992          48.82500                   Uganda
## 1594           1997          44.57800                   Uganda
## 1595           2002          47.81300                   Uganda
## 1596           2007          51.54200                   Uganda
## 1597           1952          69.18000           United Kingdom
## 1598           1957          70.42000           United Kingdom
## 1599           1962          70.76000           United Kingdom
## 1600           1967          71.36000           United Kingdom
## 1601           1972          72.01000           United Kingdom
## 1602           1977          72.76000           United Kingdom
## 1603           1982          74.04000           United Kingdom
## 1604           1987          75.00700           United Kingdom
## 1605           1992          76.42000           United Kingdom
## 1606           1997          77.21800           United Kingdom
## 1607           2002          78.47100           United Kingdom
## 1608           2007          79.42500           United Kingdom
## 1609           1952          68.44000            United States
## 1610           1957          69.49000            United States
## 1611           1962          70.21000            United States
## 1612           1967          70.76000            United States
## 1613           1972          71.34000            United States
## 1614           1977          73.38000            United States
## 1615           1982          74.65000            United States
## 1616           1987          75.02000            United States
## 1617           1992          76.09000            United States
## 1618           1997          76.81000            United States
## 1619           2002          77.31000            United States
## 1620           2007          78.24200            United States
## 1621           1952          66.07100                  Uruguay
## 1622           1957          67.04400                  Uruguay
## 1623           1962          68.25300                  Uruguay
## 1624           1967          68.46800                  Uruguay
## 1625           1972          68.67300                  Uruguay
## 1626           1977          69.48100                  Uruguay
## 1627           1982          70.80500                  Uruguay
## 1628           1987          71.91800                  Uruguay
## 1629           1992          72.75200                  Uruguay
## 1630           1997          74.22300                  Uruguay
## 1631           2002          75.30700                  Uruguay
## 1632           2007          76.38400                  Uruguay
## 1633           1952          55.08800                Venezuela
## 1634           1957          57.90700                Venezuela
## 1635           1962          60.77000                Venezuela
## 1636           1967          63.47900                Venezuela
## 1637           1972          65.71200                Venezuela
## 1638           1977          67.45600                Venezuela
## 1639           1982          68.55700                Venezuela
## 1640           1987          70.19000                Venezuela
## 1641           1992          71.15000                Venezuela
## 1642           1997          72.14600                Venezuela
## 1643           2002          72.76600                Venezuela
## 1644           2007          73.74700                Venezuela
## 1645           1952          40.41200                  Vietnam
## 1646           1957          42.88700                  Vietnam
## 1647           1962          45.36300                  Vietnam
## 1648           1967          47.83800                  Vietnam
## 1649           1972          50.25400                  Vietnam
## 1650           1977          55.76400                  Vietnam
## 1651           1982          58.81600                  Vietnam
## 1652           1987          62.82000                  Vietnam
## 1653           1992          67.66200                  Vietnam
## 1654           1997          70.67200                  Vietnam
## 1655           2002          73.01700                  Vietnam
## 1656           2007          74.24900                  Vietnam
## 1657           1952          43.16000       West Bank and Gaza
## 1658           1957          45.67100       West Bank and Gaza
## 1659           1962          48.12700       West Bank and Gaza
## 1660           1967          51.63100       West Bank and Gaza
## 1661           1972          56.53200       West Bank and Gaza
## 1662           1977          60.76500       West Bank and Gaza
## 1663           1982          64.40600       West Bank and Gaza
## 1664           1987          67.04600       West Bank and Gaza
## 1665           1992          69.71800       West Bank and Gaza
## 1666           1997          71.09600       West Bank and Gaza
## 1667           2002          72.37000       West Bank and Gaza
## 1668           2007          73.42200       West Bank and Gaza
## 1669           1952          32.54800              Yemen, Rep.
## 1670           1957          33.97000              Yemen, Rep.
## 1671           1962          35.18000              Yemen, Rep.
## 1672           1967          36.98400              Yemen, Rep.
## 1673           1972          39.84800              Yemen, Rep.
## 1674           1977          44.17500              Yemen, Rep.
## 1675           1982          49.11300              Yemen, Rep.
## 1676           1987          52.92200              Yemen, Rep.
## 1677           1992          55.59900              Yemen, Rep.
## 1678           1997          58.02000              Yemen, Rep.
## 1679           2002          60.30800              Yemen, Rep.
## 1680           2007          62.69800              Yemen, Rep.
## 1681           1952          42.03800                   Zambia
## 1682           1957          44.07700                   Zambia
## 1683           1962          46.02300                   Zambia
## 1684           1967          47.76800                   Zambia
## 1685           1972          50.10700                   Zambia
## 1686           1977          51.38600                   Zambia
## 1687           1982          51.82100                   Zambia
## 1688           1987          50.82100                   Zambia
## 1689           1992          46.10000                   Zambia
## 1690           1997          40.23800                   Zambia
## 1691           2002          39.19300                   Zambia
## 1692           2007          42.38400                   Zambia
## 1693           1952          48.45100                 Zimbabwe
## 1694           1957          50.46900                 Zimbabwe
## 1695           1962          52.35800                 Zimbabwe
## 1696           1967          53.99500                 Zimbabwe
## 1697           1972          55.63500                 Zimbabwe
## 1698           1977          57.67400                 Zimbabwe
## 1699           1982          60.36300                 Zimbabwe
## 1700           1987          62.35100                 Zimbabwe
## 1701           1992          60.37700                 Zimbabwe
## 1702           1997          46.80900                 Zimbabwe
## 1703           2002          39.98900                 Zimbabwe
## 1704           2007          43.48700                 Zimbabwe
```

```r
select(gapminder, year, lifeExp, country) #select way
```

```
## # A tibble: 1,704 x 3
##     year lifeExp country    
##    <int>   <dbl> <fct>      
##  1  1952    28.8 Afghanistan
##  2  1957    30.3 Afghanistan
##  3  1962    32.0 Afghanistan
##  4  1967    34.0 Afghanistan
##  5  1972    36.1 Afghanistan
##  6  1977    38.4 Afghanistan
##  7  1982    39.9 Afghanistan
##  8  1987    40.8 Afghanistan
##  9  1992    41.7 Afghanistan
## 10  1997    41.8 Afghanistan
## # ... with 1,694 more rows
```

```r
#Select variables from country to lifeExp
select(gapminder, country:lifeExp)
```

```
## # A tibble: 1,704 x 4
##    country     continent  year lifeExp
##    <fct>       <fct>     <int>   <dbl>
##  1 Afghanistan Asia       1952    28.8
##  2 Afghanistan Asia       1957    30.3
##  3 Afghanistan Asia       1962    32.0
##  4 Afghanistan Asia       1967    34.0
##  5 Afghanistan Asia       1972    36.1
##  6 Afghanistan Asia       1977    38.4
##  7 Afghanistan Asia       1982    39.9
##  8 Afghanistan Asia       1987    40.8
##  9 Afghanistan Asia       1992    41.7
## 10 Afghanistan Asia       1997    41.8
## # ... with 1,694 more rows
```

```r
#Select all variables, except lifeExp
select(gapminder, -lifeExp)
```

```
## # A tibble: 1,704 x 5
##    country     continent  year      pop gdpPercap
##    <fct>       <fct>     <int>    <int>     <dbl>
##  1 Afghanistan Asia       1952  8425333      779.
##  2 Afghanistan Asia       1957  9240934      821.
##  3 Afghanistan Asia       1962 10267083      853.
##  4 Afghanistan Asia       1967 11537966      836.
##  5 Afghanistan Asia       1972 13079460      740.
##  6 Afghanistan Asia       1977 14880372      786.
##  7 Afghanistan Asia       1982 12881816      978.
##  8 Afghanistan Asia       1987 13867957      852.
##  9 Afghanistan Asia       1992 16317921      649.
## 10 Afghanistan Asia       1997 22227415      635.
## # ... with 1,694 more rows
```

```r
#Put continent first, use everything()
select(gapminder, continent, everything()) #everything() includes continent but removes the redundancy
```

```
## # A tibble: 1,704 x 6
##    continent country      year lifeExp      pop gdpPercap
##    <fct>     <fct>       <int>   <dbl>    <int>     <dbl>
##  1 Asia      Afghanistan  1952    28.8  8425333      779.
##  2 Asia      Afghanistan  1957    30.3  9240934      821.
##  3 Asia      Afghanistan  1962    32.0 10267083      853.
##  4 Asia      Afghanistan  1967    34.0 11537966      836.
##  5 Asia      Afghanistan  1972    36.1 13079460      740.
##  6 Asia      Afghanistan  1977    38.4 14880372      786.
##  7 Asia      Afghanistan  1982    39.9 12881816      978.
##  8 Asia      Afghanistan  1987    40.8 13867957      852.
##  9 Asia      Afghanistan  1992    41.7 16317921      649.
## 10 Asia      Afghanistan  1997    41.8 22227415      635.
## # ... with 1,694 more rows
```

```r
#Rename continent to cont
rename(gapminder,cont=continent)
```

```
## # A tibble: 1,704 x 6
##    country     cont   year lifeExp      pop gdpPercap
##    <fct>       <fct> <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan Asia   1952    28.8  8425333      779.
##  2 Afghanistan Asia   1957    30.3  9240934      821.
##  3 Afghanistan Asia   1962    32.0 10267083      853.
##  4 Afghanistan Asia   1967    34.0 11537966      836.
##  5 Afghanistan Asia   1972    36.1 13079460      740.
##  6 Afghanistan Asia   1977    38.4 14880372      786.
##  7 Afghanistan Asia   1982    39.9 12881816      978.
##  8 Afghanistan Asia   1987    40.8 13867957      852.
##  9 Afghanistan Asia   1992    41.7 16317921      649.
## 10 Afghanistan Asia   1997    41.8 22227415      635.
## # ... with 1,694 more rows
```


## `arrange()`

1. Order by year.

2. Order by year, in descending order.

3. Order by year, then by life expectancy.


```r
#Order by year
arrange(gapminder, year) #automatically by increasing order
```

```
## # A tibble: 1,704 x 6
##    country     continent  year lifeExp      pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan Asia       1952    28.8  8425333      779.
##  2 Albania     Europe     1952    55.2  1282697     1601.
##  3 Algeria     Africa     1952    43.1  9279525     2449.
##  4 Angola      Africa     1952    30.0  4232095     3521.
##  5 Argentina   Americas   1952    62.5 17876956     5911.
##  6 Australia   Oceania    1952    69.1  8691212    10040.
##  7 Austria     Europe     1952    66.8  6927772     6137.
##  8 Bahrain     Asia       1952    50.9   120447     9867.
##  9 Bangladesh  Asia       1952    37.5 46886859      684.
## 10 Belgium     Europe     1952    68    8730405     8343.
## # ... with 1,694 more rows
```

```r
#Order by year, in descending order
arrange(gapminder, desc(year))
```

```
## # A tibble: 1,704 x 6
##    country     continent  year lifeExp       pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>     <int>     <dbl>
##  1 Afghanistan Asia       2007    43.8  31889923      975.
##  2 Albania     Europe     2007    76.4   3600523     5937.
##  3 Algeria     Africa     2007    72.3  33333216     6223.
##  4 Angola      Africa     2007    42.7  12420476     4797.
##  5 Argentina   Americas   2007    75.3  40301927    12779.
##  6 Australia   Oceania    2007    81.2  20434176    34435.
##  7 Austria     Europe     2007    79.8   8199783    36126.
##  8 Bahrain     Asia       2007    75.6    708573    29796.
##  9 Bangladesh  Asia       2007    64.1 150448339     1391.
## 10 Belgium     Europe     2007    79.4  10392226    33693.
## # ... with 1,694 more rows
```

```r
#Order by year, then by lifeExp
arrange(gapminder, year, lifeExp)
```

```
## # A tibble: 1,704 x 6
##    country       continent  year lifeExp     pop gdpPercap
##    <fct>         <fct>     <int>   <dbl>   <int>     <dbl>
##  1 Afghanistan   Asia       1952    28.8 8425333      779.
##  2 Gambia        Africa     1952    30    284320      485.
##  3 Angola        Africa     1952    30.0 4232095     3521.
##  4 Sierra Leone  Africa     1952    30.3 2143249      880.
##  5 Mozambique    Africa     1952    31.3 6446316      469.
##  6 Burkina Faso  Africa     1952    32.0 4469979      543.
##  7 Guinea-Bissau Africa     1952    32.5  580653      300.
##  8 Yemen, Rep.   Asia       1952    32.5 4963829      782.
##  9 Somalia       Africa     1952    33.0 2526994     1136.
## 10 Guinea        Africa     1952    33.6 2664249      510.
## # ... with 1,694 more rows
```


## Piping, `%>%`

Note: think of `%>%` as the word "then"!

1. Combine `select()` Task 1 with `arrange()` Task 3.


```r
select(gapminder, year, lifeExp, country) %>% 
  arrange(year, lifeExp)
```

```
## # A tibble: 1,704 x 3
##     year lifeExp country      
##    <int>   <dbl> <fct>        
##  1  1952    28.8 Afghanistan  
##  2  1952    30   Gambia       
##  3  1952    30.0 Angola       
##  4  1952    30.3 Sierra Leone 
##  5  1952    31.3 Mozambique   
##  6  1952    32.0 Burkina Faso 
##  7  1952    32.5 Guinea-Bissau
##  8  1952    32.5 Yemen, Rep.  
##  9  1952    33.0 Somalia      
## 10  1952    33.6 Guinea       
## # ... with 1,694 more rows
```

```r
#Or

gapminder %>% 
  select(year, lifeExp, country) %>% 
  arrange(year, lifeExp)
```

```
## # A tibble: 1,704 x 3
##     year lifeExp country      
##    <int>   <dbl> <fct>        
##  1  1952    28.8 Afghanistan  
##  2  1952    30   Gambia       
##  3  1952    30.0 Angola       
##  4  1952    30.3 Sierra Leone 
##  5  1952    31.3 Mozambique   
##  6  1952    32.0 Burkina Faso 
##  7  1952    32.5 Guinea-Bissau
##  8  1952    32.5 Yemen, Rep.  
##  9  1952    33.0 Somalia      
## 10  1952    33.6 Guinea       
## # ... with 1,694 more rows
```

```r
## When you pipe, it takes the output and automatically puts it as 
## the first argument (usually where the data goes)
## To override this, use . to specify where the output goes
## ex. gapminder %>% 
##        data.frame(3,.) 
## will create a data frame with 3 first, then gapminder
```


## `filter()`

1. Only take data with population greater than 100 million.

2. Of those, only take data from Asia.


```r
# Pop. > 100 million
filter(gapminder, pop > 100000000)
```

```
## # A tibble: 77 x 6
##    country    continent  year lifeExp       pop gdpPercap
##    <fct>      <fct>     <int>   <dbl>     <int>     <dbl>
##  1 Bangladesh Asia       1987    52.8 103764241      752.
##  2 Bangladesh Asia       1992    56.0 113704579      838.
##  3 Bangladesh Asia       1997    59.4 123315288      973.
##  4 Bangladesh Asia       2002    62.0 135656790     1136.
##  5 Bangladesh Asia       2007    64.1 150448339     1391.
##  6 Brazil     Americas   1972    59.5 100840058     4986.
##  7 Brazil     Americas   1977    61.5 114313951     6660.
##  8 Brazil     Americas   1982    63.3 128962939     7031.
##  9 Brazil     Americas   1987    65.2 142938076     7807.
## 10 Brazil     Americas   1992    67.1 155975974     6950.
## # ... with 67 more rows
```

```r
# Pop. > 100 million and from Asia
filter(gapminder,pop > 100000000, continent == 'Asia')
```

```
## # A tibble: 52 x 6
##    country    continent  year lifeExp       pop gdpPercap
##    <fct>      <fct>     <int>   <dbl>     <int>     <dbl>
##  1 Bangladesh Asia       1987    52.8 103764241      752.
##  2 Bangladesh Asia       1992    56.0 113704579      838.
##  3 Bangladesh Asia       1997    59.4 123315288      973.
##  4 Bangladesh Asia       2002    62.0 135656790     1136.
##  5 Bangladesh Asia       2007    64.1 150448339     1391.
##  6 China      Asia       1952    44   556263527      400.
##  7 China      Asia       1957    50.5 637408000      576.
##  8 China      Asia       1962    44.5 665770000      488.
##  9 China      Asia       1967    58.4 754550000      613.
## 10 China      Asia       1972    63.1 862030000      677.
## # ... with 42 more rows
```


## git stuff (Optional)

Knit, commit, push!

# Break/Challenge: metaprogramming

Here's an activity for you to do during the break, in case you're all caught up. It should help you understand metaprogramming a bit more.

Suppose you're the instructor of an R programming course. You write an assignment question to evaluate whether students can write an `if` statement, for which an answer to the question looks something like this:

```
my_commute <- 60
if (my_commute > 30) {
    print("That's a long commute!")
} else {
    print("That's a short commute.")
}
```

Your task is to use metaprogramming to check whether a response (like the one above) works and contains an `if` statement. You should roughly follow these steps, using [adv-r: expressions](https://adv-r.hadley.nz/expressions.html) as a resource (especially Section 18.1).

1. Wrap the above block of code in the `expr()` function from the `rlang` package.
2. Use the `eval()` function to execute the code, to see if the code runs.
3. Use the `as.character()` function to check whether this response contains an `if` statement.

# Relational/Comparison and Logical Operators in R

1. Find all entries of Canada and Algeria occuring in the '60s. 

2. Find all entries of Canada, and entries of Algeria occuring in the '60s. 
3. Find all entries _not_ including Canada and Algeria.


```r
# Canada and Algeria during the 60's
filter(gapminder, (country == 'Canada' | country == 'Algeria') & year >= 1960 & year < 1970)
```

```
## # A tibble: 4 x 6
##   country continent  year lifeExp      pop gdpPercap
##   <fct>   <fct>     <int>   <dbl>    <int>     <dbl>
## 1 Algeria Africa     1962    48.3 11000948     2551.
## 2 Algeria Africa     1967    51.4 12760499     3247.
## 3 Canada  Americas   1962    71.3 18985849    13462.
## 4 Canada  Americas   1967    72.1 20819767    16077.
```

```r
 #Or 
gapminder %>% 
  filter(country %in% c('Canada', 'Algeria'), 
         year >= 1960, 
         year < 1970)
```

```
## # A tibble: 4 x 6
##   country continent  year lifeExp      pop gdpPercap
##   <fct>   <fct>     <int>   <dbl>    <int>     <dbl>
## 1 Algeria Africa     1962    48.3 11000948     2551.
## 2 Algeria Africa     1967    51.4 12760499     3247.
## 3 Canada  Americas   1962    71.3 18985849    13462.
## 4 Canada  Americas   1967    72.1 20819767    16077.
```

```r
# %in% goes through all countries and determines whether its in the vector
# , == & in filter()
```


# Bonus Exercises

If there's time remaining, we'll practice with these three exercises. I'll give you 1 minute for each, then we'll go over the answer.

1. Take all countries in Europe that have a GDP per capita greater than 10000, and select all variables except `gdpPercap`. (Hint: use `-`).

2. Take the first three columns, and extract the names.

3. Of the `iris` data frame, take all columns that start with the word "Petal". 
    - Hint: take a look at the "Select helpers" documentation by running the following code: `?tidyselect::select_helpers`.
    - Exercise from [r-exercises](https://www.r-exercises.com/2017/10/19/dplyr-basic-functions-exercises/).
