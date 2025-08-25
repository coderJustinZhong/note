
```
https://sales-tac.hkbn.net/upsale
```

# ipad 密碼Upsellapp20258
1652756983323
## 舊場：

地址:https://mdmstage.hkbn.net/mifs/login.jsp
賬號密碼:itadgz / cmV99Tco

## 新場：
地址:https://hkbnuat.jamfcloud.com/
賬號密碼:ITDS-UAT / 4II@kRd8xenhV6~TKKqg

## upsalseApp代码仓库
地址:gitlab.com/hkbn-itad-app2
## upsalseApp测试账号
ittest / ittestc
密码1234567


# 上線操作:

## 前端

## 项目地址

> 项目地址：https://gitlab.com/hkbn-itad-app2
> 新更新地址,改成[Summary - Overview](https://dev.azure.com/HKBN-ITDS/Upsell%20App)
>
> 先翻墙或者入HKRDS注册一个账号，再稳 johnny拉入项目

公司gitleb个人账号:justin.chung@cs.hkbn.com.hk 密码:a86175310

## 编译项目

理论上git clone下来，npm install下就ok，不过新版本M1安装好似有兼容性问题，要修改部分node_modules里的文件先不会报错（具体可以百度）,

或者可以直接解压 `upsellApp.assert/example/node_modules.zip` 使用



##  运行模拟器

主界面输入sales的账号密码，UAT场可以通过以下sql获取：

```
pda_admin -> SELECT * FROM PDA_USER

ITTEST/1234567
ITTESTC/1234567 -> 这个账号可以CPE II
```
![img.png](image/img.png)

PPS登录界面，真实环境下要核对last name & first name：

![img_1.png](image/img_1.png)

开发模式只需要关注这三项就可以（*command* + D），开启debug后，可以在弹出的页面看console log
![img_3.png](image/img_3.png)
![img_4.png](image/img_4.png)


主界面：

左边Upsell这个选项目前来说已经没plan可以选的了（BPM抽走了）

![img_5.png](image/img_5.png)


## 打包 ipa文件（UAT/UAT2/LIVE）

切換到相關分支

```
// 僞代碼
git checkout uat
```

### 更改版本號

分別修改以下四個文件：

![img_6.png](image/img_6.png)

### 選擇相關的版本

![img_7.png](image/img_7.png)
### 打包

![img_9.png](image/img_9.png)
![img_10.png](image/img_10.png)
等他build完之後會彈出以下窗口：

![img_12.png](image/img_12.png)
![img_15.png](image/img_15.png)
最後導出文件即可

![img_16.png](image/img_16.png)

## 上傳UAT MDM

準備好上一個步驟打包出來的相關 ipa 文件

### 舊場

https://mdmstage.hkbn.net/mifs/login.jsp

如果版本**已經存在**，要先刪除了舊版再上傳

>賬號密碼:itadgz / cmV99Tco

![img_17.png](image/img_17.png)
點擊 Apps -> Add+

![img_18.png](image/img_18.png)
這裏選擇in house, 上傳相關的ipa，然後後面的步驟**全部默認**按next就行了

![img_19.png](image/img_19.png)
為新上傳的app添加相關的lable

![img_20.png](image/img_20.png)
![img_22.png](image/img_22.png)

### 新場

https://hkbnuat.jamfcloud.com/
>賬號密碼：ITDS-UAT / zmiCDZYNL$54

jamf市場下載地址[https://hkbnuat.jamfcloud.com/enroll](https://hkbnuat.jamfcloud.com/enroll "https://hkbnuat.jamfcloud.com/enroll")


如果存在，直接替換ipa文件就可以了，比較方便

![img_11.png](image/img_11.png)

![img_13.png](image/img_13.png)
![img_21.png](image/img_21.png)
如果沒有則重新添加

![img_23.png](image/img_23.png)
![img_24.png](image/img_24.png)
![img_25.png](image/img_25.png)
![img_26.png](image/img_26.png)

## 交Form上綫

### 1 - 導出ipa文件

創建文件夾 `yyyy.mm.dd spp_upsale_x.x.x context `， 複製ipa、icon、excel文件到文件夾内。

icon和excel文件參考目錄下 `./upsellApp.assets/example/2022.05.10 spp_upsale_1.9.8 free to go AXA` 文件夾

![img_27.png](image/img_27.png)
### 2 - 修改excel并打包zip包

修改 `Program Launch Fm (121225)(2011ITADGZ1992.xlsx` 文件下對應的版本號以及日期

![img_28.png](image/img_28.png)
最後打包成zip包



### 3 - 填launch form

前端參照：https://elite.hkbn.com.hk/hkbn?id=form&table=change_request&sys_id=fcd6a4aadbd3c154c8649c6dd39619d1&view=sp

後端參考:[form - HKBN Service Portal](https://elite.hkbn.com.hk/hkbn?id=form&table=change_request&sys_id=3d44b45adb726d508bdda51fd39619c7&view=sp)

我的地址:https://elite.hkbn.com.hk/hkbn?id=hkbn_my_change_requests

![img_29.png](image/img_29.png)
![img_30.png](image/img_30.png)
![img_31.png](image/img_31.png)

### 4 - 更新版本
-   接遠程通過PMP然後搜索192.168.92.103,ssh連接
-   修改對應文件内的版本號以及日期：

`vim /home/spp/spp_ipad_sales/build/upsell/app_version.json`

![img_32.png](image/img_32.png)
![img_33.png](image/img_33.png)
### 5 - 将live包上传到UAT MDM




## LIVE debug

這個版本會跳過customer 姓名驗證，直接輸入pps就可以login進去，方便綫上出問題可以調試，**注意不要在這個版本上落單（真實LIVE環境）**

![img_34.png](image/img_34.png)


## Profile過期

打包app要用profile， gen一次有效期一年，profile過期的話只app就用唔到

所以要係過期之前從新gen過一個新的（穩johnny gen然後導入xcode），然後用新profile打包launch只app

! apple账号不对开发使用了，起profile要问johnny tong

![img_35.png](image/img_35.png)

## DR drill

### 准备一个mita版本的app

合并 `mita` 分支到你的新分支，然后打包

> https://gitlab.com/hkbn-itad-app2/spp_upsale_app/-/tree/mita



### 上传到UAT场的MDM

DR drill开始的时候，可以上传mita版app到uat mdm上等user试



### 上传正常版本的app

DR drill结束的时候，上传正常live版app到uat mdm上等user试



# 后端

## 项目地址

>https://gitscm.hkbn.com.hk/mobile/spp_upsale_server



## 入口

后端主要行落单flow以及http api调用

retention入口API ->  `/api/ret/submitOrder` ，对应类： RetSubmitOrderController

upsell II 入口API -> `/api/submitOrder` ，对应类：SubmitOrderController



## 查看 SCRIBE 日志

### UAT

```
192.168.233.193  	
cd /home/scribe_log/salesipad/salesipad_upsell_log
```



### PROD

```
192.168.232.154
cd /home/scribe_log/salesipad/salesipad_upsell_log
```


## 查看jenkins
[spp_upsale_server [Jenkins] (hkbn.com.hk)](http://uatjenkins.hkbn.com.hk:8080/job/spp_upsale_server/)


## 查看 weblogic console


新UAT控制台:[Oracle WebLogic Server 管理控制台](https://192.168.233.193:17002/console/login/LoginForm.jsp)
賬號/密碼 weblogicuser/weblogicuser123

PROD: http://192.168.232.93:7001/console/login/LoginForm.jsp
賬號/密碼 weblogicviewer/ITAD1234


## 重啟weblogic

![img_36.png](image/img_36.png)
這種情況是死了,需要重啟



`aio` ->  AIO_RENEW_API01

`upsellApp` -> new_ManagedServer_cpe_1



## 行LIVE sql

```
script prod server -> 232.185 

cd /u01/wip/online_script
vi data1.sql
ant check1
vi test1.csv
```

或者

```
233.137

# pda
sqlplus hkbn_acq/itadgz@(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=x06p-scan.hkbn.com.hk)(PORT=2521))(CONNECT_DATA=(SERVER=DEDICATED)(SERVICE_NAME=WWWC)))

# pda admin
sqlplus pdaadmin/pdaadmin@(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=x06p-scan.hkbn.com.hk)(PORT=2521))(CONNECT_DATA=(SERVER=DEDICATED)(SERVICE_NAME=WWWC)))
```



# 落單流程

![img_37.png](image/img_37.png)
或者使用[語雀](https://www.yuque.com/)導入 `./upsellApp.assets/example/submit order flow/submit flow.lakeboard` 文件查看


# 在sql查看plan

![img_38.png](image/img_38.png)
### UAT1
```
jdbc:oracle:thin:@(DESCRIPTION =  (ADDRESS_LIST =  (ADDRESS = (PROTOCOL = TCP)(HOST = RESJU01.hkbn.com.hk)(PORT = 1630))  (ADDRESS = (PROTOCOL = TCP)(HOST = x06d02-vip.hkbn.com.hk)(PORT = 1527)))(SOURCE_ROUTE = yes) (CONNECT_DATA =  (SERVICE_NAME = OMUAT)))
```

### UAT2
```
jdbc:oracle:thin:@(DESCRIPTION = (ADDRESS_LIST = (ADDRESS = (PROTOCOL = TCP)(HOST = RESJU01.hkbn.com.hk)(PORT = 1630))(ADDRESS = (PROTOCOL = TCP)(HOST = x09d02-vip.hkbn.com.hk)(PORT = 1542)))(SOURCE_ROUTE = yes) (CONNECT_DATA =(SERVICE_NAME = OMUAT2)))
```


>OMUAT1賬號密碼:hkbn/bn1506hk
>OMUAT2賬號密碼:CALL_MENU/aNnS3kB6oEgQbVHR
```
SELECT * FROM RET_SERV_LIST WHERE HAS_FUTURE = 'N' AND SERVICE_TYPE = 'AS'
```
```
select * from ret_serv_list where service_type = 'AS' and main_bundle_setting in ('SH','SW')
```


# 查看log
## live
>ip:192.168.232.154   賬號/密碼 app_user/scR5rBJFYzsjTDOhC

![img_39.png](image/img_39.png)
![img_40.png](image/img_40.png)
``` 
cd ../scribe_log/salesipad/salesipad_upsell_log/
```
``` 
//列出所有文件
ll
```
![img_41.png](image/img_41.png)
```
// less +文件名打開文件
less salesipad_upsell_log-2022-07-01_00000
```
```
// 搜索500得關鍵字
/500
```
```
U上一個N下一個G最上gg最下
```
或者
```
less ../scribe_log/salesipad/salesipad_upsell_log/salesipad_upsell_log_current 
```
## LOG 搜索關鍵字眼  &滾動更新log
cd到salesipad_upsell_log文件下 /home/scribe_log/salesipad/salesipad_upsell_log
```
grep -rn "搜索的字眼" *
```
```
tail -f salesipad_upsell_log_current
```

```
 tail -f salesipad_upsell_log-2022-07-01_00000
```
## MANGO DB 查log
```
use itds_applog_business
db.getCollection("spp_upsale_server").find({'env':'uat','time':{'$gte':new Date(2023,4,11),'$lte':new Date(2023,4,12)}},{'message':1,'time':1,'env':1})
```

![img_42.png](image/img_42.png)
## 內部系統查LOG
uat:[Search Log - Search (hkbn.com.hk)](http://uatsystem-log.hkbn.com.hk/)
live:[Search Log - Search (hkbn.com.hk)](http://system-log.hkbn.com.hk/)

![img_43.png](image/img_43.png)

![img_44.png](image/img_44.png)

# 查看first name 同last name
[https://res.hkbn.com.hk](https://res.hkbn.com.hk/)

https://resuat2.hkbn.com.hk/
```bnuser4/Foxso1234```

![img_45.png](image/img_45.png)

![img_46.png](image/img_46.png)
[Callmenu (hkbn.com.hk)](https://business.osapps.hkbn.com.hk/callmenu-ui/?pps=724282690)

![img_47.png](image/img_47.png)

# OPEN SHIFT
地址：[https://console-openshift-console.apps.os4apps.hkbn.com.hk/topology/ns/uat-itds-business?view=list](https://console-openshift-console.apps.os4apps.hkbn.com.hk/topology/ns/uat-itds-business?view=list "https://console-openshift-console.apps.os4apps.hkbn.com.hk/topology/ns/uat-itds-business?view=list")
账号密码：uat-itds-business-admin YqPQvN0YzrlqmFXE5E4a

# 賬號過期
[https://uatadmipad.hkbn.net/spp_pda_admin/login.jsp](https://uatadmipad.hkbn.net/spp_pda_admin/login.jsp "https://uatadmipad.hkbn.net/spp_pda_admin/login.jsp")

[admipad.hkbn.net/spp_pda_admin/login.jsp](https://admipad.hkbn.net/spp_pda_admin/login.jsp)
```賬號sharon密碼sharon```
### uat場 [192.168.237.147/spp_pda_admin/login.jsp](http://192.168.237.147/spp_pda_admin/login.jsp "http://192.168.237.147/spp_pda_admin/login.jsp")

### live場 [acqmenu.apps.os4apps.hkbn.com.hk/spp_pda_admin/login.jsp](https://acqmenu.apps.os4apps.hkbn.com.hk/spp_pda_admin/login.jsp)

![img_48.png](image/img_48.png)
DB直接更新賬號

![img_49.png](image/img_49.png)
select *** from pda_user where *upper*(USER_ID) = *upper*('ittest');

select *** from pda_user where *upper*(USER_ID) = *upper*('ittestc');

update pda_user set PWD_DATE = *sysdate* where *upper*(USER_ID) = *upper*('ittestc');

# 實時睇upsellapp back end log


```
cd /u01/Oracle/Middleware/user_projects/domains/hkbn_base_domain/servers/new_ManagedServer_cpe_1/logs 
```
```
tail -f new_ManagedServer_cpe_1.out
```
![img_50.png](image/img_50.png)

## pdf server
cljp01 - 192.168.235.183

itds_app01

192.168.232.185

itadgz

b8Q82L9MQCGlijxhsk

du -sh *也会列出当前文件夹下所有文件对应的大小

## 修改apache
PMP搜索192.168.92.104這臺機



![img_51.png](image/img_51.png)
進入后使用

`cd /etc/httpd/conf.d `

`sudo vim ssl.conf`

![img_52.png](image/img_52.png)


![img_53.png](image/img_53.png)
修改
```
<Proxy balancer://ocp4UpsaleAppcluster2>                                   BalancerMember https://uat-business.osapps.hkbn.com.hk/upsale2         </Proxy> 
```

```
<Location "/upsale3">                                               
    ProxyPass balancer://ocp4UpsaleAppcluster3                         
    ProxyPassReverse balancer://ocp4UpsaleAppcluster3                 
</Location>
```

然後使用下面命令重啓

```
sudo systemctl restart httpd
sudo systemctl restart httpd.service
```

# COUCH BASE CONSOLE
<http://192.168.237.20:8091/index.html#sec=analytics&statsBucket=%2Fpools%2Fdefault%2Fbuckets%2Folsso%3Fbucket_uuid%3D61ab62157f142a3b1b691d89f23eb6be>

![img_54.png](image/img_54.png)

![img_55.png](image/img_55.png)
# 上openshift
## ## jenkins 新建項目

![img_56.png](image/img_56.png)

從別的複製過來
![img_57.png](image/img_57.png)
改參數

![img_58.png](image/img_58.png)

![img_59.png](image/img_59.png)
![img_60.png](image/img_60.png)
創建docker 跟K8S文件

![img_61.png](image/img_61.png)
push上去后人手build

## Azure
[Azure DevOps Services | Sign In](https://spsprodsea1.vssps.visualstudio.com/_signin?realm=dev.azure.com&reply_to=https%3A%2F%2Fdev.azure.com%2FHKBN-ITDS%2FUpsell%2520App&redirect=1&hid=d6aca2dc-9b22-4835-96f8-b352142852c1&force=1&context=eyJodCI6MiwiaGlkIjoiM2EyOTAzYmQtZGRkYy00ZTQyLTgwZGYtMWVkOGQwOTM2NjhhIiwicXMiOnt9LCJyciI6IiIsInZoIjoiIiwiY3YiOiIiLCJjcyI6IiJ90&prompttype=NoOption#ctx=eyJTaWduSW5Db29raWVEb21haW5zIjpbImh0dHBzOi8vbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbSIsImh0dHBzOi8vbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbSJdfQ2)

