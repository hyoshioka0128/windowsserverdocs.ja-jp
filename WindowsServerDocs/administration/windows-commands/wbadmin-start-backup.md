---
title: wbadmin のバックアップの開始
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 56f3e752-d99a-4c3d-8e97-10303c37dd78
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8eb017e8bf49191c33cd2d9f0cf4a62b08ebb07
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362345"
---
# <a name="wbadmin-start-backup"></a>wbadmin のバックアップの開始



指定されたパラメーターを使用してバックアップを作成します。 パラメーターを指定せず、スケジュールされた毎日のバックアップを作成した場合、このサブコマンドはスケジュールされたバックアップの設定を使用してバックアップを作成します。 パラメーターを指定した場合は、ボリュームシャドウコピーサービス (VSS) のコピーバックアップが作成され、バックアップされているファイルの履歴は更新されません。

このサブコマンドを使用して1回限りのバックアップを作成するには、 **Backup Operators**グループまたは**Administrators**グループのメンバーであるか、適切な権限が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、 **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします)。

このサブコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。

## <a name="syntax"></a>構文

Windows Vista および Windows Server 2008 の構文:
```
wbadmin start backup
[-backupTarget:{<BackupTargetLocation> | <TargetNetworkShare>}]
[-include:<VolumesToInclude>]
[-allCritical]
[-noVerify]
[-user:<UserName>]
[-password:<Password>]
[-noinheritAcl]
[-vssFull]
[-quiet]
```
Windows °7および Windows Server 2008 R2 以降の構文:
```
Wbadmin start backup
[-backupTarget:{<BackupTargetLocation> | <TargetNetworkShare>}]
[-include:<ItemsToInclude>]
[-nonRecurseInclude:<ItemsToInclude>]
[-exclude:<ItemsToExclude>]
[-nonRecurseExclude:<ItemsToExclude>]
[-allCritical]
[-systemState]
[-noVerify]
[-user:<UserName>]
[-password:<Password>]
[-noInheritAcl]
[-vssFull | -vssCopy] 
[-quiet]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-backuptarget|このバックアップのストレージの場所を指定します。 ハードディスクドライブ文字 (f:)、\\ @ no__t-1? \\Volume {GUID} の形式のボリューム GUID ベースのパス、またはリモート共有フォルダーへの汎用名前付け規則 (UNC) パスを指定する必要があります (\\ @ no__t-4 @ no__t-5servername > \\ @ no__t-7sharename > \\)。 既定では、バックアップは次の場所に保存されます: \\ @ no__t-1 @ no__t-2servername > \\ @ no__t-4sharename > \\**WindowsImageBackup**\\ @ No__t-8ComputerBackedUp > \\</br>重要:バックアップをリモート共有フォルダーに保存した場合、同じフォルダーを使用して同じコンピューターを再度バックアップすると、そのバックアップは上書きされます。 また、バックアップ操作が失敗した場合は、古いバックアップが上書きされますが、新しいバックアップは使用できないため、バックアップが存在しないことがあります。 これを回避するには、リモート共有フォルダーにサブフォルダーを作成して、バックアップを整理します。 これを行う場合は、サブフォルダーに親フォルダーとして2倍の領域が必要になります。|
|-含める|Windows Vista および Windows Server 2008 では、ボリュームドライブ文字、ボリュームマウントポイント、またはバックアップに含める GUID ベースのボリューム名のコンマ区切りのリストを指定します。 このパラメーターは、 **-backupTarget**パラメーターが使用されている場合にのみ使用してください。</br>Windows °7および Windows Server 2008 R2 以降では、バックアップに含める項目のコンマ区切りリストを指定します。 複数のファイル、フォルダー、またはボリュームを含めることができます。 ボリュームパスは、ボリュームドライブ文字、ボリュームマウントポイント、または GUID ベースのボリューム名を使用して指定できます。 GUID ベースのボリューム名を使用する場合は、円記号 (\\) で終了する必要があります。 ファイルへのパスを指定する場合は、ファイル名にワイルドカード文字 (\*) を使用できます。 **-BackupTarget**パラメーターが使用されている場合にのみ使用してください。|
|-除外|Windows °7および Windows Server 2008 R2 以降では、バックアップから除外する項目のコンマ区切りのリストを指定します。 ファイル、フォルダー、またはボリュームを除外することができます。 ボリュームパスは、ボリュームドライブ文字、ボリュームマウントポイント、または GUID ベースのボリューム名を使用して指定できます。 GUID ベースのボリューム名を使用する場合は、円記号 (\\) で終了する必要があります。 ファイルへのパスを指定する場合は、ファイル名にワイルドカード文字 (\*) を使用できます。 **-BackupTarget**パラメーターが使用されている場合にのみ使用してください。|
|-nonRecurseInclude|Windows °7および Windows Server 2008 R2 以降では、は、バックアップに含める項目の非再帰的なコンマ区切りのリストを指定します。 複数のファイル、フォルダー、またはボリュームを含めることができます。 ボリュームパスは、ボリュームドライブ文字、ボリュームマウントポイント、または GUID ベースのボリューム名を使用して指定できます。 GUID ベースのボリューム名を使用する場合は、円記号 (\\) で終了する必要があります。 ファイルへのパスを指定する場合は、ファイル名にワイルドカード文字 (\*) を使用できます。 **-BackupTarget**パラメーターが使用されている場合にのみ使用してください。|
|-nonRecurseExclude|Windows °7および Windows Server 2008 R2 以降では、は、バックアップから除外する、非再帰的でコンマ区切りのリストを指定します。 ファイル、フォルダー、またはボリュームを除外することができます。 ボリュームパスは、ボリュームドライブ文字、ボリュームマウントポイント、または GUID ベースのボリューム名を使用して指定できます。 GUID ベースのボリューム名を使用する場合は、円記号 (\\) で終了する必要があります。 ファイルへのパスを指定する場合は、ファイル名にワイルドカード文字 (\*) を使用できます。 **-BackupTarget**パラメーターが使用されている場合にのみ使用してください。|
|-allCritical|すべての重要なボリューム (オペレーティングシステムの状態を含むボリューム) をバックアップに含めることを指定します。 このパラメーターは、ベアメタル回復用のバックアップを作成する場合に便利です。 **-BackupTarget**が指定されている場合にのみ使用する必要があります。指定しない場合、コマンドは失敗します。 は、 **-include**オプションと共に使用できます。</br>ヒント:重要なボリュームのバックアップのターゲットボリュームにはローカルドライブを指定できますが、バックアップに含まれているボリュームを指定することはできません。|
|-systemState|Windows °7および Windows Server 2008 R2 以降では、 **-include**パラメーターで指定した他の項目に加えて、システム状態を含むバックアップが作成されます。 システム状態には、ブートファイル (Boot.ini、NDTLDR、NTDetect.com) が含まれています。これには、COM 設定、SYSVOL (グループポリシーとログオンスクリプト)、Active Directory と NTDS などの Windows レジストリが含まれます。ドメインコントローラー上の DIT、および証明書サービスがインストールされている場合は、証明書ストア。 サーバーに Web サーバーの役割がインストールされている場合は、IIS メタディレクトリが含まれます。 サーバーがクラスターの一部である場合は、クラスターサービスの情報も含まれます。|
|-noVerify|リムーバブルメディア (DVD など) に保存されたバックアップにエラーがないかどうかを確認しないように指定します。 このパラメーターを使用しない場合、リムーバブルメディアに保存されたバックアップにはエラーがあるかどうかが検証されます。|
|-ユーザー|バックアップがリモート共有フォルダーに保存されている場合、では、フォルダーに対する書き込みアクセス許可を持つユーザー名を指定します。|
|-パスワード|パラメーター **-user**によって指定されたユーザー名のパスワードを指定します。|
|-noInheritAcl|**-User**および **-password**パラメーターによって指定された資格情報に対応するアクセス制御リスト (ACL) のアクセス許可を \\ @ no__t-3 @ no__t-4servername > \\ @ no__t-6sharename > @no__7WindowsImageBackup @ no__t-8 @ no__t-9ComputerBackedUp > 0 (バックアップが格納されているフォルダー)。 後でバックアップにアクセスするには、これらの資格情報を使用するか、共有フォルダーがあるコンピューターの Administrators グループまたは Backup Operators グループのメンバーである必要があります。 **-Noinheritacl**が使用されていない場合、リモート共有フォルダーへのアクセス権を持つすべてのユーザーがバックアップにアクセスできるように、\\ @ No__t-2ComputerBackedUp > フォルダーに対する acl アクセス許可が既定で適用されます。|
|-vssFull|ボリュームシャドウコピーサービス (VSS) を使用して完全バックアップを実行します。 すべてのファイルがバックアップされ、各ファイルの履歴がバックアップされたことを反映して更新され、以前のバックアップのログが切り捨てられる可能性があります。 このパラメーターを使用しない場合、 **wbadmin start backup**はコピーバックアップを作成しますが、バックアップされているファイルの履歴は更新されません。</br>注意:Windows Server バックアップ以外の製品を使用して、現在のバックアップに含まれるボリューム上のアプリケーションをバックアップする場合は、このパラメーターを使用しないでください。 これにより、他のバックアップ製品で作成されている増分バックアップ、差分バックアップ、またはその他の種類のバックアップが壊れる可能性があります。これは、バックアップするデータの量を判断するために依存している履歴が原因で完全バックアップが実行される可能性があるためです。以上.|
|-vssCopy|Windows 7 および Windows Server 2008 R2 以降では、VSS を使用してコピーバックアップを実行します。 すべてのファイルがバックアップされますが、バックアップするファイルの履歴は更新されないため、変更や削除などのファイル、およびアプリケーションログファイルに関するすべての情報が保持されます。 この種類のバックアップを使用しても、このコピーバックアップとは独立して発生する可能性のある増分バックアップと差分バックアップのシーケンスには影響しません。 これは既定値です。</br>警告:増分バックアップまたは差分バックアップや復元では、コピーバックアップを使用できません。|
|-通知の停止|ユーザーにプロンプトを表示せずにサブコマンドを実行します。|

## <a name="BKMK_examples"></a>例

次の例は、さまざまなバックアップシナリオで**wbadmin start backup**コマンドを使用する方法を示しています。

シナリオ #1
- ボリューム e:、d: \\mountpoint、\\ @ no__t-2? \\Volume {cc566d14-4410-11d9-9d93-806e6f6e6963} のバックアップを作成します。
- バックアップをボリューム f: に保存します。
  ```
  wbadmin start backup -backupTarget:f: -include:e:,d:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
  ```
  シナリオ #2
- *F: \\folder1*および*h: \\folder2*から volume *d:* の1回限りのバックアップを実行します。
- システム状態のバックアップ
- 通常のスケジュールされた差分バックアップが影響を受けないように、コピーバックアップを作成します。
  ```
  wbadmin start backup –backupTarget:d: -include:g\folder1,h:\folder2 –systemstate -vsscopy
  ```
  シナリオ #3
- 非再帰的にバックアップする必要がある*d: \\folder1*の1回限りのバックアップを実行します。
- フォルダーをネットワーク上の場所にバックアップ *\\ @ no__t-2backupshare @ no__t-3backup1*
- バックアップへのアクセスを、 **Administrators**グループまたは**backup Operators**グループのメンバーに制限します。
  ```
  wbadmin start backup –backupTarget: \\backupshare\backup1 -noinheritacl -nonrecurseinclude:d:\folder1
  ```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
