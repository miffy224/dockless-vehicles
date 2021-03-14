# dockless-vehicles



# date: 

2020/03/11


# source: 

``` region_partition.ipynb ```

# purpose:

- 把free-floating資料(經緯)轉成virtual station(cell)，以及時段分區



# method:

假設將左上角視為原點，而這個矩形格點網路圖位於平面的第四象限，以最左上角的cell當成第(i,j)=(1,1)的cell，可得第(i,j)個cell的區域範圍, i=1,...,m, j=1,...,n；

假設第(i,j)格的編號為(i-1)*n+j, 如此第(1,1)格的編號為1；第(m,n)格的編號為mn,將所有資料的起訖座標重新轉換成cell的編號座標。

找出座標極值a,b,c,d，全體長寬加上預設dx,dy作為margin，再除m,n取得新的dx,dy。

<p>	m,i,Lon <p>
&nbsp;___________________<br />
|&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;|<br />
| a ------------- b |<br />
| |&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| |	<br />
| |&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| |n,j,Lat <br />
| |&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| | <br />
| c ------------- d | <br />
|___________________| <br />


* a(y_max, x_min)
* b(y_max, x_max)
* c(y_min, x_min)
* d(y_min, x_max)

# input file: 

```dockless-vehicles-7.csv```	------	清除 dockless-vehicles-6.csv 異常data

## 所用欄位：
  'StartLatitude','StartLongitude','EndLatitude','EndLongitude'

# parameter:

- x_min, x_max, y_min, y_max	------	座標極值

- m, n	------	x,y軸各切割成m,n等分
- dx, dy	------	單位cell 長寬

- pos_1(x_min - dx/2, y_max + dy/2)	------	左上點座標

- pos_mn(x_max + dx/2, y_min - dy/2)	------	右下點座標

- k	------	cell 編號


# output file: 
	
```index_50*50.csv```	------	印出 n,m,dx,dy,總period數，全部cell之number(k),i,j,中心x,y之WebMercator座標與經緯度（WGS84）
	
```OD_region&period.csv```	------	轉換結果(TripID, StartCell, EndCell, StartPeriod, EndPeriod)


# note:

1. it took too long in python, so cython is included in this code.

2. pyproj (https://pyproj4.github.io/pyproj/stable/)
The pyproj is a Python package that performs cartographic transformations and geodetic computations. 

==============================================



# date: 

2020/02/16


# source: 

```dockless-vehicles-mapping.ipynb```

# purpose:

	用 folium 套件在地圖上可視化某一日 OD 及 TripDuration

# input file: 

```dockless-vehicles-6.csv```

## 所用欄位：
'StartDate',<br />
    'StartLatitude',<br />
    'StartLongitude',<br />
    'EndLatitude',<br />
    'EndLongitude',<br />
    'TripDuration'

# parameter:

date ------ '2019/8/3'

# output file: 
	
```dockless-vehicles.html```







