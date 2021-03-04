Maptools Tutorial
================
Miguel Angelo
04/03/2021

## Pacote Maptools

É um pacote que possui um conjunto de ferramentas que manipula dados
geográficos. Funções para leitura, exportação e manipulação de
estruturas espaciais.

## Funções que serão apresentadas no tutorial:

readShapePoints: O readShapePoints lê dados de um arquivo de forma de
pontos em um objeto SpatialPointsDataFrame.

``` r
maptools::readShapePoints
```

readShapePoly: O readShapePoly lê dados de um shapefile de polígono em
um objeto SpatialPolygonsDataFrame.

``` r
maptools::readShapePoly
```

## Exemplo

Mapa onde mostra locais onde se encontra a Limodorum abortivum(planta)
no Tirol do Norte (Estado da Áustria)

Para fazer com que o mapa seja gerado é necessário baixar arquivos com
dados geográficos, nesse caso os arquivos a serem baixados estão aqui:
<https://drive.google.com/file/d/0B2wAunwURQNsNDkxM2NhMDctODJlYi00MzEzLWJlZmEtMDUxNGFmNGY0MzZk/view>

Depois deve instalar o pacote maptools:

``` r
install.packages("maptools")
```

Em seguida dar carregar o pacote:

``` r
library(maptools)
```

Colocar o diretório de onde está as pastas dos arquivos baixados e
selecionar os arquivos correspondentes:

``` r
setwd("E:/R/Data/Maps/Example.1_Data")
Limodorum.shp <- readShapePoints(file.choose())
TIRIS.BEZIDX_PL.shp <- readShapePoly(file.choose())
```

Examinar pontos:

``` r
summary(Limodorum.shp)
attributes(Limodorum.shp@data)
```

Examinar polígonos:

``` r
summary(TIRIS.BEZIDX_PL.shp)
attributes(TIRIS.BEZIDX_PL.shp@data)
```

Colocar os limites:

``` r
xlim <- TIRIS.BEZIDX_PL.shp@bbox[1, ]
ylim <- TIRIS.BEZIDX_PL.shp@bbox[2, ] 
```

E colocar o output:

``` r
par(mai = rep(.1, 4))

plot(TIRIS.BEZIDX_PL.shp, col = "grey93", axes = F,
     xlim = xlim, ylim = ylim, bty = "n")
points(Limodorum.shp, pch = 16,
       col = 2, cex = .5)
mtext("Limodorum abortivum", 3, line = -7,
      at = -17000, adj = 0, cex = 2, font = 3)
legend("bottomleft", inset = c(0.4, 0.2),
       legend = c("Fundpunkte", "Polit. Bezirke"),
       bty = "n", pch = c(16,-1),           # bty = "n": no box
       col = c(2, 1), pt.cex = c(.5, 1),
       lty = c(-1, 1))
```
