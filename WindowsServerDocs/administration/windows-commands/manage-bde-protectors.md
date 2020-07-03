---
title: manage-bde プロテクターの管理
description: BitLocker 暗号化キーに使用される保護方法を管理する manage-bde プロテクターコマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f9b22c5-cc93-45df-9165-bedee94998da
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/06/2018
ms.openlocfilehash: d277c070ff0cdee0d93d7a8be11dc13bea5adb95
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922303"
---
# <a name="manage-bde-protectors"></a>manage-bde プロテクターの管理

> 適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

BitLocker 暗号化キーの保護方法を管理します。

## <a name="syntax"></a>構文

```
manage-bde -protectors [{-get|-add|-delete|-disable|-enable|-adbackup|-aadbackup}] <drive> [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ----------- | ----------- |
| 取得 | ドライブで有効になっているすべてのキーの保護方法を表示し、それらの型と識別子 (ID) を提供します。 |
| 追加 | 追加**の追加**パラメーターを使用して、指定されたキー保護メソッドを追加します。 |
| -削除 | BitLocker で使用されるキーの保護方法を削除します。 削除するプロテクターを指定するためにオプションの **-delete**パラメーターを使用しない限り、すべてのキープロテクターがドライブから削除されます。 ドライブ上の最後の保護機能が削除されると、あるデータへのアクセスが失われないように不注意にドライブの BitLocker による保護が無効です。 |
| -を無効にします。 | 暗号化キーで使用できるをドライブにセキュリティで保護されて暗号化されたデータにアクセスできるようにするには、保護を無効にします。 キーの保護機能は削除されません。 次に Windows を起動したときに保護が再開されます。ただし、省略可能**な-disable**パラメーターを使用して再起動回数を指定する場合は除きます。 |
| -を有効にします。 | 保護を有効するには、ドライブから、保護されていない暗号化キーを削除します。 ドライブで構成されているすべてのキー プロテクターが適用されます。 |
| -adbackup | Active Directory ドメイン サービス (AD DS) に指定されたドライブのすべての回復情報をバックアップします。 AD DS に 1 つの回復キーのみをバックアップするには、追加、 **-id** パラメーターをバックアップする特定の回復キーの ID を指定します。 |
| -aadbackup | 指定されたドライブのすべての回復情報を Azure Active Directory (Azure AD) にバックアップします。 Azure AD に1つの回復キーだけをバックアップするには、 **-id**パラメーターを追加し、バックアップする特定の回復キーの id を指定します。 |
| `<drive>` | コロンの後にドライブ文字を表します。 |
| -computername | manage-bde.exe が別のコンピューターの BitLocker 保護を変更するために使用されることを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
| `<name>` | BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。 |
| -? または /? | コマンドプロンプトで簡単なヘルプを表示します。 |
| -help または-h | コマンドプロンプトで完全なヘルプを表示します。 |

#### <a name="additional--add-parameters"></a>追加-パラメーターの追加

-Add パラメーターでは、これらの有効な追加パラメーターを使用することもできます。

```
manage-bde -protectors -add [<drive>] [-forceupgrade] [-recoverypassword <numericalpassword>] [-recoverykey <pathtoexternalkeydirectory>]
[-startupkey <pathtoexternalkeydirectory>] [-certificate {-cf <pathtocertificatefile>|-ct <certificatethumbprint>}] [-tpm] [-tpmandpin]
[-tpmandstartupkey <pathtoexternalkeydirectory>] [-tpmandpinandstartupkey <pathtoexternalkeydirectory>] [-password][-adaccountorgroup <securityidentifier> [-computername <name>]
[{-?|/?}] [{-help|-h}]
```

| パラメーター | 説明 |
| --------- | ----------- |
| `<drive>` | コロンの後にドライブ文字を表します。 |
| -recoverypassword | 数字のパスワード保護機能を追加します。 また、 **-rp**をこのコマンドの省略版として使用することもできます。 |
| `<numericalpassword>` | 回復パスワードを表します。 |
| -recoverykey | 回復用の外部キー保護機能を追加します。 このコマンドの省略版として **-rk**を使用することもできます。 |
| `<pathtoexternalkeydirectory>` | 回復キーへのディレクトリパスを表します。 |
| -startupkey | スタートアップ用の外部キー保護機能を追加します。 また、このコマンドの省略版として **-sk**を使用することもできます。 |
| `<pathtoexternalkeydirectory>` | スタートアップキーへのディレクトリパスを表します。 |
| -証明書 | データドライブの公開キープロテクターを追加します。 使用することも **-cert** としてこのコマンドの簡易版です。 |
| cf | 公開キー証明書を提供する証明書ファイルが使用されることを指定します。 |
| <pathtocertificatefile> | 証明書ファイルをディレクトリのパスを表します。 |
| -ct | 証明書の拇印が公開キー証明書を識別するために使用されることを指定します。 |
| `<certificatethumbprint>` | 使用する証明書の拇印プロパティの値を指定します。 たとえば、証明書の拇印の値 a9 09 50 2d d8 2a e4 14 33 e6 f8 38 86 b0 0d 42 77 a3 2a a909502dd82ae41433e6f83886b00d4277a32a7b を指定する必要があります。 |
| -tpmandpin | オペレーティングシステムドライブのトラステッドプラットフォームモジュール (TPM) と暗証番号 (PIN) の保護機能を追加します。 また、このコマンドの省略版として **-tp**を使用することもできます。 |
| -tpmandstartupkey | オペレーティングシステムドライブの TPM とスタートアップキーの保護機能を追加します。 このコマンドの省略版として **-やれやれ**を使用することもできます。 |
| -tpmandpinandstartupkey | オペレーティングシステムドライブの TPM、PIN、スタートアップキーの保護機能を追加します。 また、このコマンドの省略版として **-tpsk**を使用することもできます。 |
| -パスワード | データドライブのパスワードキー保護機能を追加します。 使用することも **- pw** としてこのコマンドの簡易版です。 |
| -adaccountorgroup | セキュリティ識別子 (SID) を追加-ベースのボリュームの保護機能を識別します。 使用することも **-sid** としてこのコマンドの簡易版です。 **重要:** 既定では、WMI または manage-bde を使用して ADaccountorgroup プロテクターをリモートで追加することはできません。 配置でこのプロテクターをリモートで追加する機能が必要な場合は、制約付き委任を有効にする必要があります。 |
| -computername | 別のコンピューター上の BitLocker 保護を変更するために管理-bde を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
| `<name>` | BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。 |
| -? または /? | コマンドプロンプトで簡単なヘルプを表示します。 |
| -help または-h | コマンドプロンプトで完全なヘルプを表示します。 |

#### <a name="additional--delete-parameters"></a>追加-削除パラメーター

```
manage-bde -protectors -delete <drive> [-type {recoverypassword|externalkey|certificate|tpm|tpmandstartupkey|tpmandpin|tpmandpinandstartupkey|Password|Identity}]
[-id <keyprotectorID>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

| パラメーター | 説明 |
| --------- | ----------- |
| `<drive>` | コロンの後にドライブ文字を表します。 |
| 型 | 削除するキー保護機能を識別します。 使用することも **-t** としてこのコマンドの簡易版です。 |
| recoverypassword | 任意の回復パスワードのキー プロテクターを削除するかを指定します。 |
| externalkey | ドライブに関連付けられているすべての外部キー プロテクターを削除するかを指定します。 |
| 証明書 (certificate) | ドライブに関連付けられているすべての証明書のキー プロテクターを削除するかを指定します。 |
| tpm | TPM のみキー プロテクター ドライブに関連付けられているを削除するかを指定します。 |
| tpmandstartupkey | このドライブに関連付けられている TPM およびスタートアップキーに基づくキープロテクターを削除することを指定します。 |
| tpmandpin | ドライブに関連付けられている TPM および PIN ベースのキー保護機能を削除する必要があることを指定します。 |
| tpmandpinandstartupkey | ドライブに関連付けられている TPM、PIN、およびスタートアップキーに基づくキープロテクターを削除する必要があることを指定します。 |
| password | ドライブに関連付けられているパスワード キーの保護を削除するかを指定します。 |
| identity | ドライブに関連付けられているすべての id キー プロテクターを削除するかを指定します。 |
| -ID | キー識別子を使用して削除するキー保護機能を識別します。 このパラメーターは、代わりのオプションを **-型** パラメーター。 |
| `<keyprotectorID>` | 個々 のキー保護機能、ドライブを削除するを識別します。 使用して、キー保護機能の Id を表示できる、 **から manage-bde-プロテクター-取得** コマンドです。 |
| -computername | manage-bde.exe が別のコンピューターの BitLocker 保護を変更するために使用されることを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
| `<name>` | BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。 |
| -? または /? | コマンドプロンプトで簡単なヘルプを表示します。 |
| -help または-h | コマンドプロンプトで完全なヘルプを表示します。 |

#### <a name="additional--disable-parameters"></a>追加-disable パラメーター

```
manage-bde -protectors -disable <drive> [-rebootcount <integer 0 - 15>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

| パラメーター | 説明 |
| --------- | ----------- |
| `<drive>` | コロンの後にドライブ文字を表します。 |
| rebootcount | オペレーティングシステムボリュームの保護が中断され、Windows が再起動された後に、 **rebootcount**パラメーターで指定した回数だけ再開されることを指定します。 保護を無期限に中断する場合は**0**を指定します。 このパラメーターを指定しないと、Windows の再起動後に BitLocker 保護が自動的に再開されます。 使用することも **-rc** としてこのコマンドの簡易版です。 |
| -computername | manage-bde.exe が別のコンピューターの BitLocker 保護を変更するために使用されることを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
| `<name>` | BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。 |
| -? または /? | コマンドプロンプトで簡単なヘルプを表示します。 |
| -help または-h | コマンドプロンプトで完全なヘルプを表示します。 |

### <a name="examples"></a>例

証明書ファイルによって識別される証明書キープロテクターをドライブ E に追加するには、次のように入力します。

```
manage-bde -protectors -add E: -certificate -cf c:\File Folder\Filename.cer
```

ドメインとユーザー名で識別される**adaccountorgroup**キープロテクターをドライブ E に追加するには、次のように入力します。

```
manage-bde -protectors -add E: -sid DOMAIN\user
```

コンピューターが3回再起動されるまで保護を無効にするには、次のように入力します。

```
manage-bde -protectors -disable C: -rc 3
```

ドライブ C の TPM およびスタートアップキーベースのキー保護機能をすべて削除するには、次のように入力します。

```
manage-bde -protectors -delete C: -type tpmandstartupkey
```

ドライブ C のすべての回復情報を AD DS にバックアップするには、次のように入力します。

```
manage-bde -protectors -adbackup C:
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [manage-bde コマンド](manage-bde.md)
