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
| Result | INT| Y | 0 = OK; -2=Old Password Salah; -1=Not-OK; jika OK Engine kirim email OTP |

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
| Result | INT| Y | 0 = OK; -2=field userid2 not null ; -1=Not-OK; jika OK Engine kirim email OTP |

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
| Result | INT| Y | 0 = OK; -1 = NOT-OK , jika ok engine akan kirim email OTP|

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
| result | INT| Y | 0 = OK; -1 = NOT-OK , jika ok engine akan kirim email OTP|

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
| Result | INT| Y | 0 = OK; -1 = NOT-OK , jika ok engine update database |

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
| Result | INT| Y | 0 = Sukses; -1 = Gagal, jika OK engine confirm perubahan |

#




