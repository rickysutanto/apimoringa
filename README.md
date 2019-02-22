# API Moringa - Front End Functions

![](https://img.shields.io/github/release/pandao/editor.md.svg)

## URL-URL untuk email OTP
### URL Cek pembayaran saat aktivasi : https://moringaku.id/tools/aktivasi?code={hash}
### URL Aktivasi akun : https://moringaku.id/tools/aktivasi?code={hash}
### URL Update Warisan : https://moringaku.id/tools/warisan?code={hash}
### URL Ganti password : https://moringaku.id/tools/password?code={hash}
### URL untuk OTP yang di konfirmasi member : https://moringaku.id/tools/otp?code={hash}
#

### 1. /CreateOTP 
#### - Buat OTP baru untuk dikirim ke member
- Sender : **PHP**
- Target : **Engine**

#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| MemberId | INT | Y | member id = id di table members |
| JenisOTP | INT | Y | Jenis OTP |
|||| 1 = Change Password |
|||| 2 = Change Profile |
|||| 3 = Change Warisan |
| data | JSON | N | Data temporary |

#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = OK; -1 = Error |

#
##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/CreateOTP",
    dataType: "json",
    type : "POST",
    data: 
    {
        "memberid": 12.
        "jenisotp":1,
        "data":
        {
            "url" : "https://moringaku.id/tools/password?code=ABCDEFGH"
            
        }
    }
    contentType: "application/json; charset=utf-8",
    success : function(response) {
      console.log(response);
    }
  });
```

##### Sample response:
###### Success Response
```sh
{
    "result": 0,
}
```
#

### 2. /CheckOTP 
#### - Check OTP apakah masih valid
- Sender : **PHP**
- Target : **Engine**


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| HashData | STRING | Y | data hash yg dikirim ke email nasabah |


#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT | Y | 0 = OK; -1 = Error |
| Expired | INT| Y | 0 = Active; -1 = Expired |
| MemberId | INT | Y | member id (trxid) |
| UserName | STRING | Y | nama member |
| JenisOTP | INT | Y | 1 = Aktivasi Akun |
|||| 2 = Change Password |
|||| 3 = Change Profile |
|||| 4 = Change Warisan |
|||| 5 = Change user id |
| data | JSON | N | data temporary jika ada | 
#

##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/CheckOTP",
    dataType: "json",
    type : "POST",
    data: 
    {
        "hashdata":"5D89006A21776A45E050A8C04E0A33D8"
    }
    contentType: "application/json; charset=utf-8",
    success : function(response) {
      console.log(response);
    }
  });
```

##### Sample response:
###### Success Response
```sh
{
    "result": 0,
    "expired": 0,
    "memberid": 12,
    "username": "Ahmad fikri",
    "jenisotp": 1,
    "data" :
    {
        "nexturl" : "https://moringaku.id/tools/payment?memberid=12&trxid=134567889",
        
    }
}
```
#

### 3. /UpdateData 
#### - Permintaan ganti Password oleh Member
- Sender : **PHP**
- Target : **Engine**


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| MemberId | INT | Y | MemberId  |
| HashData | STRING | Y | hashcode OTP yg mau di konfirmasi |



#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = OK  |
|||| -1=Not-OK |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/ChangePwd",
    dataType: "json",
    type : "POST",
    data: 
    {
        "memberid": 15,
        "hashcode":"ABCDEWFGH1234567890"
    }
    contentType: "application/json; charset=utf-8",
    success : function(response) {
      console.log(response);
    }
  });
```

##### Sample response:
###### Success Response
```sh
{
    "result": 0,
    "message": "success",
}
```
#



### 4. /ChangeIdPwd
#### - Change ID & Pwd Member saat aktivasi
- Sender : **PHP**
- Target : **Engine**


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| MemberId | STRING | Y | MemberId = TrxId |
| User ID | STRING | Y | New User ID |
| Pwd | STRING | Y | New Password |


#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = OK; engine update database |
|||| -1 = NOT-OK |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/ChangeIdPwd",
    dataType: "json",
    type : "POST",
    data: 
    {
        "memberid" : 15,
        "userid" :  "iksan0201"
        "pwd" : "3220102910",
    }
    contentType: "application/json; charset=utf-8",
    success : function(response) {
      console.log(response);
    }
  });
```

##### Sample response:
###### Success Response
```sh
{
    "result": 0,
    "message": "success",
}
```
#


### 5. /CheckID 
#### - Check userid sudah terpakai / belum. 
#### Untuk ganti userid saat aktivasi awal
- Sender : **PHP**
- Target : **Engine**


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| UserId| STRING | Y | userid yg mau diperiksa |


#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = tidak terpakai |
|||| -1 = sudah terpakai / error |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/CheckID",
    dataType: "json",
    type : "POST",
    data: 
    {
        "userid":"kodokbuduk"
    }
    contentType: "application/json; charset=utf-8",
    success : function(response) {
      console.log(response);
    }
  });
```

##### Sample response:
###### Success Response
```sh
{
    "result": -1,
    "message": "already used",
}
```
#


### 6. /UpdateBeneficiary
#### - Check userid sudah terpakai / belum. 
#### Untuk ganti userid saat aktivasi awal
- Sender : **PHP**
- Target : **Engine**


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| memberid | INT | Y | member id |
| benname | STRING | Y | nama ahli waris | 
| benktp | STRING | Y | KTP |
| bendob | STRING | Y | DOB yyyymmdd |
| bengender | INT | Y | 0 = pria; 1 = wanita | 
| benemail | STRING | Y | email |
| benphone | STRING | N | phone |
| benrelation | STRING | N | 0 = Suami; 1 = Istri; 2 = Anak; 3 = kakak; 4 = adik |



#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = tidak terpakai |
|||| -1 = sudah terpakai / error |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/CheckID",
    dataType: "json",
    type : "POST",
    data: 
    {
        "memberid": 21,
        "benname" : "ahmad zakhri",
        "benktp" : "1234567890",
        "bendob" " "19720811",
        "bengender" : 0,
        "benemail" : "ahmad@email.com",
        "benphone" : "0819929919091",
        "benrelation" : 2
        
    }
    contentType: "application/json; charset=utf-8",
    success : function(response) {
      console.log(response);
    }
  });
```

##### Sample response:
###### Success Response
```sh
{
    "result": -1,
    "message": "error",
}
```
#


