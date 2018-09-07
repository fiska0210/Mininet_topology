# Mininet Manager

## 0. Prerequisite
* Mininet
* RYU Controller
* crayons
* networkx
* numpy
* cython


### Environment
Ubuntu 16.04.3 LTS (GNU/Linux 4.10.0-28-generic x86_64)
RAM info : 31 GiB
CPU info : Intel(R) Xeon(R) CPU E5-2620 v3 @ 2.40GHz

### Install
#### Install Mininet
［ 注意 ］Mininet執行的時候需要<font color="red">sudo權限</font>！

如果沒有安裝git : sudo apt-get install git-all
```
$ git clone git://github.com/mininet/mininet
```
預設是-a，安裝Mininet所有功能
-h 可列出所有可用選項
-s mydir 可指定安裝資料夾，需放在所有選項的最前面
```
$ sudo ./mininet/util/install.sh -a
```
嘗試傳送封包以測試是否完成安裝
```
$ sudo mn --test pingall 
```

#### Install RYU Controller
先安裝一些RYU Controller需要的Python套件
```
$ sudo apt-get update
$ sudo apt-get install autoconf binutils bison build-essential ccache flex gawk gettext git libncurses5-dev libssl-dev ncurses-term quilt sharutils subversion texinfo xsltproc zlib1g-dev libxml2-dev libxslt1-dev
$ sudo apt-get install python-pip 
$ sudo apt-get install python-dev
$ sudo apt-get install python-eventlet
$ sudo apt-get install python-routes
$ sudo apt-get install python-webob
$ sudo apt-get install python-paramiko
$ sudo apt-get install python-essential
$ sudo apt-get install python-gevent
```
使用pip安裝RYU並更新pip套件
```
$ sudo pip install ryu
$ sudo pip install six --upgrade
```
下載source code及libraries
```
$ sudo git clone git://github.com/osrg/ryu.git
$ sudo python ./setup.py install
$ sudo pip install flask
$ sudo pip install gevent-websocket
```
嘗試啟動RYU以測試是否完成安裝
```
$ ryu-manager
```
![](https://i.imgur.com/PULJ3Hm.png)


#### Install crayons
```
pip install crayons
```
#### Install networkx
```
pip install networkx
```
#### Install numpy
```
sudo apt-get install python-numpy
```
#### Install cyphon
```
sudo apt-get install cython
sudo python setup.py build_ext --inplace
```

#### Clone the project
要clone在mininet的資料夾裡（home/username/mininet）
```
$ sudo git clone https://github.com/denny60004/Mininet_simulator.git
```



## 1. Setup Graph
* 方法一：使用graph generator
執行"Example.py"
```
$ cd src 
$ sudo python Example.py
```
原始設定為：
![](https://i.imgur.com/Ykb91eE.png)
使用者可以依據需求，更改以下三個地方：
layerNum：graph層數
layerNodeNum：每層的節點數目
conPara：相隔兩層之間的link數量（ex:"1,1":15 第一層裡有15條link,"1,2":23 第一層與第二曾之間有23條link）

* 方法二：使用者依照指定格式自行產生
使用方法一執行完Example.py後會生成一個csv檔案，如下所示：
```
## Created at 2018-09-03 22:54:46
# Connection parameters.
# Layer1-1:15 Layer1-2:23 Layer2-2:35 Layer2-3:6
# Layer3-3:6 Layer3-4:1 Layer4-4:8
# Connection Num.
# Layer1-1:7 Layer1-2:2 Layer2-2:0 Layer2-3:0
# Layer3-3:0 Layer3-4:0 Layer4-4:0
# Lowest level starting ID, total router number
8,10
# NodeID, x_pos, y_pos, degree
0,-8665,4122,3
1,-9103,2983,3
2,-7400,4078,2
3,-8128,2840,2
4,-9948,4477,1
5,-9915,1940,1
6,-150,5492,2
7,-4325,-2290,2
8,-145,5481,1
9,-4322,-2304,1
# links
0,1
0,2
1,3
0,4
1,5
2,6
3,7
6,8
7,9
c
```
如果沒有特殊需求，建議使用方法一來作為graph的產生方法。

## 2. Start Mininet Network
step 1：用Mininet Manager 啟動network
```
$ sudo python switch_topology.py
```
step 2：使用xterm 開啟controller節點
```
mininet＞ xterm c0
```
xterm：c0
```
$ sh all.sh
```
若沒有權限，請執行：
```
$ sudo chmod -x all.sh
```
step 3：稍等大約一分鐘後，使用pingall測試network是否connect完成，若有dropped的話，則再pingall一次直到成功。
```
mininet＞ pingall
```
![](https://i.imgur.com/HSDCNCr.png)
可以開始進行想要的網路模擬！

## 3. 結束Mininet模擬並清除資料

結束Mininet模擬
```
mininet＞ exit
```
清除所有關於Mininet的暫存資料（每次結束都必需clean up，不然下次執行會有error）
```
$ sudo mn -c
```
