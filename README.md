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
| UserId | STRING | Y | member id |
| UserName | STRING | Y | nama member |
| JenisOTP | INT | Y | 1 = Aktivasi Akun |
|||| 2 = Change Password |
|||| 3 = Change Profile |
|||| 4 = Change Warisan |
|||| 5 = Change user id |
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




