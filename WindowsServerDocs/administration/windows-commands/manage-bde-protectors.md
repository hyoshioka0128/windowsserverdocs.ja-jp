---
title: manage-bde プロテクター
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f9b22c5-cc93-45df-9165-bedee94998da
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/06/2018
ms.openlocfilehash: c804fe6fa4aca8c55bd6a312536cc453962b3c1c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852843"
---
# <a name="manage-bde-protectors"></a>manage-bde: 保護機能

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

BitLocker 暗号化キーの保護方法を管理します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。
## <a name="syntax"></a>構文
```
manage-bde -protectors [{-get|-add|-delete|-disable|-enable|-adbackup|-aadbackup}] <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|取得|ドライブで有効になっているすべてのキーの保護方法を表示し、それらの型と識別子 (ID) を提供します。|
|追加|追加のキーの保護方法を使用して指定された追加[パラメーターを追加](manage-bde-protectors.md#BKMK_addprotectors)します。|
|-削除|BitLocker で使用されるキーの保護方法を削除します。 ない場合は、ドライブからすべてのキー プロテクターを削除は、省略可能な [-パラメーターを削除](manage-bde-protectors.md#BKMK_deleteprotectors) を削除するどの保護装置を指定するために使用します。 ドライブ上の最後の保護機能が削除されると、あるデータへのアクセスが失われないように不注意にドライブの BitLocker による保護が無効です。|
|-を無効にします。|暗号化キーで使用できるをドライブにセキュリティで保護されて暗号化されたデータにアクセスできるようにするには、保護を無効にします。 キーの保護機能は削除されません。 しない限り、Windows が起動されて、次回の保護を再開する、省略可能な [-パラメーターを無効にする](manage-bde-protectors.md#BKMK_disableprot) 再起動数を指定するために使用します。|
|-を有効にします。|保護を有効するには、ドライブから、保護されていない暗号化キーを削除します。 ドライブで構成されているすべてのキー プロテクターが適用されます。|
|-adbackup|Active Directory ドメイン サービス (AD DS) に指定されたドライブのすべての回復情報をバックアップします。 AD DS に 1 つの回復キーのみをバックアップするには、追加、 **-id** パラメーターをバックアップする特定の回復キーの ID を指定します。|
|-aadbackup|Azure Active Directory (Azure Ad) に指定されたドライブのすべての回復情報をバックアップします。 Azure AD に 1 つの回復キーのみをバックアップするには追加、 **-id**パラメーターをバックアップする特定の回復キーの ID を指定します。|
|<Drive>|コロンの後にドライブ文字を表します。|
|-computername|別のコンピューターに bitlocker による保護の変更に使用する、bde.exe を指定します。 使用することも **- cn**としてこのコマンドの簡易版です。|
|<Name>|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンド プロンプトでヘルプの簡単なが表示されます。|
|--help または-h|コマンド プロンプトでヘルプを完了しますが表示されます。|
### <a name="BKMK_addprotectors"></a>構文およびパラメーターの追加
```
manage-bde  protectors  add [<Drive>] [-forceupgrade] [-recoverypassword <NumericalPassword>] [-recoverykey <pathToExternalKeydirectory>]
[-startupkey <pathToExternalKeydirectory>] [-certificate {-cf <pathToCertificateFile>|-ct <CertificateThumbprint>}] [-tpm] [-tpmandpin] 
[-tpmandstartupkey <pathToExternalKeydirectory>] [-tpmandpinandstartupkey <pathToExternalKeydirectory>] [-password][-adaccountorgroup <securityidentifier> [-computername <Name>] 
[{-?|/?}] [{-help|-h}]
```
|パラメーター|説明|
|-------|--------|
|<Drive>|コロンの後にドライブ文字を表します。|
|-recoverypassword|数字のパスワード保護機能を追加します。 使用することも **- rp**としてこのコマンドの簡易版です。|
|<NumericalPassword>|回復パスワードを表します。|
|-recoverykey|回復用の外部キー プロテクターを追加します。 使用することも**rk**としてこのコマンドの簡易版です。|
|<pathToExternalKeydirectory>|回復キーをディレクトリのパスを表します。|
|-startupkey|スタートアップの外部キー保護機能を追加します。 使用することも **-sk**としてこのコマンドの簡易版です。|
|<pathToExternalKeydirectory>|スタートアップ キーには、ディレクトリ パスを表します。|
|-証明書|データ ドライブのパブリック キー保護機能を追加します。 使用することも **-cert** としてこのコマンドの簡易版です。|
|cf|公開キー証明書を提供する証明書ファイルが使用されることを指定します。|
|<pathToCertificateFile>|証明書ファイルをディレクトリのパスを表します。|
|-ct|証明書の拇印が公開キー証明書を識別するために使用されることを指定します。|
|<CertificateThumbprint>|使用する証明書の拇印プロパティの値を指定します。 たとえば、証明書のサムプリント値"a9 09 50 2d d8 2a e4 14 33 e6 f8 38 86 b0 0 d 42 77 a3 2a 7b"内"a909502dd82ae41433e6f83886b00d4277a32a7b"として指定する必要があります。|
|-tpmandpin|トラステッド プラットフォーム モジュール (TPM) と、オペレーティング システム ドライブの個人識別番号 (PIN) 保護が機能を追加します。 使用することも **-tp**としてこのコマンドの簡易版です。|
|-tpmandstartupkey|オペレーティング システム ドライブの TPM とスタートアップ キー プロテクターを追加します。 使用することも **-やれ**としてこのコマンドの簡易版です。|
|-tpmandpinandstartupkey|TPM、PIN、およびオペレーティング システム ドライブのスタートアップ キーの保護機能を追加します。 使用することも **- tpsk**としてこのコマンドの簡易版です。|
|-パスワード|データ ドライブのパスワードのキー保護機能を追加します。 使用することも **- pw** としてこのコマンドの簡易版です。|
|-adaccountorgroup|セキュリティ識別子 (SID) を追加-ベースのボリュームの保護機能を識別します。  使用することも **-sid** としてこのコマンドの簡易版です。 **大事な：** 既定では、WMI または、manage-bde を使用してリモートで ADAccountOrGroup プロテクターを追加することはできません。  デプロイには、リモートでこの保護機能を追加する機能が必要な場合は、制約付き委任を有効にする必要があります。|
|-computername|別のコンピューターに bitlocker による保護の変更に使用されるその、manage-bde を指定します。 使用することも **- cn**としてこのコマンドの簡易版です。|
|<Name>|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
### <a name="BKMK_deleteprotectors"></a>構文とパラメーターの削除
```
manage-bde  protectors  delete <Drive> [-type {recoverypassword|externalkey|certificate|tpm|tpmandstartupkey|tpmandpin|tpmandpinandstartupkey|Password|Identity}] 
[-id <KeyProtectorID>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```
|パラメーター|説明|
|-------|--------|
|<Drive>|コロンの後にドライブ文字を表します。|
|型|削除するキー保護機能を識別します。 使用することも **-t** としてこのコマンドの簡易版です。|
|recoverypassword|任意の回復パスワードのキー プロテクターを削除するかを指定します。|
|externalkey|ドライブに関連付けられているすべての外部キー プロテクターを削除するかを指定します。|
|証明書 (certificate)|ドライブに関連付けられているすべての証明書のキー プロテクターを削除するかを指定します。|
|tpm|TPM のみキー プロテクター ドライブに関連付けられているを削除するかを指定します。|
|tpmandstartupkey|TPM とスタートアップ キーに基づいてキー プロテクター ドライブに関連付けられているを削除する必要がありますを指定します。|
|tpmandpin|指定します、TPM および PIN ベースのキー プロテクター ドライブに関連付けを削除する必要があります。|
|tpmandpinandstartupkey|TPM、PIN、およびスタートアップ キーに基づいてキー プロテクター ドライブに関連付けられているを削除することを指定します。|
|password|ドライブに関連付けられているパスワード キーの保護を削除するかを指定します。|
|ID|ドライブに関連付けられているすべての id キー プロテクターを削除するかを指定します。|
|-id|キー識別子を使用して削除するキー保護機能を識別します。 このパラメーターは、代わりのオプションを **-型** パラメーター。|
|<KeyProtectorID>|個々 のキー保護機能、ドライブを削除するを識別します。 使用して、キー保護機能の Id を表示できる、 **から manage-bde-プロテクター-取得** コマンドです。|
|-computername|別のコンピューターに bitlocker による保護の変更に使用する、bde.exe を指定します。 使用することも **- cn**としてこのコマンドの簡易版です。|
|<Name>|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンド プロンプトでヘルプの簡単なが表示されます。|
|--help または-h|コマンド プロンプトでヘルプを完了しますが表示されます。|
### <a name="BKMK_disableprot"></a>構文とパラメーターを無効にします。
```
manage-bde  protectors  disable <Drive> [-RebootCount <integer 0 - 15>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```
|パラメーター|説明|
|-------|--------|
|<Drive>|コロンの後にドライブ文字を表します。|
|RebootCount|Windows 8 以降を指定再起動 RebootCount パラメーターで指定された回数の合計のオペレーティング システムのボリュームの保護が中断されているし、Windows がされた後に再開されます。 保護が無期限に停止する場合は 0 を指定します。 このパラメーターが BitLocker 保護が自動的に指定されていない場合は、Windows が再起動されたときを再開します。 使用することも **-rc** としてこのコマンドの簡易版です。|
|-computername|別のコンピューターに bitlocker による保護の変更に使用する、bde.exe を指定します。 使用することも **- cn**としてこのコマンドの簡易版です。|
|<Name>|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンド プロンプトでヘルプの簡単なが表示されます。|
|--help または-h|コマンド プロンプトでヘルプを完了しますが表示されます。|
## <a name="BKMK_Examples"></a>例
次の例を使用して、 **-プロテクター** ドライブ E に証明書ファイルで確認された証明書キー保護機能を追加するコマンド
```
manage-bde  protectors  add E: -certificate  cf "c:\File Folder\Filename.cer"
```
次の例を使用して、 **-プロテクター** を追加するコマンド、 **adaccountorgroup** ドライブ E にドメインとユーザー名で識別されるキーの保護機能
```
manage-bde  protectors  add E: -sid DOMAIN\user
```
次の例を使用して、* * * * 保護機能をコンピューターが 3 回を再起動するまで、保護を無効にするコマンドします。
```
manage-bde  protectors  disable C: -rc 3
```
次の例を使用して、 **-プロテクター**すべて TPM とスタートアップ キーを削除するコマンドがに基づいて C ドライブのキー プロテクター
```
manage-bde  protectors  delete C: -type tpmandstartupkey
```
次の例を使用して、 **-プロテクター** ドライブ C のすべての回復情報を AD DS にバックアップするコマンドです。
```
manage-bde  protectors  adbackup C:
```
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [manage-bde](manage-bde.md)
