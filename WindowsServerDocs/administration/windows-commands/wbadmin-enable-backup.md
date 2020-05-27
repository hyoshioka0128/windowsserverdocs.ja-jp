---
title: wbadmin のバックアップの有効化
description: Wbadmin enable backup のリファレンストピックでは、毎日のバックアップスケジュールを作成して有効にしたり、既存のバックアップスケジュールを変更したりします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0e57f8a-70fa-4c60-9754-e762e8ad8772
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 46ca7a4bf6790ff9ec071bea15be278c18533dab
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821392"
---
# <a name="wbadmin-enable-backup"></a>wbadmin のバックアップの有効化



毎日のバックアップスケジュールを作成して有効にするか、既存のバックアップスケジュールを変更します。 パラメーターを指定しない場合は、現在スケジュールされているバックアップの設定が表示されます。

毎日のバックアップスケジュールを構成または変更するには、 **Administrators**グループまたは**backup Operators**グループのメンバーである必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、[**コマンドプロンプト**] を右クリックし、[**管理者として実行**] をクリックします)。

## <a name="syntax"></a>構文

Windows Server 2008 の構文:
```
wbadmin enable backup
[-addtarget:<BackupTargetDisk>]
[-removetarget:<BackupTargetDisk>]
[-schedule:<TimeToRunBackup>]
[-include:<VolumesToInclude>]
[-allCritical]
[-quiet]
```
Windows Server 2008 R2 の構文:
```
wbadmin enable backup
[-addtarget:<BackupTarget>]
[-removetarget:<BackupTarget>]
[-schedule:<TimeToRunBackup>]
[-include:<VolumesToInclude>]
[-nonRecurseInclude:<ItemsToInclude>]
[-exclude:<ItemsToExclude>]
[-nonRecurseExclude:<ItemsToExclude>][-systemState]
[-allCritical]
[-vssFull | -vssCopy]
[-user:<UserName>]
[-password:<Password>]
[-quiet]
```
Windows Server 2012 および Windows Server 2012 R2 の構文:
```
wbadmin enable backup
[-addtarget:<BackupTarget>]
[-removetarget:<BackupTarget>]
[-schedule:<TimeToRunBackup>]
[-include:<VolumesToInclude>]
[-nonRecurseInclude:<ItemsToInclude>]
[-exclude:<ItemsToExclude>]
[-nonRecurseExclude:<ItemsToExclude>][-systemState]
[-hyperv:<HyperVComponentsToExclude>]
[-allCritical]
[-systemState]
[-vssFull | -vssCopy]
[-user:<UserName>]
[-password:<Password>]
[-quiet]
[-allowDeleteOldBackups]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-addtarget|Windows Server 2008 の場合は、バックアップの保存場所を指定します。 ディスク識別子としてバックアップの保存先を指定する必要があります (「解説」を参照してください)。 ディスクは使用前にフォーマットされ、そのディスク上の既存のデータは完全に消去されます。</br>Windows Server 2008 R2 以降では、バックアップの保存場所を指定します。 リモート共有フォルダー ( \\ \\ \< servername>sharename>のディスク、ボリューム、または汎用名前付け規則 (UNC) パスとして、場所を指定する必要があり \< \) ます。 既定では、バックアップは: \\ \\ <servername> \< sharename> \windowsimagebackup ComputerBackedUp に保存され \<>\. ディスクを指定すると、使用前にディスクがフォーマットされ、そのディスク上の既存のデータが完全に消去されます。 共有フォルダーを指定する場合、場所を追加することはできません。 共有フォルダーは、一度に1つのストレージの場所としてのみ指定できます。</br>重要: バックアップをリモート共有フォルダーに保存すると、同じフォルダーを使用して同じコンピューターを再度バックアップすると、そのバックアップが上書きされます。 またバックアップ操作が失敗したとき、古いバックアップは上書きされ、新しいバックアップが使用できなくなるため、結果としてバックアップが存在しなくなる場合があります。 このような問題を回避するために、リモート共有フォルダーにサブフォルダーを作成してバックアップを整理することができます。 この場合、サブフォルダーには親フォルダーの2倍の領域が必要になります。</br>1つのコマンドで指定できる場所は1つだけです。 コマンドを再実行して、複数のボリュームおよびディスクバックアップの記憶域の場所を追加できます。|
|-removetarget|既存のバックアップスケジュールから削除する記憶域の場所を指定します。 ディスク識別子として場所を指定する必要があります (「解説」を参照してください)。|
|-スケジュール|バックアップを作成する時刻を HH: MM およびコンマ区切りの形式で指定します。|
|-含める|Windows Server 2008 では、ボリュームドライブ文字、ボリュームマウントポイント、またはバックアップに含める GUID ベースのボリューム名のコンマ区切りのリストを指定します。</br>Windows Server 2008 R2and 以降では、バックアップに含める項目のコンマ区切りの一覧を指定します。 複数のファイル、フォルダー、またはボリュームを含めることができます。 ボリュームパスは、ボリュームドライブ文字、ボリュームマウントポイント、または GUID ベースのボリューム名を使用して指定できます。 GUID ベースのボリューム名を使用する場合は、円記号 () で終わる必要があり \) ます。 ファイルへのパスを指定する場合は、ファイル名にワイルドカード文字 (*) を使用できます。|
|-nonRecurseInclude|Windows Server 2008 R2 以降では、は、バックアップに含める項目の非再帰的なコンマ区切りのリストを指定します。 複数のファイル、フォルダー、またはボリュームを含めることができます。 ボリュームパスは、ボリュームドライブ文字、ボリュームマウントポイント、または GUID ベースのボリューム名を使用して指定できます。 GUID ベースのボリューム名を使用する場合は、円記号 () で終わる必要があり \) ます。 ファイルへのパスを指定する場合は、ファイル名にワイルドカード文字 (*) を使用できます。 -BackupTarget パラメーターが使用されている場合にのみ使用してください。|
|-除外|Windows Server 2008 R2 以降では、バックアップから除外する項目のコンマ区切りリストを指定します。 ファイル、フォルダー、またはボリュームを除外することができます。 ボリュームパスは、ボリュームドライブ文字、ボリュームマウントポイント、または GUID ベースのボリューム名を使用して指定できます。 GUID ベースのボリューム名を使用する場合は、円記号 () で終わる必要があり \) ます。 ファイルへのパスを指定する場合は、ファイル名にワイルドカード文字 (*) を使用できます。|
|-nonRecurseExclude|Windows Server 2008 R2 以降では、バックアップから除外する、非再帰的でコンマ区切りのリストを指定します。 ファイル、フォルダー、またはボリュームを除外することができます。 ボリュームパスは、ボリュームドライブ文字、ボリュームマウントポイント、または GUID ベースのボリューム名を使用して指定できます。 GUID ベースのボリューム名を使用する場合は、円記号 () で終わる必要があり \) ます。 ファイルへのパスを指定する場合は、ファイル名にワイルドカード文字 (*) を使用できます。|
|-hyperv|バックアップに含めるコンポーネントのコンマ区切りの一覧を指定します。 識別子には、コンポーネント名またはコンポーネント GUID (中かっこの有無を含む) を指定できます。|
|-systemState|Windows °7および Windows Server 2008 R2 以降では、 **-include**パラメーターで指定した他の項目に加えて、システム状態を含むバックアップが作成されます。 システム状態には、ブートファイル (Boot.ini、NDTLDR、NTDetect.com) が含まれています。これには、COM 設定、SYSVOL (グループポリシーとログオンスクリプト)、Active Directory と NTDS などの Windows レジストリが含まれます。ドメインコントローラー上の DIT、および証明書サービスがインストールされている場合は、証明書ストア。 サーバーに Web サーバーの役割がインストールされている場合は、IIS メタディレクトリが含まれます。 サーバーがクラスターの一部である場合は、クラスターサービス情報も含まれます。|
|-allCritical|すべての重要なボリューム (オペレーティングシステムの状態を含むボリューム) をバックアップに含めることを指定します。 このパラメーターは、完全なシステムまたはシステム状態の回復用のバックアップを作成する場合に便利です。 -BackupTarget が指定されている場合にのみ使用する必要があります。指定しない場合、コマンドは失敗します。 は、 **-include**オプションと共に使用できます。</br>ヒント: 重要なボリュームのバックアップのターゲットボリュームにはローカルドライブを指定できますが、バックアップに含まれるボリュームを指定することはできません。|
|-vssFull|Windows Server 2008 R2 以降では、はボリュームシャドウコピーサービス (VSS) を使用して完全バックアップを実行します。 すべてのファイルがバックアップされ、各ファイルの履歴がバックアップされたことを反映して更新され、以前のバックアップのログが切り捨てられる可能性があります。 このパラメーターを使用しない場合、wbadmin start backup はコピーバックアップを作成しますが、バックアップされているファイルの履歴は更新されません。</br>注意: Windows Server バックアップ以外の製品を使用して、現在のバックアップに含まれているボリューム上のアプリケーションをバックアップする場合は、このパラメーターを使用しないでください。 これにより、他のバックアップ製品が作成している増分バックアップ、差分バックアップ、その他の種類のバックアップが壊れる可能性があります。これは、バックアップするデータの量を判断するために依存している履歴があるため、不要な完全バックアップを実行する可能性があるためです。|
|-vssCopy|Windows Server 2008 R2 以降では、VSS を使用してコピーバックアップを実行します。 すべてのファイルがバックアップされますが、バックアップするファイルの履歴は更新されないため、変更や削除などのファイル、およびアプリケーションログファイルに関するすべての情報が保持されます。 この種類のバックアップを使用しても、このコピーバックアップとは独立して発生する可能性のある増分バックアップと差分バックアップのシーケンスには影響しません。 これが既定値です。</br>警告: コピーバックアップは、増分バックアップまたは差分バックアップまたは復元には使用できません。|
|-ユーザー|Windows Server 2008 R2 以降では、バックアップストレージの宛先 (リモート共有フォルダーの場合) への書き込みアクセス許可を持つユーザーを指定します。 ユーザーは、バックアップするコンピューターの Administrators グループまたは Backup Operators グループのメンバーである必要があります。|
|-パスワード|Windows Server 2008 R2 以降では、-user パラメーターによって指定されたユーザー名のパスワードを指定します。|
|-quiet|ユーザーにプロンプトを表示せずにサブコマンドを実行します。|
|-allowDeleteOldBackups|コンピューターをアップグレードする前に行われたすべてのバックアップを上書きします。|

## <a name="remarks"></a>注釈

ディスクのディスク id 値を表示するには、「 **wbadmin get disks**」と入力します。

## <a name="examples"></a>例

次の例は、さまざまなバックアップシナリオで**wbadmin enable backup**コマンドを使用する方法を示しています。

シナリオ #1
- ハードディスクドライブ e:、d:\mountpoint、 \\ ? \Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\ のバックアップをスケジュールする \\
- ファイルをディスク DiskID に保存します。
- 毎日午前9:00 にバックアップを実行する 午後 6 時まで 
  ```
  wbadmin enable backup -addtarget:DiskID -schedule:09:00,18:00 -include:e:,d:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
  ```
  シナリオ #2
- D:\documents フォルダーのバックアップをネットワーク上の場所 backupshare\backup1 にスケジュールします。 \\ \\
- バックアップ管理者 Aaren (aekel) のネットワーク資格情報を使用します。これは、ネットワーク共有へのアクセスを認証するためのドメイン CONTOSOEAST のメンバーです。 パスワードは *$ 3Hm9 ^ 5lp*です。
- 毎日午前12:00 にバックアップを実行する および 7:00 pm
  ```
  wbadmin enable backup –addtarget:\\backupshare\backup1 –include: d:\documents –user:CONTOSOEAST\aekel –password:$3hM9^5lp –schedule:00:00,19:00
  ```
  シナリオ #3
- ボリューム t: とフォルダー d:\documents のバックアップをドライブ h: にスケジュールしますが、d:\documents tmp フォルダーは除外します。 \~
- ボリュームシャドウコピーサービスを使用して完全バックアップを実行します。
- 毎日午前1:00 にバックアップを実行する
  ```
  wbadmin enable backup –addtarget:H: –include T:,D:\documents –exclude D:\documents\~tmp –vssfull –schedule:01:00
  ```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)