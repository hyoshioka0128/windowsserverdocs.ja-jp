---
title: manage-bde プロテクターの管理
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f9b22c5-cc93-45df-9165-bedee94998da
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/06/2018
ms.openlocfilehash: 1a2e2c851ec9bc93ec434a35f14c6f92ec831876
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839955"
---
# <a name="manage-bde-protectors"></a>manage-bde: プロテクター

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

BitLocker 暗号化キーの保護方法を管理します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。
## <a name="syntax"></a>構文
```
manage-bde -protectors [{-get|-add|-delete|-disable|-enable|-adbackup|-aadbackup}] <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]
```
#### <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                                                                                                                                           説明                                                                                                                                                                                            |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     取得      |                                                                                                                                            ドライブで有効になっているすべてのキーの保護方法を表示し、それらの型と識別子 (ID) を提供します。                                                                                                                                             |
|     追加      |                                                                                                                                   追加の[パラメーター](manage-bde-protectors.md#BKMK_addprotectors)を使用して、指定されたキー保護方法を追加します。                                                                                                                                    |
|    -delete    | BitLocker によって使用されるキーの保護方法を削除します。 ない場合は、ドライブからすべてのキー プロテクターを削除は、省略可能な [-パラメーターを削除](manage-bde-protectors.md#BKMK_deleteprotectors) を削除するどの保護装置を指定するために使用します。 ドライブ上の最後の保護機能が削除されると、あるデータへのアクセスが失われないように不注意にドライブの BitLocker による保護が無効です。 |
|   -disable    |                      暗号化キーで使用できるをドライブにセキュリティで保護されて暗号化されたデータにアクセスできるようにするには、保護を無効にします。 キーの保護機能は削除されません。 しない限り、Windows が起動されて、次回の保護を再開する、省略可能な [-パラメーターを無効にする](manage-bde-protectors.md#BKMK_disableprot) 再起動数を指定するために使用します。                       |
|    -enable    |                                                                                                                             保護を有効するには、ドライブから、保護されていない暗号化キーを削除します。 ドライブで構成されているすべてのキー プロテクターが適用されます。                                                                                                                             |
|   -adbackup   |                                                                          Active Directory ドメイン サービス (AD DS) に指定されたドライブのすべての回復情報をバックアップします。 AD DS に 1 つの回復キーのみをバックアップするには、追加、 **-id** パラメーターをバックアップする特定の回復キーの ID を指定します。                                                                           |
|  -aadbackup   |                                                                            指定されたドライブのすべての回復情報を Azure Active Directory (Azure Ad) にバックアップします。 Azure AD に1つの回復キーだけをバックアップするには、 **-id**パラメーターを追加し、バックアップする特定の回復キーの id を指定します。                                                                             |
|    <Drive>    |                                                                                                                                                                          コロンの後にドライブ文字を表します。                                                                                                                                                                          |
| -computername |                                                                                                              Manage-bde.exe を使用して、別のコンピューター上の BitLocker 保護を変更することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。                                                                                                              |
|    <Name>     |                                                                                                                 BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。                                                                                                                  |
|   -? または /?    |                                                                                                                                                                            コマンドプロンプトで簡単なヘルプを表示します。                                                                                                                                                                            |
|  -help または-h  |                                                                                                                                                                          コマンドプロンプトで完全なヘルプを表示します。                                                                                                                                                                           |

### <a name="-add-syntax-and-parameters"></a><a name=BKMK_addprotectors></a>-構文とパラメーターを追加する
```
manage-bde  -protectors  -add [<Drive>] [-forceupgrade] [-recoverypassword <NumericalPassword>] [-recoverykey <pathToExternalKeydirectory>]
[-startupkey <pathToExternalKeydirectory>] [-certificate {-cf <pathToCertificateFile>|-ct <CertificateThumbprint>}] [-tpm] [-tpmandpin] 
[-tpmandstartupkey <pathToExternalKeydirectory>] [-tpmandpinandstartupkey <pathToExternalKeydirectory>] [-password][-adaccountorgroup <securityidentifier> [-computername <Name>] 
[{-?|/?}] [{-help|-h}]
```

|          パラメーター           |                                                                                                                                                                                   説明                                                                                                                                                                                   |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           <Drive>            |                                                                                                                                                                 コロンの後にドライブ文字を表します。                                                                                                                                                                  |
|      -recoverypassword       |                                                                                                                                    数字のパスワード保護機能を追加します。 また、 **-rp**をこのコマンドの省略版として使用することもできます。                                                                                                                                     |
|     <NumericalPassword>      |                                                                                                                                                                        回復パスワードを表します。                                                                                                                                                                        |
|         -recoverykey         |                                                                                                                                回復用の外部キー保護機能を追加します。 このコマンドの省略版として **-rk**を使用することもできます。                                                                                                                                 |
| <pathToExternalKeydirectory> |                                                                                                                                                               回復キーへのディレクトリパスを表します。                                                                                                                                                                |
|         -startupkey          |                                                                                                                                 スタートアップ用の外部キー保護機能を追加します。 また、このコマンドの省略版として **-sk**を使用することもできます。                                                                                                                                 |
| <pathToExternalKeydirectory> |                                                                                                                                                                スタートアップキーへのディレクトリパスを表します。                                                                                                                                                                |
|         -証明書         |                                                                                                                               データドライブの公開キープロテクターを追加します。 使用することも **-cert** としてこのコマンドの簡易版です。                                                                                                                               |
|             -cf              |                                                                                                                                              公開キー証明書を提供する証明書ファイルが使用されることを指定します。                                                                                                                                              |
|   <pathToCertificateFile>    |                                                                                                                                                             証明書ファイルをディレクトリのパスを表します。                                                                                                                                                              |
|             -ct              |                                                                                                                                           証明書の拇印が公開キー証明書を識別するために使用されることを指定します。                                                                                                                                           |
|   <CertificateThumbprint>    |                                                       使用する証明書の拇印プロパティの値を指定します。 たとえば、証明書の拇印の値 a9 09 50 2d d8 2a e4 14 33 e6 f8 38 86 b0 0d 42 77 a3 2a a909502dd82ae41433e6f83886b00d4277a32a7b を指定する必要があります。                                                        |
|          -tpmandpin          |                                                                                           オペレーティングシステムドライブのトラステッドプラットフォームモジュール (TPM) と暗証番号 (PIN) の保護機能を追加します。 また、このコマンドの省略版として **-tp**を使用することもできます。                                                                                           |
|      -tpmandstartupkey       |                                                                                                                    オペレーティングシステムドライブの TPM とスタートアップキーの保護機能を追加します。 このコマンドの省略版として **-やれやれ**を使用することもできます。                                                                                                                    |
|   -tpmandpinandstartupkey    |                                                                                                                オペレーティングシステムドライブの TPM、PIN、スタートアップキーの保護機能を追加します。 また、このコマンドの省略版として **-tpsk**を使用することもできます。                                                                                                                 |
|          -password           |                                                                                                                              データドライブのパスワードキー保護機能を追加します。 使用することも **- pw** としてこのコマンドの簡易版です。                                                                                                                              |
|      -adaccountorgroup       | ボリュームのセキュリティ識別子 (SID) ベースの id プロテクターを追加します。  使用することも **-sid** としてこのコマンドの簡易版です。 **重要:** 既定では、WMI または manage-bde を使用して ADAccountOrGroup プロテクターをリモートで追加することはできません。  配置でこのプロテクターをリモートで追加する機能が必要な場合は、制約付き委任を有効にする必要があります。 |
|        -computername         |                                                                                                       別のコンピューター上の BitLocker 保護を変更するために管理-bde を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。                                                                                                       |
|            <Name>            |                                                                                                         BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。                                                                                                         |

### <a name="-delete-syntax-and-parameters"></a><a name=BKMK_deleteprotectors></a>-構文とパラメーターの削除
```
manage-bde  -protectors  -delete <Drive> [-type {recoverypassword|externalkey|certificate|tpm|tpmandstartupkey|tpmandpin|tpmandpinandstartupkey|Password|Identity}] 
[-id <KeyProtectorID>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

|       パラメーター        |                                                                              説明                                                                               |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        <Drive>         |                                                             コロンの後にドライブ文字を表します。                                                             |
|         型          |                               削除するキー保護機能を識別します。 使用することも **-t** としてこのコマンドの簡易版です。                               |
|    recoverypassword    |                                                 任意の回復パスワードのキー プロテクターを削除するかを指定します。                                                 |
|      externalkey       |                                        ドライブに関連付けられているすべての外部キー プロテクターを削除するかを指定します。                                         |
|      証明書       |                                       ドライブに関連付けられているすべての証明書のキー プロテクターを削除するかを指定します。                                       |
|          tpm           |                                        TPM のみキー プロテクター ドライブに関連付けられているを削除するかを指定します。                                         |
|    tpmandstartupkey    |                                このドライブに関連付けられている TPM およびスタートアップキーに基づくキープロテクターを削除することを指定します。                                |
|       tpmandpin        |                                    ドライブに関連付けられている TPM および PIN ベースのキー保護機能を削除する必要があることを指定します。                                    |
| tpmandpinandstartupkey |                             ドライブに関連付けられている TPM、PIN、およびスタートアップキーに基づくキープロテクターを削除する必要があることを指定します。                             |
|        password        |                                        ドライブに関連付けられているパスワード キーの保護を削除するかを指定します。                                         |
|        ID        |                                        ドライブに関連付けられているすべての id キー プロテクターを削除するかを指定します。                                         |
|          -id           |                キー識別子を使用して削除するキー保護機能を識別します。 このパラメーターは、代わりのオプションを **-型** パラメーター。                 |
|    <KeyProtectorID>    |        個々 のキー保護機能、ドライブを削除するを識別します。 使用して、キー保護機能の Id を表示できる、 **から manage-bde-プロテクター-取得** コマンドです。         |
|     -computername      | Manage-bde.exe を使用して、別のコンピューター上の BitLocker 保護を変更することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
|         <Name>         |    BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。     |
|        -? または /?        |                                                               コマンドプロンプトで簡単なヘルプを表示します。                                                               |
|      -help または-h       |                                                             コマンドプロンプトで完全なヘルプを表示します。                                                              |

### <a name="-disable-syntax-and-parameters"></a><a name=BKMK_disableprot></a>-構文とパラメーターを無効にする
```
manage-bde  -protectors  -disable <Drive> [-RebootCount <integer 0 - 15>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

|   パラメーター   |                                                                                                                                                                                                                   説明                                                                                                                                                                                                                    |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <Drive>    |                                                                                                                                                                                                  コロンの後にドライブ文字を表します。                                                                                                                                                                                                  |
|  RebootCount  | Windows 8 以降では、オペレーティングシステムボリュームの保護が中断され、Windows が再起動された後に、RebootCount パラメーターで指定した回数だけ再開されることを指定します。 保護が無期限に停止する場合は 0 を指定します。 このパラメーターが BitLocker 保護が自動的に指定されていない場合は、Windows が再起動されたときを再開します。 使用することも **-rc** としてこのコマンドの簡易版です。 |
| -computername |                                                                                                                                      Manage-bde.exe を使用して、別のコンピューター上の BitLocker 保護を変更することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。                                                                                                                                      |
|    <Name>     |                                                                                                                                         BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。                                                                                                                                          |
|   -? または /?    |                                                                                                                                                                                                    コマンドプロンプトで簡単なヘルプを表示します。                                                                                                                                                                                                    |
|  -help または-h  |                                                                                                                                                                                                  コマンドプロンプトで完全なヘルプを表示します。                                                                                                                                                                                                   |

## <a name="examples"></a><a name=BKMK_Examples></a>例
次の例を使用して、 **-プロテクター** ドライブ E に証明書ファイルで確認された証明書キー保護機能を追加するコマンド
```
manage-bde  -protectors  -add E: -certificate  -cf c:\File Folder\Filename.cer
```
次の例を使用して、 **-プロテクター** を追加するコマンド、 **adaccountorgroup** ドライブ E にドメインとユーザー名で識別されるキーの保護機能
```
manage-bde  -protectors  -add E: -sid DOMAIN\user
```
次の例では、**プロテクター**コマンドを使用して、コンピューターが3回再起動されるまで保護を無効にしています。
```
manage-bde  -protectors  -disable C: -rc 3
```
次の例では、 **-プロテクター**コマンドを使用して、C ドライブのすべての TPM とスタートアップキーに基づくキープロテクターを削除しています。
```
manage-bde  -protectors -delete C: -type tpmandstartupkey
```
次の例を使用して、 **-プロテクター** ドライブ C のすべての回復情報を AD DS にバックアップするコマンドです。
```
manage-bde  -protectors  -adbackup C:
```
## <a name="additional-references"></a>その他の参照情報
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [manage-bde](manage-bde.md)
