# API Moringa - Front End Functions

![](https://img.shields.io/github/release/pandao/editor.md.svg)

## URL-URL untuk email OTP
### URL untuk email member pending (welcome email) : https://moringaku.id/tools/aktivasi?code={hash}
### URL untuk email aktivasi akun (member active) : https://moringaku.id/tools/aktivasi?code={hash}

### Jenis OTP 1 : URL Ganti password : https://moringaku.id/tools/password?code={hash}
### Jenis OTP 2 : URL Ganti profile  : https://moringaku.id/tools/profile?code={hash}
### Jenis OTP 3 : URL Update Warisan : https://moringaku.id/tools/warisan?code={hash}
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
| Result | INT| Y | 0 = OK; 1 = Error |
| Message| STRING | N | error message |

#
##### - Sample call:
###### Change Password 
```sh
    data: 
    {
        "memberid": 12.
        "jenisotp":1,
        "data":
        {
            "nexturl" : "https://moringaku.id/tools/password?code=ABCDEFGH"
            
        }
    }
    
```

#
##### - Sample call:
###### Change Profile 
```sh
    data: 
    {
        "memberid": 12.
        "jenisotp":2,
        "data":
        {
            "nexturl" : "https://moringaku.id/tools/profile?code=ABCDEFGH",
            "nomornpwp": "711501718439000",
            "namawpajak": "pian", 
            "alamatwpajak" : "Sopian",
            "nomorac": "8330059568",
            "namaac" : "Rini Purnamasari",
            "namabank" : "BCA2",
            "cabangBank" : "Jakarta",
            "email" : "storialika@gmail.com",
            "hideemail" : 1,
            "telepon" : "083804649937",
            "hidephone" : 1,
            "whatsapp" : "083804649937",
            "hidewa" : 1            
        }
    }
    
```

##### Sample response:
###### Success Response
```sh
{
    "result": 0,
    "message": ""
}
```
#

### 2. /CheckOTP 
#### - Check OTP apakah masih valid
- Sender : **PHP**
- Target : **Engine**
- Note : untuk target URL Heksa  selama UAT menggunakan : "http://103.58.146.64/heksaecommerce/beli/repayment?trxid=153689959640413612&refid=moringaku" 
        


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| HashCode | STRING | Y | data hash yg dikirim ke email nasabah |


#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT | Y | 0 = OK; 1 = Error |
| Expired | INT| Y | 0 = Active; 1 = Expired |
| MemberId | INT | Y | member id (trxid) |
| UserName | STRING | Y | nama member |
| JenisOTP | INT | Y | 1 = Aktivasi Akun |
|||| 2 = Change Password |
|||| 3 = Change Profile |
|||| 4 = Change Warisan |
|||| 5 = Change user id |
|||| 6 = proses pembayaran setelah dapat welcome email |
| data | JSON | N | data temporary jika ada | 
| Message| STRING | N | error message |

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
        "hashcode":"5D89006A21776A45E050A8C04E0A33D8"
    }
    contentType: "application/json; charset=utf-8",
    success : function(response) {
      console.log(response);
    }
  });
```

##### Sample response:
###### Success Response aktivasi akun JenisOTP 1
```sh
{
    "result": 0,
    "expired": 0,
    "memberid": 61,
    "username": "Rini Purnamasari",
    "jenisotp": 1,
    "data" :
    {
        "nexturl" : "",
        
    }
    "message" : ""
}
```
###### Success Response Proses pembayaran JenisOTP 6
```sh
{
    "result": 0,
    "expired": 0,
    "memberid": 61,
    "username": "Rini Purnamasari",
    "jenisotp": 6,
    "data" :
    {
        "nexturl" : "https://heksainsurance.co.id/heksaecommerce/beli/repayment?trxid=153689959640413612&refid=moringaku"
        
    }
}
```
#

### 3. /UpdateData 
#### - Update data temporary yang disimpan waktu CreateOTP
- Sender : **PHP**
- Target : **Engine**


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| MemberId | INT | Y | MemberId  |
| HashCode | STRING | Y | hashcode OTP yg mau di konfirmasi |



#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = OK  |
|||| 1=Not-OK |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/UpdateData",
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
| MemberId | INT | Y | MemberId |
| UserId | STRING | N | New User ID , tidak diisi jika ganti password saja/reset pwd|
| Pwd | STRING | Y | New Password |


#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = OK; engine update database |
|||| 1 = NOT-OK |
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
#### Untuk Check userid saat pilih userid di page aktivasi 
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
|||| 1 = sudah terpakai / error |
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
    "result": 1,
    "message": "already used",
}
```
#


### 6. /UpdateBeneficiary
#### - update data warisan 
#### Untuk ganti warisan saat aktivasi awal
- Sender : **PHP**
- Target : **Engine**


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| memberid | INT | Y | member id |
| benname | STRING | Y | nama ahli waris | 
| benktp | STRING | Y | KTP |
| bendob | STRING | Y | DOB dd/mm/yyyy |
| bengender | INT | Y | 0 = pria; 1 = wanita | 
| benemail | STRING | Y | email |
| benphone | STRING | N | phone |
| benrelation | INT | N | 0 = Suami; 1 = Istri; 2 = Anak; 3 = kakak; 4 = adik |



#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = tidak terpakai |
|||| 1 =  error |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/UpdateBeneficiary",
    dataType: "json",
    type : "POST",
    data: 
    {
        "memberid": 21,
        "benname" : "ahmad zakhri",
        "benktp" : "1234567890",
        "bendob" " "19/02/2019",
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
    "result": 1,
    "message": "error",
}
```
#


