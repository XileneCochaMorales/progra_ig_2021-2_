Tarea nº5
================
Xilene Cocha Morales
30/1/2022

### Nivel I

1.Generar un diagrama de Walter y Lieth con la data de datcli, este debe
llevar de título “Estación Campo de Marte”, a una altitud de 80 msnm
durante el año 2017, con los meses simbolizados por números. Las
temperaturas deberán visualizarse de color verde; las precipitaciones,
en naranja; los meses de congelación segura, en azul y los de
congelación probable, en celeste. No trazar una línea suplementaria de
precipitación.

``` r
data(datcli)
#Función diagwl
diagwl(datcli,"Estación Campo de Marte",80,"2017",mlab = "Other",pcol = "orange",tcol ="green",pfcol = "light blue",sfcol = "blue",shem = FALSE,p3line = FALSE)
```

![](Tarea-nº5_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

2.Recrea minuciosamente el siguiente diagrama de la rosa de los vientos
(pista: col=rainbow(8)).

``` r
data(windfr)
#Función rosavent()
rosavent(windfr,fnum=6,fint = 2,flab = 1,ang = 3*pi/8,col=rainbow(8),uni = "km/s")
```

![](Tarea-nº5_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

### Nivel II

3.  Convertir la data diaria de tmax en una data de medias mensuales.
    Posteriormente, homogeneizar dichos datos mensuales con una
    normalización por estandarización y gráficos de medias anuales y
    correcciones aplicadas en el análisis exploratorio de datos
    (utilizar dos decimales).

``` r
data(tmax)
##Función dd2m()
#a.Exportamos archivos del database de R a nuestro equipo:
write.table(dat,"Tmax_2001-2003.dat",row.names = F,col.names = F)
write.table(est.c,"Tmax_2001-2003.est",row.names = F,col.names = F)
#b. Convertimos el database (.dat) diario a mensual:
dd2m("Tmax",2001,2003,ndec = 2,valm = 2)
```

    ##   1  2  3
    ## 
    ## Monthly mean values saved to file Tmax-m_2001-2003.dat 
    ##   (Months with more than 10 missing original daily data
    ##   have also been set to missing)

``` r
Tmax_m <- read.table("Tmax_2001-2003.dat",header=FALSE)
##homogen()
#Homogenizamos una serie climatológica de temperaturas mensuales:
homogen("Tmax",2001,2003,std = 3,ndec=2,gp=3,expl=TRUE)
```

    ## 
    ## HOMOGEN() APPLICATION OUTPUT  (From R's contributed package 'climatol' 3.1.1)
    ## 
    ## =========== Homogenization of Tmax, 2001-2003. (Sun Jan 30 23:25:42 2022)
    ## 
    ## Parameters: varcli=Tmax anyi=2001 anyf=2003 suf=NA nm=NA nref=10,10,4 std=3 swa=NA ndec=2 dz.max=5 dz.min=-5 wd=0,0,100 snht1=0 snht2=0 tol=0.02 maxdif=0.005 mxdif=0.005 maxite=999 force=FALSE wz=0.001 trf=0 mndat=NA gp=3 ini=NA na.strings=NA vmin=NA vmax=NA nclust=100 cutlev=NA grdcol=#666666 mapcol=#666666 hires=TRUE expl=TRUE metad=FALSE sufbrk=m tinc=NA tz=UTC cex=1.2 verb=TRUE
    ## 
    ## Data matrix: 1095 data x 3 stations

    ## Computing inter-station distances:  1  2
    ## 
    ## 
    ## ========== STAGE 3 (Final computation of all missing data) ==========
    ## 
    ## Computing inter-station weights... (done)

    ## Computation of missing data with outlier removal
    ## (Suggested data replacements are provisional)
    ## 
    ## The following lines will have one of these formats:
    ##   Station(rank) Date: Observed -> Suggested (Anomaly, in std. devs.)
    ##   Iteration Max.data.difference (Station_code)
    ## 2 -0.1884 (S01)
    ## 3 -0.0407 (S01)
    ## 4 -0.0088 (S01)
    ## 5 -0.0019 (S01)
    ## 
    ## Last series readjustment (please, be patient...)

    ## 
    ## ======== End of the missing data filling process, after 0.95 secs 
    ## 
    ## ----------- Final computations:
    ## 
    ## ACmx: Station maximum absolute autocorrelations of anomalies
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##  0.4900  0.5050  0.5200  0.5167  0.5300  0.5400 
    ## 
    ## SNHT: Standard normal homogeneity test (on anomaly series)
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   16.30   26.95   37.60   42.57   55.70   73.80 
    ## 
    ## RMSE: Root mean squared error of the estimated data
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   3.544   3.642   3.739   3.699   3.776   3.814 
    ## 
    ## POD: Percentage of original data
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   81.00   84.50   88.00   87.33   90.50   93.00 
    ## 
    ##   ACmx SNHT RMSE POD Code Name     
    ## 1 0.54 73.8 3.5  81  S01  La Vall  
    ## 2 0.52 37.6 3.7  88  S02  Lucent   
    ## 3 0.49 16.3 3.8  93  S03  Sunflower

    ## 
    ## ----------- Generated output files: -------------------------
    ## 
    ## Tmax_2001-2003.txt :  This text output 
    ## Tmax_2001-2003_out.csv :  List of corrected outliers 
    ## Tmax_2001-2003_brk.csv :  List of corrected breaks 
    ## Tmax_2001-2003.pdf :  Diagnostic graphics 
    ## Tmax_2001-2003.rda :  Homogenization results. Postprocess with (examples):
    ##    dahstat('Tmax',2001,2003) #get averages in file Tmax_2001-2003-me.csv 
    ##    dahstat('Tmax',2001,2003,stat='tnd') #get OLS trends and their p-values 
    ##    dahgrid('Tmax',2001,2003,grid=YOURGRID) #get homogenized grids 
    ##    ... (See other options in the package documentation)

4.  Recortar la data mensual de Ptest desde 1965 hasta 2005.
    Homogeneizar dicha data mediante clústers o áreas rectangulares, con
    un ancho de superposición de 0, mediante una estandarización y con
    gráficos de totales anuales en el análisis exploratorio de datos.
    Mostrar las medias de las series homogeneizadas en un archivo Excel
    que, además, mencione los totales anuales y los datos de la latitud,
    longitud y nombre de cada estación (utilizar dos decimales).

``` r
data(Ptest)
#Función datsubset
#Exportamos archivos del database de R nuestro equipo:
write.table(dat,"Ptest_1951-2010.dat",row.names = F,col.names = F)
write.table(est.c,"Ptest_1951-2010.est",row.names = F,col.names = F)
#Recortamos el database (.dat)de 1951-2010 a 1965-2005:
datsubset("Ptest",1951,2010,1965,2005,1)
```

    ## Subset data written to files Ptest_1965-2005.dat and Ptest_1965-2005.est

``` r
read.table("Ptest_1965-2005.dat")
```

    ##        V1    V2    V3    V4    V5    V6     V7    V8    V9   V10   V11   V12
    ## 1    27.1    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA    NA
    ## 2    17.1  50.8  92.8  16.3  72.5  13.2  134.5  62.4  98.8    NA    NA    NA
    ## 3      NA    NA    NA    NA    NA    NA     NA    NA  32.4 112.5  64.7  17.5
    ## 4    75.0  47.2 125.2  33.1 111.2    NA     NA    NA    NA    NA    NA    NA
    ## 5      NA    NA    NA    NA  55.8 190.6  122.3  87.0 138.3  82.1 759.1  45.1
    ## 6    69.4    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA    NA
    ## 7    11.4  82.8  98.9  28.7  51.1  68.7  177.9  26.7  40.6    NA    NA    NA
    ## 8      NA    NA    NA    NA    NA    NA     NA    NA  33.3  98.0  81.3  35.5
    ## 9    56.3  61.6 473.8  50.0  45.5    NA     NA    NA    NA    NA    NA    NA
    ## 10     NA    NA    NA    NA  22.4  41.3   21.1  16.4  30.2  27.8  36.2  21.3
    ## 11   20.6    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA    NA
    ## 12   11.0  12.7  19.7  33.0  13.2  19.1   50.9  12.0  36.4    NA    NA    NA
    ## 13     NA    NA    NA    NA    NA    NA     NA    NA   3.5   0.4   1.6   0.6
    ## 14    0.8   0.7   1.0   2.0   4.3    NA     NA    NA    NA    NA    NA    NA
    ## 15     NA    NA    NA    NA   0.0   8.6     NA   0.0   0.9   1.6   0.5   0.0
    ## 16    0.0    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA    NA
    ## 17    0.1   0.0   0.0   0.0   2.3   7.1   13.7   1.1   0.0    NA    NA    NA
    ## 18     NA    NA    NA    NA    NA    NA     NA    NA   0.6   0.0   0.0   0.0
    ## 19    0.0   0.0   0.0   4.3  18.3    NA     NA    NA    NA    NA    NA    NA
    ## 20     NA    NA    NA    NA  30.7   6.7    4.6   1.7  11.3  11.7  81.3   0.0
    ## 21    4.0    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA    NA
    ## 22  121.3 240.2 268.2 139.6 258.0 159.6  589.8 108.8 257.7    NA    NA    NA
    ## 23     NA    NA    NA    NA    NA    NA     NA    NA 157.5 202.4 171.5  58.7
    ## 24  166.5 151.4 356.7  80.4 178.8    NA     NA    NA    NA    NA    NA    NA
    ## 25     NA    NA    NA    NA   8.4  29.9   19.8  30.9  12.0  22.8 153.2  17.7
    ## 26   16.1    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA    NA
    ## 27    6.4  21.2  18.1  17.1  33.8  57.6  172.3   1.3   6.0    NA    NA    NA
    ## 28     NA    NA    NA    NA    NA    NA     NA    NA  19.6  88.1  53.5  32.8
    ## 29   39.2  44.8  85.6  68.5  27.4    NA     NA    NA    NA    NA    NA    NA
    ## 30     NA    NA    NA    NA  22.0   8.8   12.4   2.8   4.9   9.9 100.3   8.1
    ## 31   13.0    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA    NA
    ## 32    4.5  32.7  32.0  46.3  24.6  15.5   32.1   5.1  10.3    NA    NA    NA
    ## 33     NA    NA    NA    NA    NA    NA     NA    NA   0.0   0.0   2.3   0.4
    ## 34    0.4   0.3   1.3   2.7   5.5    NA     NA    NA    NA    NA    NA    NA
    ## 35     NA    NA    NA    NA   0.0    NA    0.0   0.0   0.0   0.0   0.0   0.0
    ## 36    0.0    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA    NA
    ## 37    2.1   0.0   0.0   0.0   0.0   0.0   38.6   0.0   0.0    NA    NA    NA
    ## 38     NA    NA    NA    NA    NA    NA     NA    NA  29.3  70.5 113.8  82.1
    ## 39   22.8  55.3 172.8  81.1   3.2    NA     NA    NA    NA    NA    NA    NA
    ## 40     NA    NA    NA    NA    NA  93.0   57.9  83.9    NA  91.4 151.8  47.4
    ## 41   63.9    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA 146.4
    ## 42  300.3    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA 166.4
    ## 43  183.5 553.9 696.9 359.0 670.5 472.2  818.9 334.4 377.3    NA    NA    NA
    ## 44     NA    NA    NA    NA    NA    NA     NA 304.4  24.9  79.1  38.2  15.7
    ## 45   16.7  41.4  63.8  40.8  39.7    NA     NA    NA    NA    NA    NA    NA
    ## 46     NA    NA    NA  27.1  73.3 110.6   98.0  68.7  85.7  45.9 288.5  57.2
    ## 47   63.1    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA  89.1
    ## 48   42.9  55.6  65.2  18.7  40.2  58.5  121.5  21.7  54.6    NA    NA    NA
    ## 49     NA    NA    NA    NA    NA    NA     NA  64.6   2.6  21.7   8.8   1.3
    ## 50    8.8  17.3 127.8  12.3  10.7    NA     NA    NA    NA    NA    NA    NA
    ## 51     NA    NA    NA  31.2 109.0  61.3   56.8  38.8  57.6 107.3 437.7  44.3
    ## 52   88.5    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA  72.4
    ## 53    8.1  42.8  63.3  35.6  45.2  31.3   43.1   8.0   6.4    NA    NA    NA
    ## 54     NA    NA    NA    NA    NA    NA     NA  64.0   7.9   1.3   1.5   6.9
    ## 55    8.5   4.8  10.5   4.1   4.8    NA     NA    NA    NA    NA    NA    NA
    ## 56     NA    NA    NA  13.1   0.0   0.0    0.3   0.0   0.0   4.5   1.1   0.5
    ## 57    0.0    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA   0.0
    ## 58    5.0   0.0  22.4  35.2   0.0   0.0    0.0   0.0   0.0    NA    NA    NA
    ## 59     NA    NA    NA    NA    NA    NA     NA  13.3   0.0   0.0  41.1  65.7
    ## 60    5.5   0.0   1.3  16.8   0.0    NA     NA    NA    NA    NA    NA    NA
    ## 61     NA    NA    NA   6.7  82.2  65.8   41.1  55.4  71.2  69.2 147.8  63.5
    ## 62   42.8    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA 101.8
    ## 63   21.3 141.0 228.5  63.2 113.7  40.3  216.5 145.7 128.0    NA    NA    NA
    ## 64     NA    NA    NA    NA    NA    NA     NA  88.7  59.8 139.2 152.5  21.6
    ## 65  113.2 100.7 414.8  58.8 156.8    NA     NA    NA    NA    NA    NA    NA
    ## 66     NA    NA    NA  81.1 102.7  88.0   74.8 113.5  71.0  28.5 325.8  34.6
    ## 67   53.0    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA 127.3
    ## 68   20.7  11.2  11.3  16.6  10.6  42.6   96.9   0.7   8.7    NA    NA    NA
    ## 69     NA    NA    NA    NA    NA    NA     NA  20.9  21.0  47.1  51.1  30.8
    ## 70   50.8  52.3 181.5  51.4  59.4    NA     NA    NA    NA    NA    NA    NA
    ## 71     NA    NA    NA  65.5  56.9  81.7   27.3  40.3  69.3  53.8 209.4  28.6
    ## 72   46.7    NA    NA    NA    NA    NA     NA    NA    NA    NA    NA  62.0
    ## 73   13.3  59.5  90.9  55.3  42.8  38.8   74.6   7.0  17.7    NA    NA    NA
    ## 74     NA    NA    NA    NA    NA    NA     NA  68.1  26.4   3.6  26.6  22.2
    ## 75   10.1  16.2  29.3  30.1  26.0    NA     NA    NA    NA    NA    NA    NA
    ## 76     NA    NA    NA  38.1   8.3  12.7    4.1  13.8  15.0  12.4  22.0  20.6
    ## 77   25.3    NA    NA    NA    NA    NA     NA    NA    NA   3.0    NA   7.2
    ## 78   34.8   3.6  25.7  21.6  38.9  63.0  159.2  10.7    NA    NA    NA    NA
    ## 79     NA    NA    NA    NA    NA  18.2     NA  20.7  12.1  50.9 110.4 111.6
    ## 80   28.4    NA  69.1  14.6  18.4    NA     NA    NA    NA    NA    NA    NA
    ## 81     NA 110.6    NA  51.2   9.4   9.4   17.2  13.0   7.6  16.1  61.9  16.9
    ## 82    0.0    NA    NA    NA    NA    NA     NA    NA    NA  40.5    NA  16.0
    ## 83   38.7    NA    NA    NA    NA    NA     NA    NA    NA 167.9    NA  72.2
    ## 84   34.4  65.9  31.7  37.5 111.8  44.7  126.0  60.5  28.3    NA    NA    NA
    ## 85     NA    NA    NA    NA    NA  41.5     NA  88.6  41.8 130.2  83.3  40.1
    ## 86   65.0 108.4 236.7  46.7  25.1    NA     NA    NA    NA    NA    NA    NA
    ## 87     NA  85.1    NA 101.6  41.6  57.1   39.7  39.9  52.6  47.2 180.1  28.2
    ## 88   40.5    NA    NA    NA    NA    NA     NA    NA    NA  83.0    NA  49.2
    ## 89   23.1  42.1  50.2  25.0  22.4  48.7  148.6  18.9  58.9    NA    NA    NA
    ## 90     NA    NA    NA    NA    NA  34.9     NA  41.2   6.6  32.3  30.5   6.2
    ## 91    9.9  18.4  95.3  36.2  11.8    NA     NA    NA    NA    NA    NA    NA
    ## 92     NA  10.2    NA  10.3   7.0  30.2    9.2   5.7  11.3  17.3  46.3   7.7
    ## 93   42.1    NA    NA    NA    NA    NA     NA    NA    NA   6.2    NA   6.9
    ## 94   19.0  94.0 101.0  36.8  60.4    NA  129.1  22.0  58.4    NA    NA    NA
    ## 95     NA    NA    NA    NA    NA 127.0     NA  47.3   4.4   6.9   9.5  16.3
    ## 96   23.5  11.1   6.5  20.9  27.5    NA     NA    NA    NA    NA    NA    NA
    ## 97     NA   3.2    NA  33.9   0.3   0.9    2.9   0.0   0.0   5.4   8.8   1.8
    ## 98    0.3    NA    NA    NA    NA    NA     NA    NA    NA   3.2    NA   1.3
    ## 99   59.2   0.0  10.5   1.7  21.2   0.0    0.0   0.0   0.0    NA    NA    NA
    ## 100    NA    NA    NA    NA    NA   0.0     NA   0.0   7.0 132.1 128.0  82.3
    ## 101  41.5    NA  16.9  44.9   0.0    NA     NA    NA    NA    NA    NA    NA
    ## 102    NA 114.7    NA  73.4   0.0   2.2   10.2  40.3  15.4  19.2  48.2  16.3
    ## 103   2.6    NA    NA    NA    NA    NA     NA    NA    NA  10.3    NA  18.4
    ## 104  32.9 132.1 128.8  41.2  62.7  82.6  188.6  74.9    NA    NA    NA    NA
    ## 105    NA    NA    NA    NA    NA  70.6     NA  69.8 149.2 183.0 156.7  86.4
    ## 106 167.8 228.6 528.7 138.8 194.8    NA     NA    NA    NA    NA    NA    NA
    ## 107    NA 181.2    NA 128.1  29.4  66.1   29.5  49.0  40.6  31.2 340.9  44.0
    ## 108  67.7    NA    NA    NA    NA    NA     NA    NA    NA  62.3    NA  42.5
    ## 109  46.2  26.8  21.9  28.7  20.5  68.8  231.1  22.7  57.3    NA    NA    NA
    ## 110    NA    NA    NA    NA    NA  24.6     NA  37.8  29.9  70.8  38.3  13.3
    ## 111  44.1  50.0 194.5  41.0  12.2    NA     NA    NA    NA    NA    NA    NA
    ## 112    NA  56.3    NA  88.8  11.9   7.1    3.8   0.0   7.4   5.7   7.1   0.0
    ## 113   0.0    NA    NA    NA    NA    NA     NA    NA    NA   0.0    NA   9.6
    ## 114  11.8   7.4  33.2    NA   6.5  13.9    9.7   4.6   4.8    NA    NA    NA
    ## 115    NA    NA    NA    NA    NA  14.4     NA   5.9  11.2   3.4   8.3   3.5
    ## 116   5.9  14.4  20.8   9.4  21.0    NA     NA    NA    NA    NA    NA    NA
    ## 117    NA   6.9    NA  10.1   0.0   0.0    0.0   0.0   0.0   0.3   0.0   0.0
    ## 118   5.1    NA    NA    NA    NA    NA     NA    NA    NA   0.0    NA   0.0
    ## 119 104.1  50.7  65.2    NA  72.6  39.4   78.9  15.1 129.8    NA    NA    NA
    ## 120    NA    NA    NA    NA    NA  50.7     NA  62.2  39.9  84.5  71.6  49.2
    ## 121  10.7  27.0  61.8  34.4  23.3    NA     NA    NA    NA    NA    NA    NA
    ## 122    NA 107.9    NA  51.8  97.8  87.6   35.3  72.7  88.1  58.5  57.0  29.8
    ## 123  59.0    NA    NA    NA    NA    NA     NA    NA    NA  28.6    NA  39.0
    ## 124  17.1    NA    NA    NA    NA    NA     NA  16.4    NA  20.5    NA  11.6
    ## 125 341.9 272.9 411.3 157.6 361.8 238.7  492.1 210.7 195.1    NA    NA    NA
    ## 126    NA    NA    NA  66.4    NA 197.3     NA 182.1 196.5 203.7 242.1  68.4
    ## 127 197.9 110.9 301.1 141.4 239.0    NA     NA    NA    NA    NA    NA 145.9
    ## 128    NA 208.0    NA 143.2  25.9  18.1   15.8  19.3  21.8  20.5 101.1  21.4
    ## 129  47.4    NA    NA    NA    NA    NA     NA   5.0    NA  25.3    NA  34.3
    ## 130 145.2 127.1 207.1  77.8 150.3 122.5  445.9  78.0 179.5    NA    NA    NA
    ## 131    NA    NA    NA 111.4    NA 121.1     NA 190.8  42.0  75.5  30.1  27.7
    ## 132  30.1  65.9 217.0  40.2  33.3    NA     NA    NA    NA    NA    NA  29.6
    ## 133    NA  38.9    NA  72.7  90.1  71.8   60.4  52.6 180.9  78.4 270.4  60.1
    ## 134 155.0    NA    NA    NA    NA    NA     NA  49.9    NA 164.4    NA  70.2
    ## 135   1.7  10.1  25.9  10.3   1.8   9.1    6.4   2.3   0.0    NA    NA    NA
    ## 136    NA    NA    NA   1.9    NA   6.0     NA   4.7   1.3   0.0   0.0   0.9
    ## 137   0.4   0.8   2.0   0.0   0.2    NA     NA    NA    NA    NA    NA   0.0
    ## 138    NA   0.0    NA   0.1  43.4  16.4   20.3  28.3  22.4  42.3  95.1  57.7
    ## 139    NA    NA    NA    NA    NA    NA     NA  17.8    NA  30.8    NA   9.7
    ## 140   6.5   0.0   0.0   0.0   0.0   0.0    0.0   0.0   0.0    NA    NA    NA
    ## 141    NA    NA    NA   0.2    NA   0.0     NA   0.6  40.5 142.6 120.7 143.0
    ## 142  32.0  83.1 114.5  39.5  48.7    NA     NA    NA    NA    NA    NA 147.3
    ## 143    NA 119.7    NA  76.6 171.5 103.9  114.1  26.3  82.6  62.1  91.7 222.1
    ## 144 166.5    NA    NA    NA    NA    NA     NA  73.4    NA 113.8    NA  98.8
    ## 145  35.8  76.1 155.4  14.5 106.3  31.4  163.8  59.0  34.3    NA    NA    NA
    ## 146    NA    NA    NA  32.6    NA  74.1     NA  81.5  31.0  40.3  36.9  13.4
    ## 147  18.4  41.2  28.3  22.1  12.5    NA     NA    NA    NA    NA    NA  34.3
    ## 148    NA  44.7    NA  13.9  57.9 117.5   65.2  87.0  58.3  41.5 194.8  52.5
    ## 149  33.2    NA    NA    NA    NA    NA     NA  51.3    NA  75.0    NA  80.4
    ## 150 134.9 108.0 124.4  98.4 101.7 154.0  818.8 120.5 186.0    NA    NA    NA
    ## 151    NA    NA    NA 101.2    NA 113.9     NA  81.1  87.3  78.1  77.6  48.7
    ## 152  75.7  84.8 316.5  58.5    NA    NA     NA    NA    NA    NA    NA  55.8
    ## 153    NA  97.5    NA 117.5  92.2   8.3   13.0  14.4  26.5  19.1  32.9  20.9
    ## 154  34.7    NA    NA    NA    NA    NA     NA  19.9    NA   8.4    NA  19.5
    ## 155   0.0  11.0  14.9   7.7   2.7   6.0   17.9   1.3   0.0    NA    NA    NA
    ## 156    NA    NA    NA   6.5    NA   5.5     NA   6.1  37.0   9.8  26.5   1.3
    ## 157  15.4   9.1  28.5  16.8  20.1    NA     NA    NA    NA    NA    NA  11.8
    ## 158    NA   5.8    NA  12.6   7.9  20.4    8.9  44.8   6.2   2.7   5.7   9.0
    ## 159  43.0    NA    NA    NA    NA    NA     NA   6.6    NA   6.5    NA   2.6
    ## 160 109.0  34.1  52.6  28.6 181.3 113.2  144.0  41.5  22.7    NA    NA    NA
    ## 161    NA    NA    NA 135.1    NA 212.2     NA  48.9   0.0   0.0   0.0   0.0
    ## 162   0.0   0.0   9.0   0.0   0.0    NA     NA    NA    NA    NA    NA   0.0
    ## 163    NA   0.0    NA   0.0  37.5   1.9    0.0  12.1   0.0   4.7  45.8   4.9
    ## 164   5.5    NA    NA    NA    NA    NA     NA   9.2    NA  12.1    NA  14.3
    ## 165  71.9    NA    NA    NA    NA    NA     NA 310.5    NA  74.6    NA 118.1
    ## 166  30.8    NA    NA  16.2   6.4  14.0   39.1  17.5  21.4    NA    NA    NA
    ## 167    NA    NA    NA  27.1    NA  66.3     NA  21.1  48.1    NA  20.4   7.8
    ## 168  23.5  32.6  52.8  21.0  21.3    NA     NA    NA    NA    NA    NA  59.2
    ## 169    NA  27.9    NA  24.0  33.0    NA   14.6  22.9  37.2   7.0  30.2  23.6
    ## 170   8.2    NA    NA    NA    NA    NA     NA  21.1    NA  37.3    NA  16.9
    ## 171 169.6    NA  76.8  72.3  91.3 216.2  625.6  33.7 106.0    NA    NA    NA
    ## 172    NA    NA    NA  59.9    NA  82.6     NA 130.8  24.7    NA  38.5  12.6
    ## 173  14.8  43.1    NA  39.1  14.5    NA     NA    NA    NA    NA    NA  24.3
    ## 174    NA  35.1    NA  43.3  31.1    NA   66.8  16.7  41.8  40.4  65.6  19.9
    ## 175  68.8    NA    NA    NA    NA    NA     NA  20.5    NA  86.8    NA  30.7
    ## 176 110.0    NA 233.1 233.5 277.8 169.0  325.9  33.9 133.0    NA    NA    NA
    ## 177    NA    NA    NA  94.5    NA 291.8     NA 220.3   3.9    NA   1.3   3.3
    ## 178   1.4   1.1   9.9   0.4   0.8    NA     NA    NA    NA    NA    NA   0.8
    ## 179    NA   1.0    NA   3.0  48.9    NA   19.2  19.2   5.6  30.4  60.9   7.9
    ## 180  32.3    NA    NA    NA    NA    NA     NA  42.9    NA  18.2    NA   6.4
    ## 181  84.5    NA 112.9  51.7  62.1  73.9   92.4  34.2  14.7    NA    NA    NA
    ## 182    NA    NA    NA  59.5    NA  39.8     NA 100.6  36.2    NA  48.0  59.4
    ## 183  21.8  21.1  40.2  25.2   0.0    NA     NA    NA    NA    NA    NA  39.9
    ## 184    NA   0.0    NA   3.2  85.9    NA    6.8   6.0  23.2  29.4  21.5  10.2
    ## 185  23.9    NA    NA    NA    NA    NA     NA   4.6    NA  22.4    NA   9.1
    ## 186  17.5    NA  20.4   9.0  46.7  38.4  142.0  42.9  56.6    NA    NA    NA
    ## 187    NA    NA    NA  40.9    NA  16.0     NA  22.0  95.2    NA  59.7    NA
    ## 188  68.0  43.7  91.9  29.5   6.4    NA     NA    NA    NA    NA    NA  67.8
    ## 189    NA  66.3    NA  38.3 122.8    NA   52.4  86.2  54.7  67.6 328.3  29.5
    ## 190  60.5    NA    NA    NA    NA    NA     NA  38.9    NA  83.8    NA 100.5
    ## 191  18.8    NA  23.5  14.1  50.6  33.8   85.1  16.2  24.9    NA    NA    NA
    ## 192    NA    NA    NA   5.0    NA  11.8     NA   4.1  36.6    NA  22.2  29.5
    ## 193  30.9  53.7 305.0  68.2  32.4    NA     NA    NA    NA    NA    NA  28.9
    ## 194    NA  39.4    NA  84.4  44.3    NA   56.9  37.3  62.1  65.7 124.3  33.4
    ## 195  82.4    NA    NA    NA    NA    NA     NA  15.0    NA  92.7    NA  82.7
    ## 196  51.4    NA  69.8  53.8  33.2  42.4   77.2  15.8  24.7    NA    NA    NA
    ## 197    NA    NA    NA  90.0    NA  74.9     NA  59.1  24.5    NA  35.8  11.3
    ## 198  37.8   9.8  20.6  51.7  55.4    NA     NA    NA  33.9    NA    NA  19.5
    ## 199    NA  20.0    NA  34.3   6.8    NA   26.3   5.5   8.8  16.4 185.1  22.3
    ## 200  51.9    NA    NA    NA  14.9    NA     NA  16.8    NA   5.2    NA   0.5
    ## 201   4.1    NA  35.1  19.2  12.6  11.3   49.8   0.0   5.7    NA    NA    NA
    ## 202  50.7    NA    NA   2.0    NA  78.6     NA   3.6   0.0    NA  52.8  68.1
    ## 203  22.6  13.3  13.3    NA   0.0    NA     NA    NA  17.3    NA    NA   0.0
    ## 204    NA  54.5    NA  17.2 180.0    NA  138.4  80.3 126.5  54.1 148.0  82.2
    ## 205  28.1    NA    NA    NA  87.1    NA     NA 105.7    NA 164.7    NA  88.3
    ## 206 116.0    NA    NA    NA  89.1    NA     NA  75.1    NA  77.4    NA  90.4
    ## 207  23.9    NA  78.2  50.1  23.0  14.7   74.1  44.7  32.2    NA    NA    NA
    ## 208  50.8    NA    NA  39.8    NA 105.9     NA  55.0  54.1    NA  68.8  18.2
    ## 209  83.8 106.0 178.6  89.2 107.5    NA     NA    NA  60.5    NA    NA  44.6
    ## 210    NA  62.0    NA  31.8  87.1    NA   71.7  39.9    NA  27.6 145.6  31.6
    ## 211  58.4    NA    NA    NA  69.4    NA     NA  87.2    NA  98.3    NA  62.0
    ## 212 101.6    NA 115.9  88.2 136.0 197.2  440.2  16.6  40.0    NA    NA    NA
    ## 213 172.0    NA    NA 113.8    NA  66.0     NA  83.1   1.4    NA   0.0   0.4
    ## 214   0.0   1.3   4.9   0.0   0.0    NA     NA    NA   2.8    NA    NA   0.0
    ## 215    NA   0.0    NA   0.0   0.0    NA    0.0   0.0   0.0    NA  20.8   0.0
    ## 216   0.0    NA    NA    NA   2.1    NA     NA   0.0    NA   0.0    NA   0.0
    ## 217  12.7    NA  70.8  23.1  10.0  14.1   38.8   6.5  10.1    NA    NA    NA
    ## 218  42.9    NA    NA  15.7    NA 100.8     NA  40.5  26.2    NA   7.5   9.8
    ## 219   6.0   4.7   6.8   3.0   5.1    NA     NA    NA   9.4    NA    NA   9.2
    ## 220    NA   4.2    NA  10.5   5.5    NA    8.8  10.1  15.8   8.8  15.2  28.0
    ## 221  40.9    NA    NA    NA  15.3    NA     NA   8.6    NA  20.8    NA   9.4
    ## 222   0.0    NA   0.0   0.8  18.0   0.0   76.0   0.0   0.0    NA    NA    NA
    ## 223   3.9    NA    NA   0.6    NA   0.0     NA   0.1 114.8    NA 274.1 142.8
    ## 224  46.2 145.8 296.6 201.7  35.4    NA     NA    NA 157.5    NA    NA  83.9
    ## 225    NA    NA    NA 195.4   9.7    NA    9.5   5.8   0.0   0.0   5.7  16.2
    ## 226   2.5   0.0    NA    NA   4.3    NA     NA   1.3    NA    NA    NA   1.9
    ## 227 160.7    NA 263.4 134.9 315.6 147.2  369.7  73.0 146.5 124.5    NA    NA
    ## 228 315.5    NA    NA  66.4    NA    NA     NA 163.1 106.5    NA 162.2  31.3
    ## 229  82.4  81.2  74.5  49.5  25.3  43.4     NA    NA  94.3    NA    NA 138.1
    ## 230    NA    NA    NA  39.1  15.7    NA   22.1  25.7   8.1  12.8  38.5  15.8
    ## 231   4.8   3.0    NA    NA  18.6    NA     NA   4.4    NA    NA    NA  24.3
    ## 232  38.4    NA  64.7  58.0  60.4 159.9  256.7  22.3  46.8  27.0    NA    NA
    ## 233  84.9    NA    NA  71.4    NA    NA     NA  59.1  25.7    NA  42.1  11.8
    ## 234  29.1  19.8 172.4  29.7  32.0  35.8     NA    NA  45.1    NA    NA  39.8
    ## 235    NA    NA    NA    NA  18.6    NA    5.5   6.9  21.7   9.7  13.4   1.7
    ## 236  11.8   6.0    NA    NA  14.7    NA     NA   6.5    NA    NA    NA    NA
    ## 237  17.5    NA    NA  35.8  47.1  64.3   81.8   6.5  23.3  25.6    NA    NA
    ## 238  59.4    NA    NA   4.7    NA    NA     NA    NA   0.0    NA   0.1   0.0
    ## 239   0.1   0.0   1.0   0.0   0.2   0.0     NA    NA   0.0    NA    NA   0.0
    ## 240    NA    NA    NA    NA  89.6    NA   55.1  44.5  57.2  41.1 235.2  79.6
    ## 241  83.0  88.4    NA    NA  45.6    NA     NA  50.0    NA    NA    NA    NA
    ## 242   0.0    NA   0.0   0.0   0.0   0.0    0.0   0.0   0.0   0.0    NA    NA
    ## 243   0.0    NA    NA   0.2    NA    NA     NA    NA   7.4    NA  46.6  40.7
    ## 244   9.9   0.0   2.2   0.0   0.0   6.3     NA    NA   3.7    NA    NA  25.8
    ## 245    NA    NA    NA    NA  51.1    NA   19.4  20.8  17.4  47.6  91.7  43.2
    ## 246  31.5  46.7    NA    NA  20.6    NA     NA  47.2    NA    NA    NA    NA
    ## 247  55.9  27.4    NA    NA  12.4    NA     NA  27.9    NA    NA    NA    NA
    ## 248  72.5    NA 120.6 100.0 111.7 134.7  485.2  54.4  61.3  68.2    NA    NA
    ## 249 137.8    NA    NA 130.0    NA    NA     NA    NA 127.9    NA 167.4 159.9
    ## 250 187.7 224.5 292.3  55.8 178.7  57.6     NA    NA 144.4    NA    NA 122.5
    ## 251    NA    NA    NA    NA 149.3    NA   71.3 116.0  79.4  57.8 376.0  73.4
    ## 252    NA  34.2    NA    NA 113.4    NA     NA  43.6    NA    NA    NA    NA
    ## 253  47.9    NA  60.8  64.8  52.8 148.6  125.0  35.3  44.8  49.3    NA    NA
    ## 254  55.6    NA    NA  85.9    NA    NA     NA    NA   2.3    NA  11.3   6.1
    ## 255  10.8  15.4  26.1   2.2   8.7   5.2     NA    NA  14.9    NA    NA   8.8
    ## 256    NA    NA    NA    NA 191.2  87.7   70.8 116.0  73.4 125.8 315.6  71.0
    ## 257  94.4  77.1    NA    NA  74.7    NA     NA  49.4    NA    NA    NA    NA
    ## 258   0.5  16.8  30.5  20.7   2.7  15.7   36.3   4.3   5.4   8.5    NA    NA
    ## 259  17.6    NA    NA  11.5    NA    NA     NA    NA  27.3    NA  36.6  25.7
    ## 260  31.3  31.5  55.4  16.9  40.1  23.6     NA    NA  33.5    NA    NA  43.0
    ## 261    NA    NA    NA    NA   0.0   0.0    2.5   0.0   0.0   2.3  12.8   0.3
    ## 262   8.8   1.6    NA    NA   3.4    NA     NA   1.1    NA    NA    NA    NA
    ## 263   0.0   0.0   0.6  24.5   0.0   0.0    0.0   0.2   1.8   0.0    NA    NA
    ## 264   0.0    NA    NA   0.0    NA    NA    0.0    NA   2.1   0.0   0.0   0.0
    ## 265   0.0   0.0  26.8   0.0   0.0  10.9     NA    NA   0.0    NA    NA   0.0
    ## 266    NA    NA   0.0    NA  82.4  25.9   12.3  22.5  22.2   9.1  30.1  26.0
    ## 267  43.0  47.7    NA    NA  49.5    NA     NA  31.3    NA    NA  40.4    NA
    ## 268  76.9 140.9  91.6  55.6 113.2 106.1  281.9  60.8  44.4  37.4    NA    NA
    ## 269  91.1    NA    NA  45.6    NA    NA   82.6    NA 161.7 316.0 214.7  70.4
    ## 270 199.8 219.6 210.0 105.4  91.6  74.0     NA    NA 129.1    NA    NA 270.6
    ## 271    NA    NA 147.8    NA  58.5  45.1   47.1  39.3  31.7  27.1  85.4  26.8
    ## 272  26.9    NA    NA    NA  41.4    NA     NA  31.8    NA    NA  28.9    NA
    ## 273  64.5  91.8  72.8  56.8  77.0 133.4  344.9  18.8  48.7  55.4    NA    NA
    ## 274  68.4    NA    NA 111.1    NA    NA   91.7    NA   6.8  16.7  19.6   3.2
    ## 275  11.4   6.7  32.4  14.1  10.5   6.9     NA    NA  26.7    NA    NA   2.3
    ## 276    NA    NA  13.6    NA 107.5  70.2   48.3  76.7  91.3  36.1 146.7  20.7
    ## 277  51.4  67.2    NA    NA  67.3    NA     NA  46.3    NA    NA  43.3    NA
    ## 278  79.0 237.9 305.9 242.7 225.1 131.6  268.3  71.8 159.5  50.5    NA    NA
    ## 279 242.2    NA    NA 155.4    NA    NA  177.2    NA  16.6   9.2   3.1   4.6
    ## 280  14.0   4.5   5.4   2.3    NA   5.4     NA    NA   6.1    NA    NA  12.5
    ## 281    NA    NA   1.1    NA  64.8  16.2   10.1  49.8   6.4  31.0 134.2  75.0
    ## 282  30.9  39.8    NA    NA  13.9    NA     NA  11.3    NA    NA  13.7    NA
    ## 283  36.1   2.6   7.5  11.9   0.0   0.0   68.2   2.2  15.1   0.0    NA    NA
    ## 284  83.8    NA    NA  82.0    NA    NA   15.6    NA  94.5 176.1 226.5 282.7
    ## 285  51.1 100.6 130.0 224.1  58.1  61.8     NA    NA 125.7    NA    NA    NA
    ## 286    NA    NA  82.7    NA  59.8  16.2    9.0  44.2  19.0   8.5  47.7  25.9
    ## 287  49.3  42.4    NA    NA  36.2    NA     NA    NA    NA    NA  38.2    NA
    ## 288 112.1  76.4    NA    NA 221.7    NA     NA    NA    NA    NA 162.5    NA
    ## 289 388.4 327.3 603.3 335.8 467.1 307.6 1019.8 258.8 350.3 353.4    NA    NA
    ## 290 357.4    NA    NA    NA    NA    NA  248.5    NA  43.9 168.3  89.0   8.6
    ## 291  96.5  44.8  46.8  25.0   0.0  35.4     NA    NA  23.8    NA    NA    NA
    ## 292    NA    NA  34.0    NA  68.2  56.6   58.4  62.0  98.4  26.0 190.9  43.0
    ## 293  69.0  32.9    NA    NA  99.6    NA     NA    NA    NA    NA  51.2    NA
    ## 294  88.2  43.2  38.2    NA  56.2 148.7  369.0  47.4  48.5  61.0    NA    NA
    ## 295 111.3    NA    NA    NA    NA    NA   64.0    NA   8.5   5.1   7.3  19.0
    ## 296   6.9  12.4  31.5  10.7   9.9   6.3     NA    NA  37.2    NA    NA    NA
    ## 297    NA    NA  10.2    NA  94.3  29.6   48.4  42.7  42.4  45.4 181.6  25.0
    ## 298  60.8 119.4    NA    NA  47.0    NA     NA    NA    NA    NA  52.5    NA
    ## 299   3.5  20.4  47.4  21.5  29.8    NA    5.5   0.3   0.0   8.6    NA    NA
    ## 300  37.1    NA    NA    NA    NA    NA    1.5    NA  25.5  13.0   9.9  20.8
    ## 301  21.6  32.9  35.5  24.5  11.5  11.8     NA    NA  25.9    NA    NA    NA
    ## 302    NA    NA  48.4    NA   0.0  10.7    5.1  19.6  17.1  29.7 100.7  34.1
    ## 303  22.5  14.6    NA    NA  18.9    NA     NA    NA    NA    NA  23.5    NA
    ## 304 109.4  59.1  86.5  10.6  94.3  55.3  122.1  16.0  22.0   0.1    NA    NA
    ## 305  85.5    NA    NA    NA    NA    NA   42.2    NA  13.4  15.8   0.0  24.2
    ## 306   0.0  16.6    NA   0.0   0.0   0.0     NA    NA   2.8    NA    NA    NA
    ## 307    NA    NA   0.0    NA  58.5  16.7   25.2  68.4  45.8  74.4 103.2  12.3
    ## 308   9.4  17.0    NA    NA  62.3    NA     NA    NA    NA    NA  27.8    NA
    ## 309 113.1  64.1  84.1  65.4  75.6    NA  292.5 139.0 235.2  54.6    NA    NA
    ## 310 140.7    NA    NA    NA    NA    NA  122.3    NA  89.7  90.2 133.5  19.7
    ## 311  80.4  28.7 101.3  31.9  57.1  96.3     NA    NA  84.3    NA    NA    NA
    ## 312    NA    NA 102.7    NA  19.4   0.0   11.6  15.2  19.3   6.4  53.3   4.7
    ## 313  10.6   8.0    NA    NA   7.8    NA     NA    NA    NA    NA   1.6    NA
    ## 314  15.1  18.5  46.6  18.5  48.9  25.0   95.9   1.7   5.8  42.4    NA    NA
    ## 315  63.6    NA    NA    NA    NA    NA    0.0    NA  35.4  55.3  56.8  15.2
    ## 316  37.0  39.6  76.1  70.7  28.6  23.4     NA    NA  50.4    NA    NA    NA
    ## 317    NA    NA  31.9    NA 190.7  52.1   46.4 102.0  60.8  73.3 261.3  34.5
    ## 318  78.7  73.9    NA    NA  89.4    NA     NA    NA    NA    NA 102.6    NA
    ## 319  10.5  41.3  67.8  28.3  31.6  34.9   52.8   4.8  14.2  19.7    NA    NA
    ## 320  39.7    NA    NA    NA    NA    NA   20.9    NA   4.3   2.4   4.4   7.4
    ## 321   4.8   4.7   4.8   3.9   2.9   3.6     NA    NA   7.4    NA    NA    NA
    ## 322    NA    NA   3.2    NA   0.0  22.6   26.6   0.0   4.9   5.8   6.1   0.0
    ## 323   0.0   8.5    NA    NA   4.8    NA     NA    NA    NA    NA   0.0    NA
    ## 324   6.5   9.4   0.3   5.7  10.0  60.8   79.5   0.0   0.0   0.0    NA    NA
    ## 325  32.6    NA    NA    NA   5.4    NA    0.0    NA  16.4  49.3  92.4  19.5
    ## 326  18.1  47.1  81.2  70.1  10.5  14.7     NA    NA  42.7    NA    NA    NA
    ## 327  76.4    NA  39.0    NA  50.7   4.9    5.8   9.5  18.5   0.4  48.2  19.3
    ## 328  37.9  25.2    NA    NA  11.1    NA     NA    NA  20.3    NA  26.6    NA
    ## 329  54.4  85.8    NA    NA 257.5    NA     NA    NA  90.5    NA 201.3    NA
    ## 330 165.3  92.5  66.9    NA 152.1 141.7  229.0  91.6 168.4  75.8    NA    NA
    ## 331 169.9    NA    NA    NA 113.7    NA   92.1    NA 289.5 188.8 141.8  93.0
    ## 332 207.6 174.6 447.8  75.8 236.4 147.8     NA    NA 184.6    NA    NA    NA
    ## 333 167.7    NA 176.6    NA  79.3  66.3   61.1  57.4  69.3  46.2 507.4    NA
    ## 334  34.4  28.2    NA    NA 103.7    NA     NA    NA  48.2    NA  65.6    NA
    ## 335  52.5  29.9  53.5  83.2  77.2 143.0  210.4  25.8  30.4  90.4    NA    NA
    ## 336 114.0    NA    NA    NA  35.4    NA  138.6    NA   0.0   7.3   1.3   0.0
    ## 337   0.2   8.0  18.0   0.9   2.3   0.1     NA    NA   7.9    NA    NA    NA
    ## 338   3.0    NA   0.0    NA  32.0   5.7   11.6   0.0  10.7  25.9 265.6  15.6
    ## 339  27.6  10.2    NA    NA   9.4    NA     NA    NA  10.8    NA  32.7    NA
    ## 340  38.4  24.7  96.5  65.4  65.0  64.4  115.9  15.8  29.5  32.2    NA    NA
    ## 341 130.5    NA    NA    NA  32.7    NA   49.1    NA  20.6  24.2  21.1  14.8
    ## 342  31.4  16.0  27.3  29.4  40.7  27.8     NA    NA  14.1    NA    NA    NA
    ## 343  17.0    NA  33.7    NA  67.9  27.8   40.7  21.5   8.9  43.9 105.8  44.5
    ## 344  94.3 122.1    NA    NA  34.4    NA     NA    NA  66.7    NA  74.4    NA
    ## 345   4.0  17.8   1.5  17.6   8.3   0.0    0.0   5.0   0.0   7.2    NA    NA
    ## 346  35.3    NA    NA    NA  26.2    NA   53.4    NA  99.1  91.0 333.2 189.3
    ## 347  47.2 151.7 260.5  82.6  62.8  99.5     NA    NA  90.1    NA    NA    NA
    ## 348 234.5    NA 139.8    NA 207.8  76.9   63.3 125.6  67.8  51.2  50.9  67.3
    ## 349  88.3  88.0    NA    NA 121.1    NA     NA    NA  41.8    NA 118.2    NA
    ## 350  26.1  36.5  22.1  29.3  53.2  21.1   79.8  29.1  12.8  14.3    NA    NA
    ## 351  75.3    NA    NA    NA  66.3    NA    9.6    NA  68.7  95.1 153.9  26.0
    ## 352  84.8  79.5 254.5  66.2 157.3  54.6     NA    NA  48.2    NA    NA    NA
    ## 353 137.0    NA 118.0    NA  96.9  43.7   93.1  38.9  58.4  47.5 199.2  26.4
    ## 354  60.0  20.1    NA    NA  79.5    NA     NA    NA  52.2    NA  66.4    NA
    ## 355  29.4  35.9  50.5  29.2  33.4  35.8  120.2   6.6    NA  36.4    NA    NA
    ## 356  32.0    NA    NA    NA  20.6    NA   17.3    NA  68.9  58.3  62.5  53.3
    ## 357  85.8  58.7 228.6  57.0  35.1  36.7     NA    NA 154.5    NA    NA    NA
    ## 358  60.5    NA 124.5    NA  13.6   0.0    8.1   9.5   3.6   9.6  95.1  15.7
    ## 359  31.7   0.0    NA    NA  15.6    NA     NA    NA   5.0    NA  54.2    NA
    ## 360  35.8  24.1 100.4  26.2  27.4  55.7   70.2  13.4  63.1  39.9    NA    NA
    ## 361  50.9    NA    NA    NA  41.1    NA   25.5    NA   4.7   0.5   6.0   1.9
    ## 362    NA   4.3   7.2   3.0   1.8   4.5     NA    NA   4.3    NA    NA    NA
    ## 363   5.5    NA   6.5    NA   5.8   0.0    0.0   4.2   1.8    NA   0.3   0.0
    ## 364   0.0   5.8    NA    NA   3.6    NA     NA    NA   0.0    NA   0.0    NA
    ## 365   1.9   0.0   0.0   2.1   0.0   0.0   59.3   0.0   0.0   0.5    NA    NA
    ## 366   0.3    NA    NA    NA   0.0    NA    1.1    NA  23.6  50.3 115.5  47.0
    ## 367   4.6  24.4  31.6  53.7  31.9   5.4     NA    NA  20.4    NA    NA    NA
    ## 368  24.2    NA   7.2    NA  63.9  25.0   24.8  31.4  80.7  24.6  46.7  22.4
    ## 369   4.3  54.5    NA    NA  70.1    NA     NA    NA  17.8    NA 138.5    NA
    ## 370 100.8  56.0    NA    NA 298.7    NA     NA    NA  50.6    NA  86.2    NA
    ## 371  60.7 187.4 173.3 143.1 300.8 129.5  243.4 129.4 171.3 107.4    NA    NA
    ## 372 183.7    NA    NA    NA 160.6    NA  255.8    NA 359.8 294.3 244.6 176.2
    ## 373 270.7 285.9 735.5 183.0 286.5 114.0     NA    NA 251.9    NA    NA    NA
    ## 374 229.3    NA 352.5    NA  32.0  51.0   63.7  40.6    NA  49.4 253.8  31.2
    ## 375  41.6  14.9    NA    NA 105.9    NA     NA    NA  46.4    NA  37.5    NA
    ## 376  51.3  46.8  66.4  34.1  56.0  49.0  356.8  30.2  78.8  54.4    NA    NA
    ## 377  45.2    NA    NA    NA  45.0    NA   54.7    NA  12.8   7.5   9.6   3.3
    ## 378   4.0  13.4  18.2   0.9   1.9   1.4     NA    NA  29.0    NA    NA    NA
    ## 379   7.7    NA   5.8    NA  23.2   2.5   11.2  12.5   1.0  24.1 129.1   3.2
    ## 380   9.1  34.6    NA  24.8  13.7    NA     NA    NA   5.0    NA  17.9    NA
    ## 381  19.5  12.7  49.8  22.6  22.5  47.9   85.0   3.4   7.4  19.0    NA  22.7
    ## 382  31.3    NA    NA    NA  33.9    NA   12.4    NA   7.4   0.1    NA   1.3
    ## 383   0.3   1.5    NA   2.4   3.2   2.1     NA   2.0   1.1    NA    NA    NA
    ## 384   0.0    NA   1.4    NA   5.0  16.0    8.1   5.2  21.1  23.3 105.3  49.2
    ## 385  65.7  57.6    NA   5.1  13.2    NA     NA    NA  18.1    NA  88.3    NA
    ## 386  16.9   0.0   3.6   0.8   0.0  22.7    0.0   0.0   0.0  50.4    NA   0.0
    ## 387   6.7    NA    NA    NA   0.3    NA    0.0    NA  32.5  78.8 256.7 158.9
    ## 388  70.4  96.4  84.2  20.7   9.7  26.5     NA 265.1  45.0    NA    NA    NA
    ## 389 106.2    NA  51.8    NA  25.1  19.6    5.7  25.3  37.8  15.2  19.0  28.6
    ## 390  21.9  12.4    NA  21.3  30.5    NA     NA    NA  14.7    NA  32.7    NA
    ## 391 102.3  59.0  37.7  70.9  67.3  73.9  246.6  27.1  78.8  76.1    NA 174.9
    ## 392 116.4    NA    NA    NA  51.9    NA   46.1    NA  82.3 156.8  83.4  66.1
    ## 393 108.6 115.6 207.8  44.7 103.8    NA     NA 221.3 151.1    NA    NA    NA
    ## 394  87.7    NA 138.0    NA  70.7 156.9  106.6 107.0 118.4  63.5 596.9  52.6
    ## 395  57.6  49.0    NA 177.8 140.8    NA     NA    NA  74.5    NA  60.8    NA
    ## 396  90.1  42.2  55.7  38.4  40.4  54.9  283.9  39.1  52.5  99.9    NA  86.2
    ## 397 105.5    NA    NA    NA  51.5    NA   75.1    NA  67.8  87.3  66.3  47.7
    ## 398  68.4  80.4 259.8  61.7  49.5  25.4     NA  89.7 209.2    NA    NA    NA
    ## 399  58.9    NA  65.9    NA 100.0  50.8   35.2  64.7  50.1  98.3 358.9  20.7
    ## 400  73.3  42.5    NA 109.7  76.7    NA     NA    NA  43.1    NA 104.0    NA
    ## 401   0.9   7.7   8.5   7.0   1.8   4.5    1.6   1.7   1.3    NA    NA  19.9
    ## 402  12.5    NA    NA    NA   0.0    NA    5.8    NA   0.2   0.6   2.5   0.5
    ## 403   1.0   0.8   1.4   0.7   1.1   1.5     NA   0.0   3.5    NA    NA    NA
    ## 404   3.9    NA   5.6    NA   6.3   7.8    6.0  19.8  15.0  15.0  55.5  32.3
    ## 405  29.2   0.7    NA  32.8  17.6    NA     NA    NA  10.1    NA  42.8    NA
    ## 406   0.0   0.0  11.7   2.5  12.8   3.9   41.3   0.0   0.0   0.0    NA   0.0
    ## 407   0.0    NA    NA    NA   0.0    NA    0.0    NA 137.0 143.4 239.8 201.9
    ## 408  41.1 134.7 166.4  54.9  27.1  52.4     NA 224.5 159.2    NA    NA    NA
    ## 409 144.6    NA  88.7    NA 174.9  45.5   23.6  23.1  86.5  38.3  88.7 124.9
    ## 410  38.9 138.6    NA  38.7  63.9    NA     NA    NA  23.8    NA 174.7    NA
    ## 411  28.8  43.0    NA  41.3  43.0    NA     NA    NA  33.3    NA  81.3    NA
    ## 412 233.6 257.4 366.7 232.0 290.9  92.8  540.9 242.4 208.6 132.6    NA 630.0
    ## 413 428.5    NA    NA    NA 297.8    NA  313.8    NA 148.6 116.1 100.2  38.9
    ## 414  46.3  75.2 248.5 106.3 164.0  55.5     NA 116.2  69.3    NA    NA    NA
    ## 415  78.9    NA 428.7    NA  33.5  75.6   54.0  65.0  57.1   9.6  26.7   8.8
    ## 416  20.9  19.9    NA  42.5  48.7    NA     NA    NA  37.5    NA   8.0    NA
    ## 417  14.9  18.9  18.5  15.2  14.7  33.3   19.3   2.5   7.8  28.0    NA  41.8
    ## 418  18.5    NA    NA    NA  14.8    NA   27.5    NA  90.5 175.6 111.3  76.0
    ## 419  85.5 107.3 484.3 130.4  55.8  70.3     NA 117.6 272.2    NA    NA    NA
    ## 420  63.9    NA 101.9    NA 261.2  73.0   57.5  60.5  46.1  96.9 318.6  70.2
    ## 421  88.5 133.8    NA 118.4  92.9    NA     NA    NA  77.5    NA 193.3    NA
    ## 422  69.7 129.7 163.8 181.9 150.5  88.1  138.5  30.2  55.7  95.3    NA 163.5
    ## 423 196.8    NA    NA    NA  80.8    NA  118.3    NA   1.0   0.0   1.2   2.5
    ## 424   1.8   1.8   5.0   1.3   0.7   0.5     NA   0.6   4.3    NA    NA    NA
    ## 425   0.0    NA   5.0    NA    NA   0.0    0.0   0.0   0.0   0.0   1.7   0.0
    ## 426   0.0   0.0    NA   0.0   0.4    NA     NA    NA   0.0    NA   4.9    NA
    ## 427  76.4   5.5   3.0  79.8  24.6  51.8  145.1   0.0   0.1  26.5    NA   0.0
    ## 428  48.6    NA    NA    NA   7.1    NA  103.7    NA   2.1  25.6  81.0  64.5
    ## 429  15.0  53.5  10.9   7.9  21.9  10.9     NA  39.7  14.1    NA    NA    NA
    ## 430  65.8    NA  10.5    NA  50.2  16.6    1.8  12.9  27.1   8.6  12.5   0.0
    ## 431  21.9  33.3    NA  36.3  28.6    NA     NA    NA  10.4    NA  27.5    NA
    ## 432  97.5 281.6 251.7  98.0 199.4 109.9  494.4  97.7 198.7  95.1    NA 274.9
    ## 433 116.3    NA    NA    NA 221.9    NA  214.9    NA  37.0  50.7  36.0  16.4
    ## 434  20.0  30.5  63.5  67.7 126.2  31.5     NA  83.6  27.7    NA    NA    NA
    ## 435  23.0    NA  65.1    NA  14.2   3.2   11.0  24.8  27.2   7.4  14.4  12.5
    ## 436   4.6   0.1    NA  31.3  20.1    NA     NA    NA   4.2    NA   0.0    NA
    ## 437  31.7  19.1  21.8  17.4  20.3  54.8  118.0  14.3  17.8  23.8    NA  29.6
    ## 438  15.3    NA    NA    NA  10.1    NA   46.0    NA  34.0  46.7  24.0  17.6
    ## 439  43.8  25.2 138.7  38.0  22.3  16.6     NA  44.1  53.0    NA    NA    NA
    ## 440  29.7    NA  52.7    NA 143.0  55.2   37.4  42.0  46.4  67.2  99.3  43.7
    ## 441  65.5  52.8    NA  64.7  45.6    NA     NA    NA  57.7    NA 138.3    NA
    ## 442   5.2  33.2  36.9  24.2   9.1  24.2   48.9   2.2   6.7   2.8    NA  22.5
    ## 443  23.4    NA    NA    NA  33.5    NA   10.0    NA  25.4   6.4  28.9  23.3
    ## 444  15.3  20.6  48.0  15.1  21.9  31.3     NA  33.1  21.7    NA    NA    NA
    ## 445  23.2    NA  41.5    NA   0.4   6.7   18.3   8.0  10.2  29.2  29.6   3.2
    ## 446  30.7  29.3    NA  18.7   5.9    NA     NA    NA   9.3    NA  13.2    NA
    ## 447   0.0   1.4   0.1   0.0   0.0   3.7    3.9   0.0   0.0   0.0    NA   0.0
    ## 448   0.0    NA    NA    NA   1.4    NA    0.0    NA   6.5  24.2  44.5  78.1
    ## 449   8.0  64.3  43.0  62.0  55.1   8.7     NA 104.8  44.0    NA    NA    NA
    ## 450  60.5    NA  75.4    NA  62.2  44.8   11.0  38.5  48.7  23.3  27.5   4.1
    ## 451   4.2  12.2    NA  63.9  48.1    NA     NA    NA  56.6    NA  66.2    NA
    ## 452  29.1  28.3    NA  14.5    NA    NA     NA    NA  42.0    NA  38.2    NA
    ## 453  58.7 156.6 112.5    NA 186.5  88.1  284.3 122.7  83.5  60.6    NA 254.6
    ## 454    NA    NA    NA    NA  58.9    NA  113.6    NA 184.0 185.9 211.4    NA
    ## 455 165.0 198.7 402.5  95.2 162.2 137.2     NA 147.4    NA    NA    NA    NA
    ## 456 134.0    NA 274.3    NA  57.1 123.3   91.2    NA 122.3  33.0 304.9  28.3
    ## 457  26.6  58.1    NA  60.2    NA    NA     NA    NA  74.2    NA  31.3    NA
    ## 458   0.0   5.2   0.0    NA   0.0   0.9   15.3   0.0   0.0   0.0    NA   0.0
    ## 459    NA    NA    NA    NA   2.4    NA    0.0    NA   5.5    NA   6.6    NA
    ## 460  18.6  17.1  90.9   4.3   2.9   8.9     NA  13.2    NA    NA    NA    NA
    ## 461   4.5    NA   6.3    NA 114.0  19.8   18.6    NA  20.2  85.7 215.3  12.0
    ## 462  44.1  27.1    NA  90.1    NA    NA     NA    NA  18.5    NA 206.9    NA
    ## 463   0.0   1.4   0.0    NA   0.0   0.5    0.0   0.0   0.0   4.4    NA   0.0
    ## 464    NA    NA    NA    NA   0.0    NA    0.0    NA   5.6   0.2   0.2    NA
    ## 465   1.0   4.0   8.4   0.0   0.6   6.0     NA   0.4    NA    NA    NA    NA
    ## 466   1.0    NA   1.1    NA   0.9   1.3    0.0    NA   0.0   3.9   0.9   0.0
    ## 467   0.0   2.2    NA   0.0    NA    NA     NA    NA   0.0    NA   0.0    NA
    ## 468   0.0   0.0   0.0    NA   0.0   0.0    0.0   0.8   0.0   0.0    NA   0.0
    ## 469    NA    NA    NA    NA   0.0    NA    0.0    NA 167.8 114.4 275.7    NA
    ## 470  26.1  77.0 124.5 144.0  42.0  61.6     NA 274.5    NA    NA    NA    NA
    ## 471 273.7    NA  70.1    NA  61.7  22.8   38.9    NA   3.4  30.6  17.8   8.0
    ## 472  10.9  18.6    NA  22.7    NA    NA     NA    NA  37.9    NA 118.2    NA
    ## 473  51.2  22.3  33.7    NA  21.9  12.0   53.0  12.8  32.8  19.4    NA  22.2
    ## 474    NA    NA    NA    NA  20.3    NA   19.6    NA  32.3  66.4  39.8    NA
    ## 475  61.9  59.2 119.7  33.3  35.2  15.4     NA  98.7    NA    NA    NA    NA
    ## 476  35.3    NA   0.0    NA  65.1 126.9   86.8    NA  97.3  42.0 443.5  34.7
    ## 477  33.6  11.8    NA  98.2    NA    NA     NA    NA  61.3    NA  52.6    NA
    ## 478 178.1  53.8 107.1    NA  74.8 205.5  590.8  45.2  48.8 163.6    NA 211.1
    ## 479    NA    NA    NA    NA  98.5    NA  182.0    NA  18.5  42.9  21.0    NA
    ## 480  22.0  17.1  74.0  37.6  11.2   7.6     NA  19.8    NA    NA    NA    NA
    ## 481  10.9    NA   7.0    NA  37.5  35.8   44.2    NA  50.3  59.4 204.2   6.8
    ## 482  20.0  34.8    NA 105.7    NA    NA     NA    NA  49.7    NA  50.9    NA
    ## 483  39.2  82.7  91.5    NA 102.1  72.0  112.6  16.1  43.5  43.4    NA 108.9
    ## 484    NA    NA    NA    NA 101.3    NA   74.2    NA   0.5   0.9   2.7    NA
    ## 485   2.9   0.5   4.7   4.6   0.0   5.2     NA   1.8    NA    NA    NA    NA
    ## 486   0.5    NA   0.4    NA   0.0   0.8    1.8    NA   2.5   4.4   3.8   0.0
    ## 487   0.0   1.4    NA   1.3    NA    NA     NA    NA   0.0    NA   0.9    NA
    ## 488   2.2   9.2   0.4    NA  12.1  30.2  238.3   0.3   8.8  10.4    NA  88.7
    ## 489    NA    NA    NA    NA  41.3    NA    0.0    NA  76.8 108.3    NA    NA
    ## 490  27.8  68.9  99.9  58.3  49.9  45.6     NA 179.9    NA    NA    NA    NA
    ## 491 184.8    NA  77.6    NA  31.6  39.8   13.6    NA  22.5  65.9  68.5   0.0
    ## 492   0.0  14.9    NA  37.5    NA    NA     NA    NA  22.3    NA 104.7    NA
    ## 493   3.7   3.6    NA   4.2    NA    NA     NA    NA    NA    NA  17.1    NA
    ## 494   4.2  10.5  17.2    NA   9.9   9.5   36.0   6.3  40.4  18.6    NA  11.8
    ## 495    NA    NA    NA    NA    NA    NA    6.6    NA  67.5 278.1 132.2    NA
    ## 496  93.0 114.5 536.3  70.9 225.0 101.8  192.9 106.4    NA    NA    NA    NA
    ## 497    NA    NA 205.7    NA  63.1 158.1  110.1    NA 152.5  90.9 468.5  51.6
    ## 498  68.1  31.8  41.5 152.1    NA    NA     NA    NA    NA    NA  82.5    NA
    ## 499  13.2  17.0  10.4    NA   1.8  17.7   44.3  15.6  27.6  30.8  13.0   5.2
    ## 500    NA    NA    NA    NA    NA    NA   54.4    NA  12.9  29.0  47.2    NA
    ## 501  24.6  37.9 118.9  21.7  11.2  11.2   16.3  15.0    NA    NA    NA    NA
    ## 502    NA    NA  15.6    NA  18.9   9.9   13.2    NA   0.0  42.6 180.9  15.3
    ## 503  25.6   8.4  26.5  21.1    NA    NA     NA    NA    NA    NA  38.6    NA
    ## 504  11.8  59.0  76.9    NA  31.1  18.7   36.7  17.4  52.3  23.0  17.2  26.6
    ## 505    NA    NA    NA    NA    NA    NA   48.2    NA  25.8   2.6   1.3    NA
    ## 506   2.9  25.8  61.1  26.7  18.6  17.1    9.5   8.8    NA    NA    NA    NA
    ## 507    NA    NA  25.9    NA  62.1  23.2   16.6    NA  15.5  39.2 127.6  53.5
    ## 508  86.4  50.0  20.6  13.4    NA    NA     NA    NA    NA    NA  98.2    NA
    ## 509   0.0   0.0  16.4    NA   0.0   0.0    5.8   0.9   0.0   0.0   0.0   0.0
    ## 510    NA    NA    NA    NA    NA    NA    1.5    NA  53.2  88.1 158.1    NA
    ## 511  24.4  90.3 129.5  95.5  36.2  58.2   50.6  52.0    NA    NA    NA    NA
    ## 512    NA    NA  52.1    NA  17.4    NA    8.8    NA  10.2   5.2    NA  35.3
    ## 513   9.1   3.1   0.0   2.6    NA    NA     NA    NA    NA    NA  54.4    NA
    ## 514  10.1   7.5  13.2    NA   0.0   7.1   40.9   4.0   0.0   8.2  10.7   8.8
    ## 515    NA    NA    NA    NA    NA    NA   24.7    NA 155.7 273.7 135.4    NA
    ## 516 164.1 226.5 394.2 111.4 145.5 118.1  207.0  85.5    NA    NA    NA    NA
    ## 517    NA    NA 190.8    NA 165.0 262.2  118.6    NA 198.3  85.2 742.6  40.6
    ## 518  58.5  52.4  29.1 257.7    NA    NA     NA    NA    NA    NA  73.3    NA
    ## 519  94.7  45.3  63.7    NA  54.4  78.5  201.7  29.0  41.7  63.1  68.0  74.1
    ## 520    NA  26.5    NA    NA    NA    NA  120.6    NA   0.0  24.0  15.0    NA
    ## 521   8.6  15.3  50.1  17.3   2.8   2.2    4.0   6.5    NA   3.7    NA    NA
    ## 522    NA    NA   4.8    NA 173.8  91.2   77.9    NA 128.9  69.1 250.9  74.9
    ## 523 103.8  82.1 261.2  75.2    NA  65.0     NA    NA    NA    NA 282.0    NA
    ## 524   4.6  15.1  61.2    NA  34.9  29.9   37.1   4.3   9.7  10.6  30.0  31.2
    ## 525    NA   4.0    NA    NA    NA    NA   15.9    NA   3.1   0.0   0.6    NA
    ## 526   3.3   1.3   6.5   2.5   2.7   6.5    3.0   1.3    NA   5.5    NA    NA
    ## 527    NA    NA   5.1    NA  36.9    NA   39.6    NA  14.7  29.6  42.6  62.7
    ## 528  24.5  95.7  24.0   6.9    NA  59.8     NA    NA    NA    NA 112.4    NA
    ## 529  57.3  34.3  12.1    NA  24.8  30.1   46.7   0.0  23.2   1.2  19.4  53.4
    ## 530    NA   0.0    NA    NA    NA    NA   10.6    NA  62.2  46.3 228.2    NA
    ## 531  20.8  94.4 130.9  58.0  61.7  54.8   42.0  95.2    NA  46.9    NA    NA
    ## 532    NA    NA  84.1    NA 145.1  64.5   25.3    NA  41.2  50.5  44.8  89.0
    ## 533  42.4  80.7  35.5  18.0    NA  27.4     NA    NA    NA    NA  82.7    NA
    ## 534  12.8  57.8  24.4  10.2    NA   3.9     NA    NA    NA    NA  86.3    NA
    ## 535  15.7  23.2  63.6    NA 142.9  54.7  218.7  41.4  57.4  17.8   0.0  43.7
    ## 536    NA  31.9    NA    NA    NA    NA   51.2    NA 178.0 280.1 147.1    NA
    ## 537 166.2 217.1 234.3  84.4 181.4 269.3  218.7 144.9    NA 227.7    NA    NA
    ## 538    NA    NA 221.4    NA 155.4 209.2  178.8    NA 115.3  51.1 515.4  93.0
    ## 539  65.0 157.4  57.0 156.7    NA  41.0     NA    NA    NA    NA  91.6    NA
    ## 540   0.0   2.2   0.0    NA   0.0   0.0    0.0    NA   0.3   0.0   0.0   0.0
    ## 541    NA   0.0    NA    NA    NA    NA    0.0    NA  43.1  78.0  35.3    NA
    ## 542  39.0  37.5 208.6  35.3  21.8  19.7   20.4  11.5    NA  20.3    NA    NA
    ## 543    NA    NA  35.1    NA  27.6  10.0    7.9    NA  10.5  10.0  11.5   0.0
    ## 544  11.6  12.2  62.8   0.0    NA   3.7     NA    NA    NA    NA  37.8    NA
    ## 545  13.4  76.3 101.7    NA  75.0  64.9   77.6  24.0  26.2  86.4  46.4  36.6
    ## 546    NA  39.4    NA    NA    NA    NA   89.6    NA   6.7   6.8   8.0    NA
    ## 547  17.3   2.9   3.8   6.2   5.1   1.7    2.9   6.3    NA   5.9    NA    NA
    ## 548    NA    NA  11.9    NA   2.0    NA    0.0    NA   0.1   3.7  32.2   0.0
    ## 549   3.7  10.9   0.4   3.6    NA   0.0     NA    NA    NA    NA  26.3    NA
    ## 550   0.0   0.0   0.0    NA   0.0   0.0   18.8   0.1   0.0   0.0   5.5   0.0
    ## 551    NA   0.0    NA    NA    NA    NA    0.0    NA  13.6   0.0  46.2    NA
    ## 552   0.0  11.8  18.0   1.7   3.2   0.0    0.0  11.3    NA   4.9    NA    NA
    ## 553    NA    NA  40.0    NA 135.6  13.0   28.2    NA  29.8  70.0  81.9  72.9
    ## 554  36.4  61.5  88.2  39.4    NA  62.7     NA    NA    NA    NA 131.5    NA
    ## 555  82.7    NA 298.4    NA 134.0  84.0  391.6 128.2 130.4 139.4 168.8 212.6
    ## 556    NA 112.0    NA    NA    NA    NA  126.7    NA 113.9 210.8  78.0    NA
    ## 557  93.2 194.5 258.6  76.4  98.6  85.5  120.4 130.5    NA 125.2    NA    NA
    ## 558    NA    NA 140.0    NA  20.8  36.0   23.5    NA  27.5   4.2  62.9  13.4
    ## 559  11.0   6.3   8.4  32.1    NA   8.5     NA    NA    NA    NA  11.5    NA
    ## 560   6.0  16.6   7.8    NA   7.2  16.7   53.6   1.6  15.6   3.6   9.5   3.2
    ## 561    NA   3.2    NA    NA    NA    NA   12.1    NA 146.2 116.4    NA    NA
    ## 562 131.2 103.7 424.5  94.0  75.8 127.0   56.4  47.7    NA  98.8    NA    NA
    ## 563    NA    NA 180.6    NA 214.1  95.0   95.9    NA 212.3 202.9 780.1 117.9
    ## 564 180.5 170.3 316.9 112.8    NA 115.6     NA    NA    NA    NA 368.0    NA
    ## 565  62.7 135.3  85.3    NA  77.9  88.6  124.3  22.6  85.8  97.0  58.4 100.9
    ## 566    NA  48.2    NA    NA    NA    NA   68.1    NA   1.9   0.1   0.1    NA
    ## 567   0.7   0.7  15.3   0.0   0.0   0.8    0.2   0.0    NA   0.9    NA    NA
    ## 568    NA    NA   2.0    NA   0.0   0.0    0.2    NA   0.0   0.0   0.5   0.0
    ## 569   0.0   0.0   0.0   0.0    NA   0.0     NA    NA    NA    NA   0.1    NA
    ## 570   0.0    NA   0.4    NA   0.0   0.0   51.6   8.9  45.8   0.6   7.4   0.0
    ## 571    NA  46.7    NA    NA    NA    NA   36.9    NA   8.6  90.7  47.9    NA
    ## 572  32.7  85.4 115.3 115.4  26.9   0.0   23.5  70.0    NA  40.4    NA    NA
    ## 573    NA    NA  42.5    NA  60.7  26.8   19.6    NA  29.8  21.3  13.3  11.8
    ## 574  24.5  20.8  12.3  34.9    NA  12.7     NA    NA    NA    NA  32.0    NA
    ## 575  21.2  28.7  21.3  53.8    NA  36.8     NA    NA    NA    NA  85.5    NA
    ## 576 132.0  75.1 106.2    NA 309.0 117.9  247.7 104.8 116.2 112.8  88.5 139.0
    ## 577    NA 145.6    NA    NA    NA    NA  152.2    NA   9.4  93.8  63.9    NA
    ## 578  38.3  42.4  77.1  76.6  96.9  69.3   97.4  48.7    NA 100.6    NA    NA
    ## 579    NA    NA  76.2    NA  26.3  43.9   24.4    NA  43.0   4.9  46.6  11.1
    ## 580  14.5   0.0   0.0  20.0    NA  12.1     NA    NA    NA    NA  16.2    NA
    ## 581  87.3  58.9  70.3    NA  90.4 145.5  609.1  42.8  94.9 164.9 148.2 102.7
    ## 582    NA  31.2    NA    NA    NA    NA  163.4    NA  24.6  30.2  14.0    NA
    ## 583  20.8  23.4 112.0  25.5  12.8  22.8   16.4  13.5    NA  15.4  14.2    NA
    ## 584    NA    NA  19.4    NA  24.6  15.1   23.4    NA  23.5  37.2 120.0  15.5
    ## 585  72.5  26.2 112.8  16.4    NA  38.1   25.4    NA    NA    NA 104.9    NA
    ## 586  62.0  97.6 112.1    NA  90.2  53.3   79.5  22.5  54.5  71.5  83.7  63.5
    ## 587    NA  58.8  87.0    NA    NA    NA   63.5    NA   9.8  11.6  14.4  17.4
    ## 588  33.4   7.9  20.4  29.2  46.6  19.7    8.9  14.3    NA  62.3  38.1    NA
    ## 589    NA    NA  16.2    NA  11.1   0.0    0.0   9.9   3.1  10.5   7.7  45.1
    ## 590  67.3  19.3  11.6  11.8    NA  38.7   12.1    NA    NA    NA  25.9    NA
    ## 591   0.0   5.1  15.0  17.2  11.8  45.0  241.3   9.2  39.1   4.0  12.1  27.8
    ## 592    NA   0.1  37.6    NA    NA    NA   50.9    NA  28.0  17.8   0.0  71.9
    ## 593  12.0  21.7  38.2   2.3   1.9   0.0    0.0  10.5    NA  15.8   3.2    NA
    ## 594    NA    NA  23.3    NA  16.2   0.0    3.6   6.4   0.2  14.1  21.3  10.9
    ## 595   2.3   6.6   1.2   3.4    NA   8.2    0.0    NA    NA    NA  61.8    NA
    ## 596  29.0  49.2 106.9  52.1 111.8  39.3   70.2  53.5  34.5  26.3  11.2  95.5
    ## 597    NA  40.3  27.0    NA    NA    NA   69.4    NA  48.0 206.6 119.3  46.6
    ## 598 125.0 137.4 289.1  83.4 110.7  73.9   71.0  79.5    NA 117.7 115.8    NA
    ## 599    NA    NA 158.7    NA 160.7 185.5  102.3 127.1  87.4  62.9 541.1  37.5
    ## 600  70.2  59.9  24.1  99.3    NA  57.2   57.3    NA    NA    NA  77.6    NA
    ## 601  24.0  21.4  34.0  21.3  28.0  23.7   73.3  11.2  34.9  41.5  24.1  32.2
    ## 602    NA  11.6  50.3    NA    NA    NA   36.1    NA  15.9   5.5  18.0  15.3
    ## 603  11.2  22.5  77.7  16.8  10.0  15.2    9.0   8.4    NA   8.4  17.5    NA
    ## 604    NA    NA  25.7    NA  31.3  10.5   25.1  11.9  12.7  32.5  34.0  27.1
    ## 605  25.7  11.2 100.2   7.0    NA  24.2   12.3    NA    NA    NA  67.3    NA
    ## 606  68.5  32.2  98.1  63.6  29.4  42.6   55.4  13.2  40.2  64.1  31.7  28.8
    ## 607    NA  26.9  63.4    NA    NA    NA   30.7    NA   6.3   8.4   8.3   6.4
    ## 608   2.1   6.3   2.4   4.7  10.8  13.9    7.2  11.6    NA  28.4  25.7    NA
    ## 609    NA    NA  29.9    NA  37.1   3.3    8.3  71.4  31.4  22.4 114.7  61.9
    ## 610  63.3  87.8   2.9  26.5    NA  42.5   13.1    NA    NA    NA 125.3    NA
    ## 611   0.0  40.1   2.9   0.0  21.6   0.0    0.0   0.0   0.0   0.0   0.0  20.3
    ## 612    NA   0.0   0.0    NA    NA    NA    0.0    NA  25.4 130.1 225.3 127.4
    ## 613  69.2  58.1 158.6  14.6   8.4  36.5   23.6  98.6    NA  23.3  15.8    NA
    ## 614    NA    NA   1.3    NA  71.2  28.2   38.1  91.9  16.1  34.6  71.2  74.8
    ## 615  86.0  80.6  66.6  21.9    NA  57.3   56.7    NA    NA    NA  38.4    NA
    ## 616  28.3  51.8  39.7  38.9    NA  29.0   43.8    NA    NA    NA  71.4    NA
    ## 617 121.9 104.8 121.4  40.8 113.8  54.4  153.5    NA 119.8  68.6  91.3  58.1
    ## 618    NA  59.9 130.8    NA    NA    NA  190.1    NA  52.1  66.6  37.9  13.1
    ## 619  55.5  53.8  24.3    NA   0.0   7.8   11.5  16.8    NA  46.5  21.1    NA
    ## 620    NA    NA   0.0    NA  76.1  50.0   37.5  31.6  50.2  46.6 193.7    NA
    ## 621  19.1   8.9   4.4  33.1    NA  10.4   34.6    NA    NA    NA  42.5    NA
    ## 622  82.4  27.4  97.9  39.0  38.3  67.0  125.8    NA  55.6 104.5  80.3  50.9
    ## 623    NA  22.0  79.6    NA    NA    NA   85.1    NA   7.3  13.2   7.5   3.6
    ## 624   6.8   8.2  45.3    NA    NA   8.0    7.6   5.0    NA   7.1   3.5    NA
    ## 625    NA    NA   4.5    NA 106.7   9.7   20.3  28.4  40.2  42.8 254.2    NA
    ## 626  52.7  88.6 161.3  30.5    NA  15.5   30.8    NA    NA    NA  77.2    NA
    ## 627   6.0  26.0  17.5  12.7   5.9   7.6    3.1    NA   3.4   7.8   8.1   4.1
    ## 628    NA   3.1   3.3    NA    NA    NA   10.7    NA  44.4   9.9  17.3  33.4
    ## 629  41.5  20.4  40.3    NA  15.2  36.6   28.6  23.8    NA  40.0  29.0    NA
    ## 630    NA    NA  37.8    NA  23.4   5.1    4.2   4.2   2.2  20.7   6.8    NA
    ## 631   9.2  15.5   5.4   4.1    NA  32.2    5.8    NA    NA    NA  27.7    NA
    ## 632  68.9  38.8   3.9  38.8  62.1  51.7  248.9    NA  51.6   0.0   0.0  49.3
    ## 633    NA   3.3  28.3    NA    NA    NA   31.8    NA   0.0  41.0  79.7 110.7
    ## 634  15.9  49.2  22.8    NA   0.0  28.1    6.5  46.4    NA   3.3   1.9    NA
    ## 635    NA    NA  34.6    NA  94.6   0.0    0.0  12.1  14.3    NA  36.1    NA
    ## 636 104.7  11.1   2.3  15.1    NA  16.9    5.7    NA    NA    NA  90.9    NA
    ## 637  98.8  75.1 153.6  72.8 133.7  74.7  275.0    NA 233.1 171.9 131.0 100.1
    ## 638    NA 150.5 143.5    NA    NA    NA  107.7    NA 102.5  85.2 145.0  31.9
    ## 639  79.9 110.8 255.5    NA  46.4  29.0   37.2  26.4    NA  34.4  38.9    NA
    ## 640    NA    NA  93.5    NA  20.3  20.5    9.0  11.6   8.3   2.6  50.8    NA
    ## 641  17.9   3.7   2.1  19.0    NA   7.7    9.1    NA    NA    NA  10.4    NA
    ## 642  11.6  17.7  13.3  12.5   7.8  12.6   20.2    NA  11.5  32.5  35.4   7.1
    ## 643    NA   8.1  29.1    NA    NA    NA   14.4    NA  30.9  65.4  68.2  29.7
    ## 644  56.5  36.1 101.2    NA  32.1  40.5   24.8  20.5    NA  25.9  33.0    NA
    ## 645    NA    NA  52.6    NA 147.8  49.2   50.9  39.3 105.2 124.9 292.5    NA
    ## 646  39.6  92.2 176.5  49.4    NA  55.6   62.3    NA    NA    NA  97.6    NA
    ## 647    NA  30.9    NA  31.9  20.0   4.6   14.8    NA   7.2  15.3  16.0  12.3
    ## 648    NA  17.6   2.9    NA    NA    NA    9.7    NA  31.8   5.0  31.0  45.7
    ## 649  26.9  22.1  43.1    NA  35.5  26.4   24.0  16.5    NA  93.7  29.7    NA
    ## 650    NA    NA  31.1    NA   7.0  16.6   23.6   4.3  23.0   7.1  45.0    NA
    ## 651   3.8  62.2  36.7   7.7    NA   0.0   13.8    NA    NA    NA  30.3    NA
    ## 652   0.0   0.0   0.0   0.0   0.0   0.0    0.0    NA   0.0   0.0   0.0   0.0
    ## 653    NA   0.0   0.0    NA    NA    NA    0.0    NA  56.7  54.3  58.8  73.0
    ## 654  19.9  45.0  77.2    NA   4.9  51.3   35.3  38.4    NA  10.2   9.0    NA
    ## 655    NA    NA  83.6    NA  96.3  23.7    2.9  18.0  11.1    NA  21.5    NA
    ## 656  61.1  51.9  42.0  11.0    NA  34.3   20.3    NA    NA    NA 132.1    NA
    ## 657  51.5   1.7    NA  30.3    NA  13.3   34.9    NA    NA    NA    NA    NA
    ## 658  80.6 150.5 292.1 126.4 299.8 139.6  606.6    NA 232.0  99.7    NA 332.9
    ## 659    NA 143.0 370.7    NA    NA    NA     NA    NA  60.5  35.0  31.9  23.6
    ## 660  40.4  33.4 104.6    NA 117.3  63.0     NA  96.8    NA 107.8  47.7    NA
    ## 661    NA    NA    NA    NA  25.2  51.3   51.5  32.8  52.6  30.9 308.5    NA
    ## 662  27.8   9.6    NA  53.8    NA  18.3   39.7    NA    NA    NA    NA    NA
    ## 663  31.6   8.3  13.6  16.4  37.1  14.4   70.6    NA  37.5  54.1    NA  10.5
    ## 664    NA  23.9  33.5    NA    NA    NA     NA    NA  31.2  74.8  82.1  32.3
    ## 665  58.1  48.9 147.2    NA  38.5  31.2     NA  29.1    NA  38.7  30.4    NA
    ## 666    NA    NA    NA    NA  79.4  60.8   38.4  24.7  33.8  34.2 165.8    NA
    ## 667  50.8  82.6    NA  35.7    NA  42.9   76.4    NA    NA    NA    NA    NA
    ## 668   8.2  26.7  20.0  52.0  25.1  14.3   40.7    NA  14.9  75.9    NA  22.9
    ## 669    NA  16.4  37.3    NA    NA    NA     NA    NA   0.6   0.1   1.3   0.6
    ## 670   1.6   0.1   0.3    NA   0.0   0.4     NA   0.2    NA   0.0   0.0    NA
    ## 671    NA    NA    NA    NA   0.4   0.0    1.0   2.0   0.3   2.1  21.6    NA
    ## 672   1.2  11.0    NA   4.5    NA   0.7    1.1    NA    NA    NA    NA    NA
    ## 673  42.0 113.2  31.9  34.2 126.9  74.6  185.6    NA   1.2 135.0    NA 115.1
    ## 674    NA   1.2  51.7    NA    NA    NA     NA    NA  21.6  28.6  67.1  53.2
    ## 675  14.7  56.9  12.3    NA  43.9  29.5     NA  60.4    NA  46.1  10.7    NA
    ## 676    NA    NA    NA    NA 187.0  52.5   31.4  89.7  65.4 128.4  76.5    NA
    ## 677  51.5  68.1    NA  49.6    NA  85.2   72.1    NA    NA    NA    NA    NA
    ## 678 100.1 166.5 144.8 103.2 200.3 156.1  323.9    NA 145.9 186.6    NA 210.9
    ## 679    NA 152.9 366.6    NA    NA    NA     NA    NA  27.6  84.6  36.0  23.0
    ## 680  28.2  17.2  48.7    NA  68.0  12.9     NA  39.3    NA  94.6  30.7    NA
    ## 681    NA    NA    NA    NA 165.3 177.5  127.9 153.3 219.7 122.4 495.4    NA
    ## 682  40.7  61.8    NA 184.5    NA  23.0  150.1    NA    NA    NA    NA    NA
    ## 683  51.6  42.5  80.3  87.1  69.2 136.6  441.2    NA  41.2  94.3    NA  75.9
    ## 684    NA  30.4  84.7    NA    NA    NA     NA    NA  31.3  35.9  49.4  19.6
    ## 685  24.4  25.0 189.2    NA  17.9  20.5     NA  18.6    NA  32.9  24.5    NA
    ## 686    NA    NA    NA    NA  16.7  18.2   34.1   0.0  13.5  11.9  62.4    NA
    ## 687  20.6  12.7    NA   4.7    NA   7.1    8.0    NA    NA    NA    NA    NA
    ## 688  19.2  32.3  30.6  50.4  42.7  11.5   35.0    NA  17.7  58.7    NA  29.5
    ## 689    NA  12.6  30.3    NA    NA    NA     NA    NA   0.0   0.0   0.0   0.0
    ## 690   0.0   0.0   0.0    NA   0.0   0.0     NA   0.0    NA   0.3   0.1    NA
    ## 691    NA    NA    NA    NA  75.9  41.8   34.7  77.5  38.3  56.2 155.7    NA
    ## 692  67.1  61.7    NA  47.5    NA 114.1   33.1    NA    NA    NA    NA    NA
    ## 693   0.0   2.8   0.4   0.0  32.8   0.0    0.0    NA   0.0   2.2    NA   1.5
    ## 694    NA   0.0   0.0    NA    NA    NA     NA    NA   0.0  12.3  46.5   0.0
    ## 695  11.5  23.1   1.2    NA   0.0   2.0     NA  29.7    NA    NA   1.7    NA
    ## 696    NA    NA    NA    NA  43.3  25.9   51.9  28.0  39.4  33.3  65.9    NA
    ## 697  83.4  79.8    NA  33.8    NA    NA   22.1    NA    NA    NA    NA    NA
    ## 698  17.9  41.2    NA  42.8    NA    NA   78.8    NA    NA    NA    NA    NA
    ## 699 252.0 285.6 392.0 193.5 402.6 145.4  811.4    NA 304.5 173.4    NA 251.0
    ## 700    NA    NA 667.1    NA    NA    NA     NA    NA 138.2 106.3  91.4  30.2
    ## 701 128.6 132.5 243.6    NA 126.5 134.1     NA  67.6    NA    NA  68.5    NA
    ## 702    NA    NA    NA    NA  50.0  38.4   13.5  28.7  92.6  35.9  72.3    NA
    ## 703  38.1  15.5    NA  36.7    NA    NA   37.6    NA    NA    NA    NA    NA
    ## 704   6.4  18.2  19.1  11.2  10.6  14.2   44.7    NA   6.9  27.0    NA   6.3
    ## 705    NA    NA  16.2    NA    NA    NA     NA    NA  97.8 137.6 135.6  94.7
    ## 706 145.0 127.2 536.3    NA  69.7 120.6     NA  58.6    NA    NA 151.6    NA
    ## 707    NA    NA    NA    NA 279.3 161.5  180.1 121.3 134.8 178.4 673.9    NA
    ## 708 125.4 204.5    NA  96.6    NA    NA  133.5    NA    NA    NA    NA    NA
    ## 709  90.2 179.3 117.1 100.6 140.0  72.8  118.3    NA  85.8 126.2    NA  84.4
    ## 710    NA    NA 148.1    NA    NA    NA     NA    NA  11.0   2.7   4.2   3.3
    ## 711   6.8   1.7   4.3    NA   1.0   6.0     NA   0.4    NA    NA   4.5    NA
    ## 712    NA    NA    NA    NA   0.6    NA    2.3   3.3   0.0   6.7   7.1    NA
    ## 713   0.0   0.0    NA   0.1    NA    NA    3.0    NA    NA    NA    NA    NA
    ## 714  87.3  43.0  54.1 102.2  58.4 105.8  240.7    NA  27.6  58.4    NA  33.7
    ## 715    NA    NA 101.8    NA    NA    NA     NA    NA  81.2  66.1  90.6 117.3
    ## 716  15.5  46.4  85.0    NA   0.0  11.4     NA  74.3    NA    NA   3.0    NA
    ## 717    NA    NA    NA    NA   9.3  44.3    6.8   9.3  15.8   0.9  19.2    NA
    ## 718   0.0   9.1    NA  12.3    NA    NA    0.0    NA    NA    NA    NA    NA
    ## 719 153.2 157.4 126.8 150.6 103.2  61.7  469.9    NA 189.0 134.5    NA 105.5
    ## 720    NA    NA 205.7    NA    NA    NA     NA    NA    NA  93.2  51.8  27.9
    ## 721  52.2  32.9 150.5    NA    NA  31.6     NA  24.8    NA    NA  88.7    NA
    ## 722    NA    NA    NA    NA   0.0   0.0    4.6   9.9   7.5   0.0  37.2    NA
    ## 723   9.1   0.0    NA   0.0    NA    NA    0.0    NA    NA    NA    NA    NA
    ## 724  26.2  21.5  14.9  27.8  13.8  72.3  258.6    NA  32.7  41.3    NA  18.2
    ## 725    NA    NA  28.7    NA    NA    NA     NA    NA   8.2  31.6   7.0  12.1
    ## 726  10.2  33.3 117.6    NA   8.3    NA     NA   7.9    NA    NA   4.2    NA
    ## 727    NA    NA    NA    NA  27.4  51.4   35.5  29.5  61.7  35.4  41.4    NA
    ## 728   9.1  34.6    NA  20.5    NA    NA   23.6    NA    NA    NA    NA    NA
    ## 729  21.9  57.8  93.2  87.8  79.9    NA  116.3    NA  41.2  39.3    NA  32.2
    ## 730    NA    NA  19.2    NA    NA    NA     NA    NA  11.5   3.9   2.0   3.8
    ## 731   4.7   0.4   3.8    NA    NA   6.0     NA   1.2    NA    NA   3.5    NA
    ## 732    NA    NA    NA    NA  11.2    NA   14.4   8.5  12.6  34.0  36.3    NA
    ## 733  20.6  72.3    NA   2.7    NA    NA   16.6    NA    NA    NA    NA    NA
    ## 734   0.0   0.0   0.0   0.0   0.0   8.7    0.0    NA   0.0   2.2    NA   3.2
    ## 735    NA    NA   0.0    NA    NA    NA     NA    NA  33.4  83.4 165.0 145.3
    ## 736  57.1  78.4 109.6    NA  43.1  29.1     NA  53.1    NA    NA  15.1    NA
    ## 737    NA    NA    NA    NA  73.1  63.1   49.8  92.8  39.3  79.6 175.1    NA
    ## 738  25.7  60.1    NA  67.2    NA    NA   87.7    NA    NA    NA    NA    NA
    ## 739  14.3   0.0    NA   6.4    NA    NA   15.8    NA    NA    NA    NA    NA
    ## 740  74.8  57.6 117.5  58.8  48.1  44.5  130.4    NA  65.3  87.3    NA  61.0
    ## 741    NA    NA 112.9    NA    NA    NA     NA    NA  68.2 182.7 240.3  87.7
    ## 742 138.8 136.4 292.7    NA 261.6  98.0     NA 107.3    NA    NA  99.6    NA
    ## 743    NA    NA    NA    NA 213.6 256.5  214.5 127.4 242.7  60.9 524.2    NA
    ## 744  73.7 135.9    NA 257.2    NA    NA  167.5    NA    NA    NA    NA    NA
    ## 745   4.7  15.2  10.3   8.0   0.0   8.0   59.5    NA  39.0  23.8    NA  15.7
    ## 746    NA    NA   5.8    NA    NA    NA     NA    NA  25.8  57.2  43.9  26.8
    ## 747  37.7  50.3 183.5    NA  38.1  51.1     NA  26.8    NA    NA  24.5    NA
    ## 748    NA    NA    NA    NA 139.6  37.8   19.6  43.6  43.1  45.2 231.7    NA
    ## 749  43.0 113.1    NA  42.1    NA    NA   41.6    NA    NA    NA    NA    NA
    ## 750   9.6  13.1  32.5  76.4  18.0  15.1   48.2    NA   7.5  14.3    NA  13.1
    ## 751    NA    NA  28.9    NA    NA    NA     NA    NA  45.6  15.0  21.5  40.9
    ## 752  27.6   9.1  34.7    NA  81.5    NA     NA  11.9    NA    NA  39.0    NA
    ## 753    NA    NA    NA    NA   5.7   8.3    9.4   4.3   5.4   3.0  49.5    NA
    ## 754  27.9  11.0    NA   6.9    NA    NA    1.4    NA    NA    NA    NA    NA
    ## 755   3.1   0.0   0.0   4.8   0.0   0.0    0.0    NA   0.0   4.8    NA   3.1
    ## 756    NA    NA   5.1    NA    NA    NA     NA    NA  87.1 143.2 142.4 107.8
    ## 757  19.8  64.9  10.1    NA   0.0  43.2     NA 178.5    NA    NA  30.9    NA
    ## 758    NA    NA    NA    NA 141.9  26.5   10.4  93.0  45.4  39.1 162.1    NA
    ## 759  34.0  30.9    NA  38.9    NA    NA   18.7    NA    NA    NA    NA    NA
    ## 760  31.3  28.3  39.5  31.2  49.7  22.7   75.5    NA  66.8  36.9    NA  36.7
    ## 761    NA    NA  98.8    NA    NA    NA     NA    NA 119.6 118.2 110.0  88.7
    ## 762  73.7  83.7 290.3    NA  79.8 102.1     NA  84.2    NA    NA  55.8    NA
    ## 763    NA    NA    NA    NA  36.1  90.1   60.8  43.9  91.7  32.9 206.2    NA
    ## 764  23.6   9.2    NA  57.7    NA    NA   63.5    NA    NA    NA    NA    NA
    ## 765  39.1  45.7  47.0  60.5  69.0 109.6  317.6    NA  54.1  62.2    NA  43.3
    ## 766    NA    NA  51.7    NA    NA    NA     NA    NA  65.8  97.0 101.0  53.1
    ## 767  51.1  43.9 267.9    NA  36.8  60.6     NA  67.3    NA    NA  67.2    NA
    ## 768    NA    NA    NA    NA    NA  13.5   12.4  14.9  13.4  26.6  47.2    NA
    ## 769  15.1  42.6    NA  17.5    NA    NA   19.5    NA    NA    NA    NA    NA
    ## 770  27.0  61.1  76.5  52.6  53.7  53.2   53.1    NA  33.4  18.6    NA  38.1
    ## 771    NA    NA  46.6    NA    NA    NA     NA    NA   4.3    NA   3.2   1.8
    ## 772   1.5   6.7  12.5    NA   0.0   0.9     NA   1.8    NA    NA   2.2    NA
    ## 773    NA    NA    NA    NA   0.0   0.9    2.5   1.8   1.9   0.6   6.4    NA
    ## 774   0.0   0.0    NA   3.4    NA    NA    1.6    NA    NA    NA    NA    NA
    ## 775  26.4   0.0   0.0   1.6   0.0   3.7   22.9    NA   0.4   2.1    NA  24.0
    ## 776    NA    NA   7.3    NA    NA    NA     NA    NA   0.0   0.0   0.0   0.0
    ## 777   0.0  28.8  20.5    NA   0.0   0.0     NA   0.0    NA    NA   0.0    NA
    ## 778    NA    NA    NA    NA 133.5  19.4   27.5  26.1  17.4  16.1 104.8    NA
    ## 779   2.2  32.0    NA  46.6    NA    NA   41.8    NA    NA    NA    NA    NA
    ## 780 132.6 158.8    NA    NA    NA    NA  175.1    NA    NA    NA    NA    NA
    ## 781  58.3  67.6  98.3  56.9 118.2  30.2  101.7    NA  89.2 112.0    NA    NA
    ## 782    NA    NA 343.8    NA    NA    NA     NA    NA  40.5  49.3  36.4  54.2
    ## 783  33.6  65.1 204.4    NA  62.0  45.2     NA    NA    NA    NA  23.8    NA
    ## 784    NA    NA    NA    NA 130.8 254.2  140.4 170.6 157.7  76.3 670.9    NA
    ## 785  65.5  98.9    NA    NA    NA    NA  184.3    NA    NA    NA    NA    NA
    ## 786  52.6  61.2  89.7 117.7  99.8 212.7  439.3    NA  57.7 105.1    NA    NA
    ## 787    NA    NA  82.6    NA    NA    NA     NA    NA  44.4  61.3  33.5  17.0
    ## 788  35.3  39.9 145.3    NA  17.4  16.7     NA    NA    NA    NA  38.2    NA
    ## 789    NA    NA    NA    NA  94.8  95.5   95.5  68.6  93.6  71.1 187.6    NA
    ## 790  48.9  52.0    NA    NA    NA    NA   78.5    NA    NA    NA    NA    NA
    ## 791  59.8 156.3 108.1 164.5  94.3  76.9  120.8    NA  51.3 107.6    NA    NA
    ## 792    NA    NA  66.8    NA    NA    NA     NA    NA   4.0    NA   9.4   7.3
    ## 793   6.4   7.3  14.3    NA   4.1  13.6     NA    NA    NA    NA   0.2    NA
    ## 794    NA    NA    NA    NA   5.0   3.1    1.0   0.8   2.1   0.6   0.3    NA
    ## 795   3.9   0.0    NA    NA    NA    NA    0.7    NA    NA    NA    NA    NA
    ## 796   0.0   0.0   0.0   0.0   0.0  20.0    0.0    NA   0.0   0.0    NA    NA
    ## 797    NA    NA   0.7    NA    NA    NA     NA    NA 125.2 104.2 216.1 222.9
    ## 798  50.6  77.2 293.4    NA  71.0 232.4     NA    NA    NA    NA  29.1    NA
    ## 799    NA    NA    NA    NA  46.1  22.6   34.0  15.4  18.7   8.5  20.8    NA
    ## 800   3.8  55.9    NA    NA    NA    NA   52.3    NA    NA    NA    NA    NA
    ## 801   8.1  78.1  18.5  30.0  91.9  20.2   79.5    NA  84.1   5.6    NA    NA
    ## 802    NA    NA  44.2    NA    NA    NA     NA    NA 191.6 295.2 197.6  99.7
    ## 803 237.6 201.7 482.6    NA 149.9 215.4     NA    NA    NA    NA 195.8    NA
    ## 804    NA    NA    NA    NA  89.9  96.3  104.5  95.7  98.2  58.9 293.1    NA
    ## 805    NA  54.8    NA    NA    NA    NA  114.3    NA    NA    NA    NA    NA
    ## 806 113.8  86.2 128.0  76.4 106.1 102.2  504.5    NA  76.2 248.6    NA    NA
    ## 807    NA    NA 114.5    NA    NA    NA     NA    NA  81.8  91.8  72.2  52.3
    ## 808  75.4  76.1 122.6    NA  35.9  62.9     NA    NA    NA    NA  40.7    NA
    ## 809    NA    NA    NA    NA  64.1  25.3   18.2  69.4  51.6  43.6  38.3    NA
    ## 810  17.4 100.1    NA    NA    NA    NA   36.8    NA    NA    NA    NA    NA
    ## 811   8.4  36.4  56.3  35.7  49.4  33.8   21.4    NA  26.3  43.7    NA    NA
    ## 812    NA    NA  31.9    NA    NA    NA     NA    NA  39.5  18.5  20.4  14.0
    ## 813  19.7  11.3  12.9    NA  25.8  51.9     NA    NA    NA    NA  52.8    NA
    ## 814    NA    NA    NA    NA  14.0   3.6   14.0  18.5  10.8  17.1  10.3    NA
    ## 815  15.4  65.6    NA    NA    NA    NA     NA    NA    NA    NA    NA    NA
    ## 816   0.0   0.0   0.0   0.0   0.0   0.0    7.4    NA   0.0   0.1    NA    NA
    ## 817    NA    NA    NA    NA    NA    NA     NA    NA  58.8 166.5 229.9 169.2
    ## 818  59.8 130.9 152.3    NA  62.5  62.9     NA    NA    NA    NA    NA    NA
    ## 819    NA    NA    NA    NA  96.6  44.5   21.0  11.1  47.9   3.1  11.2    NA
    ## 820  23.4  61.3    NA    NA    NA    NA     NA    NA    NA    NA    NA    NA

``` r
#homogsplit()
homogsplit("Ptest",1965,2005,2,39,0,0,3,ndec=2,gp = 4)
```

    ## Split areas and station map saved as Ptest_1965-2005-map.pdf 
    ## No further action required

    ## NULL
