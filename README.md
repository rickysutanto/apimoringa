# API Moringa - Front End Functions

### URL-URL untuk email OTP
#### URL untuk email member pending (welcome email) : https://moringaku.id/tools/aktivasi?code={hash}
#### URL untuk email aktivasi akun (member active) : https://moringaku.id/tools/aktivasi?code={hash}
#

### 1. /CreateOTP 
#### - Buat OTP baru untuk dikirim ke member
#### Jenis OTP 2,3, 4 & 5 : URL untuk email ganti data  : https://moringaku.id/tools/profile?code={hash}
#
- Sender : **PHP**
- Target : **Engine**

#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| MemberId | INT | Y | member id = id di table members |
| JenisOTP | INT | Y | 1 = not used |
|||| 2 = Change Password |
|||| 3 = Change Profile |
|||| 4 = Change Warisan |
|||| 5 = Change user id |
|||| 6 = not used |
| data | JSON | N | Data temporary |
|||| "nexturl"       : url tujuan untuk dikirim ke email |
|||| ----- Jenis OTP = 3 ----- |
|||| "nomornpwp"     : no npwp |
|||| "namawpajak"    : nama npwp |
|||| "alamatwpajak"  : alamat npwp|
|||| "nomorac"       : AC nomor |
|||| "namaac"        : AC Nama |
|||| "namabank"      : Nama Bank |
|||| "cabangBank"    : Cabang bank |
|||| "email"         : email |
|||| "hideemail"     : hide email 0 = No, 1 = Yes |
|||| "telepon"       : Telepon |
|||| "hidephone"     : hide phone 0 = No, 1 = Yes |
|||| "whatsapp"      : Whatsapp No |
|||| "hidewa"        : hide Whatsapp 0 = No, 1 = Yes|
|||| ----- Jenis OTP 4 ----- |
|||| "benname"       : nama ahli waris |
|||| "benktp"        : ktp ahli wris |
|||| "bendob"        : tgl lahir ahli waris yyyy-mm-dd |
|||| "bengender"     : gender 0 = Pria , 1 = wanita |
|||| "benemail"      : email ahli waris |
|||| "benphone"      : telp ahli waris |
|||| "benrelation"   : hubungan 0 = suami, 1 = istri, 2 = anak, 3 = kakak, 4 = adik |
|||| ----- Jenis OTP 5 ----- |
|||| "newuserid"     : user id baru (field database : userid2) |

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
        "jenisotp":2,
        "data":
        {
            "nexturl" : "https://moringaku.id/tools/profile?code="
            
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
        "jenisotp":3,
        "data":
        {
            "nexturl"       : "https://moringaku.id/tools/profile?code=",
            "nomornpwp"     : "711501718439000",
            "namawpajak"    : "pian", 
            "alamatwpajak"  : "Jl. cagak",
            "nomorac"       : "8330059568",
            "namaac"        : "Rini Purnamasari",
            "namabank"      : "BCA2",
            "cabangBank"    : "Jakarta",
            "email"         : "storialika@gmail.com",
            "hideemail"     : 1,
            "telepon"       : "083804649937",
            "hidephone"     : 1,
            "whatsapp"      : "083804649937",
            "hidewa"        : 1            
        }
    }
    
```
#
##### - Sample call:
###### Change warisan 
```sh
    data: 
    {
        "memberid": 12.
        "jenisotp":4,
        "data":
        {
            "nexturl"   : "https://moringaku.id/tools/profile?code=",
            "benname"   : "Surya atmadja",
            "benktp"    : "3891000001212",
            "bendob"    : "1988-03-20",
            "bengender" : 0,
            "benemail"  : "surya@email.com",
            "benphone"  : "0819910000",
            "benrelation": 3
        }
    }
    
```
#
##### - Sample call:
###### Change user id
```sh
    data: 
    {
        "memberid": 12.
        "jenisotp":5,
        "data":
        {
            "nexturl"   : "https://moringaku.id/tools/profile?code=",
            "newuserid" : "Surya001"
            
        }
    }
    
```
##### Sample response:
###### Success Response
```sh
{
    "result": 0,
    "message": "ok"
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
| Result | INT | Y | 0 = OK; 1 = Not OK |
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

    data: 
    {
        "hashcode":"5D89006A21776A45E050A8C04E0A33D8"
    }
    
```

##### Sample response:
###### Success Response aktivasi akun JenisOTP 1 s/d 5
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
    "message" : "ok"
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
|||| 1=Not OK |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh

    data: 
    {
        "memberid": 15,
        "hashcode":"ABCDEWFGH1234567890"
    }
    
```

##### Sample response:
###### Success Response
```sh
{
    "result": 0,
    "message": "ok",
}
```
#



### 4. /ChangeIdPwd
#### - Change ID & Pwd Member saat aktivasi / saat member meminta dari member area dan melalui email link OTP
- Sender : **PHP**
- Target : **Engine**


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| MemberId | INT | Y | MemberId |
| UserId | STRING | N | New User ID , tidak diisi jika ganti password saja/reset pwd|
| Pwd | STRING | Y | New Password |
| hashcode | STRING | N | kode OTP |
| otpvalue | INT | N | nilai untuk update OTP |

#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = OK; engine update database |
|||| 1 = NOT OK |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh

    data: 
    {
        "memberid" : 15,
        "userid" :  "iksan0201"
        "pwd" : "3220102910",
        "hashcode" : "ajkshash8as87d8as7d8asd8a7aduudf",
        "otpvalue" : 1
        
    }
    
```

##### Sample response:
###### Success Response
```sh
{
    "result": 0,
    "message": "ok",
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
| Result | INT| Y | 0 = OK, tidak terpakai |
|||| 1 = sudah terpakai / error |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh

    data: 
    {
        "userid":"kodokbuduk"
    }
    
```

##### Sample response:
###### Error Response
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
| bendob | STRING | Y | DOB yyyy-mm-dd |
| bengender | INT | Y | 0 = pria; 1 = wanita | 
| benemail | STRING | Y | email |
| benphone | STRING | N | phone |
| benrelation | INT | N | 0 = Suami; 1 = Istri; 2 = Anak; 3 = kakak; 4 = adik |



#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = ok |
|||| 1 =  error |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh

    data: 
    {
        "memberid": 21,
        "benname" : "ahmad zakhri",
        "benktp" : "1234567890",
        "bendob" " "2019-02-10",
        "bengender" : 0,
        "benemail" : "ahmad@email.com",
        "benphone" : "0819929919091",
        "benrelation" : 2
        
    }
    
```

##### Sample response:
###### Error Response
```sh
{
    "result": 1,
    "message": "error",
}
```
#

