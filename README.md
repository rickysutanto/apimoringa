# API Moringa - Front End Functions

![](https://img.shields.io/github/release/pandao/editor.md.svg)

## URL-URL untuk email OTP
### URL Aktivasi akun : https://moringaku.id/tools/aktivasi?code={hash}
### URL Update Warisan : https://moringaku.id/tools/warisan?code={hash}
### URL Ganti password : https://moringaku.id/tools/password?code={hash}
### URL untuk OTP yang di konfirmasi member : https://moringaku.id/tools/otp?code={hash}
#

### 1. /CheckOTP 
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
| Expired | INT| Y | 0 = Active; 1 = Expired |
| MemberId | STRING | Y | member id (trxid) |
| UserName | STRING | Y | nama member |
| JenisOTP | INT | Y | 1 = Aktivasi Akun |
|||| 2 = Change Password |
|||| 3 = Change Profile |
|||| 4 = Change Warisan |
|||| 5 = Change user id |
#

##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/CheckOTP",
    dataType: "json",
    type : "GET",
    data: "hashdata=5D89006A21776A45E050A8C04E0A33D8",
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
    "expired": 0,
    "memberid": "15012001012",
    "username": "Ahmad fikri",
    "jenisotp": 1,
}
```
#

### 2. /ChangePwd 
#### - Permintaan ganti Password oleh Member
- Sender : **PHP**
- Target : **Engine**


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| MemberId | STRING | Y | MemberId = TrxId |
| OldPassword | STRING | Y | Password lama |
| NewPassword | STRING | Y | Password Baru |


#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = OK ;Engine kirim email OTP |
|||| -2=Old Password Salah | 
|||| -1=Not-OK |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/ChangePwd",
    dataType: "json",
    type : "GET",
    data: "memberid=15012001012&oldpassword=paswordlamaku&newpassword=passwordbaruku",
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
    "result": -2,
    "message": "wrong old password",
}
```
#

### 3. /ChangeID 
#### - Permintaan ganti userid oleh Member (hanya berlaku jika field userid2 = null)
- Sender : **PHP**
- Target : **Engine**


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| MemberId | STRING | Y | MemberId = TrxId |
| UserId | STRING | Y | user id baru |



#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = OK; Engine kirim email OTP |
|||| -2=field userid2 not null |
|||| -1=Not-OK |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/ChangeID",
    dataType: "json",
    type : "GET",
    data: "memberid=15012001012&userid=moringaku1",
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
    "result": -2,
    "message": "already changed before",
}
```
#

### 4. /ChangeProfile
#### - Permintaan ganti Profile oleh Member
- Sender : **PHP**
- Target : **Engine**


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| MemberId | STRING | Y | MemberId = TrxId |
| NoNPWP| STRING | N | Nomor NPWP |
| NamaNPWP | STRING | N | Nama Wajib Pajak |
| AddNPWP | STRING | N | Alamat Wajib Pajak |
| AcctNo | STRING | N | Nomor Rekening |
| AcctName | STRING | N | Nama Pemilik Rekening |
| BankName | STRING | N | Nama Bank |
| BankBranch | STRING | N | Cabang Bank |
| Email | STRING | Y | Email nasabah |
| Phone | STRING | N | Telepon nasabah |
| whatsapp | STRING | N | Whatsapp nasabah |
| HideEmail | INT | N| 0 = no; 1 = yes |
| HidePhone | INT | N| 0 = no; 1 = yes |
| HideWa | INT | N| 0 = no; 1 = yes |



#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = OK; engine akan kirim email OTP|
|||| -1 = NOT-OK |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/ChangeProfile",
    dataType: "json",
    type : "GET",
    data: "memberid=15012001012&nonpwp=8100020102910&namapwp=iksan&addnpwp=alam sutera&acctno=3220102910&acctname=iksan harianto&bankname=bca&bankbranch=tebet&emai=iksan@email.com&phone=081299912&whatsapp=0812999912&hideemail=1&hidephone=1&hidewa=1",
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

### 5. /ChangeWarisan
#### - Permintaan ganti Data Warisan oleh Member
- Sender : **PHP**
- Target : **Engine**


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| MemberId | STRING | Y | MemberId = TrxId |
| BeneficiaryName| STRING | N | Nama Ahli Waris |
| BeneficiaryKtp | STRING | N | Ktp Ahli Waris|
| BeneficiaryDOB | DATE | N | Tgl lahir ahli waris |
| BeneficiaryEmail | STRING | N | Emai hli Waris |
| BeneficiaryGender | INT | N | Gender ahli waris |
| BeneficiaryPhone | STRING | N | Phone ahli waris |
| BeneficiaryRelation | STRING | N | Hubungan Ahli waris|



#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = OK ; engine akan kirim email OTP|
|||| -1 = NOT-OK |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/ChangeWarisan",
    dataType: "json",
    type : "GET",
    data: "memberid=15012001012&beneficiaryname=iksan&beneficiaryktp=3220102910&beneficiarydob=12031971&beneficiaryemail=iksan@email.com&beneficiarygender=0&beneficiaryphone=0812999912&beneficiaryrelation=istri",
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


### 6. /ChangeIdPwd
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
    type : "GET",
    data: "memberid=15012001012&userid=iksan0201&pwd=3220102910",
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

### 7. /ChangedConfirm 
#### - Konfirmasi perubahan setelah menerima OTP. 
#### Untuk ganti password, ganti profile, & ganti warisan
- Sender : **PHP**
- Target : **Engine**


#### - Parameter:
| Params | Data Type | Mandatory | Description |
|--|--|--|--|
| HashData | STRING | Y | data hash yg dikirim ke email nasabah |


#### - Output:
| Param | Data Type | Mandatory | Description |
|--|--|--|--|
| Result | INT| Y | 0 = Sukses; engine confirm perubahan |
|||| -1 = Gagal |
| Message | STRING | Y | Jika ada pesan error |

#

##### - Sample call:
###### JQuery Ajax Call 
```sh
$.ajax({
    url: "http://api.moringaku.com/internal/ChangedConfirm",
    dataType: "json",
    type : "GET",
    data: "hashdata=5D89006A21776A45E050A8C04E0A33D8",
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

### 8. /CheckID 
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
    type : "GET",
    data: "userid=kodokbuduk",
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



