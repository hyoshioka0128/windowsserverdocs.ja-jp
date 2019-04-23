---
title: wbadmin バックアップの有効化
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0e57f8a-70fa-4c60-9754-e762e8ad8772
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6fd0bea5da83ca9351d5ea1028c94392bdb40422
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845543"
---
# <a name="wbadmin-enable-backup"></a>wbadmin バックアップの有効化



作成日単位のバックアップ スケジュールを有効または既存のバックアップ スケジュールを変更します。 パラメーターを指定せずには、現在スケジュールされているバックアップの設定が表示されます。

を構成または日単位のバックアップ スケジュールを変更するには、いずれかのメンバーである、**管理者**または**Backup Operators**グループ。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (を開き、管理者特権でコマンド プロンプトを右クリック**コマンド プロンプト**し**管理者として実行**)。

このサブコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

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

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-addtarget|Windows Server 2008 では、バックアップの格納場所を指定します。 ディスクの識別子としてのバックアップの保存先を指定する必要があります (「解説」を参照してください)。 を使用する前にフォーマットされているし、上の既存のデータは完全に消去されます。</br>Windows Server 2008 R2 以降では、バックアップの格納場所を指定します。 ディスク、ボリューム、またはリモート共有フォルダーへの汎用名前付け規則 (UNC) パスとして場所を指定する必要があります (\\\\\<servername >\<sharename >\)します。 既定で、バックアップが保存されます: \\ \\ <servername> \<sharename > \WindowsImageBackup\<名 >\. ディスクを指定する場合、使用する前に、ディスクがフォーマットし、上の既存のデータが完全に消去します。 共有フォルダーを指定する場合より多くの場所を追加することはできません。 1 つの共有フォルダーは、一度に記憶域の場所としてのみ指定できます。</br>重要:リモート共有フォルダーにバックアップを保存する場合は、同じコンピューターを再度バックアップを同じフォルダーを使用する場合にそのバックアップが上書きされます。 さらに、バックアップ操作が失敗した場合が最終的にバックアップが存在、古いバックアップが上書きされますが、新しいバックアップは使用できません。 バックアップを整理するリモート共有フォルダーのサブフォルダーを作成してこれを回避できます。 これを行う場合、サブフォルダーは、親フォルダーの 2 倍の容量を必要があります。</br>1 つのコマンドでは、1 つの場所を指定できます。 コマンドをもう一度実行して、複数のボリュームとディスクのバックアップ ストレージの場所を追加できます。|
|-removetarget|既存のバックアップのスケジュールから削除する記憶域の場所を指定します。 ディスクの識別子として場所を指定する必要があります (「解説」を参照してください)。|
|-スケジュール|バックアップを作成する 1 日の時間を指定します。 HH:MM とコンマ区切りとして書式設定します。|
|-が含まれます|Windows Server 2008 では、ボリュームのドライブ文字、ボリューム マウント ポイント、またはバックアップに含めるには、GUID ベースのボリューム名のコンマ区切りリストを指定します。</br>Windows Server 2008 R2and の後で、バックアップに含める項目のコンマ区切りリストを指定します。 複数のファイル、フォルダー、またはボリュームを含めることができます。 ボリュームのドライブ文字、ボリューム マウント ポイント、または GUID ベースのボリューム名を使用して、ボリュームのパスを指定できます。 GUID ベースのボリューム名を使用する場合、円記号で終了する必要があります (\)します。 ファイルへのパスを指定するときに、ファイル名にワイルドカード文字 (*) を使用することができます。|
|-nonRecurseInclude|Windows Server 2008 R2 以降では、再帰的に、バックアップに含める項目のコンマ区切りの一覧を指定します。 複数のファイル、フォルダー、またはボリュームを含めることができます。 ボリュームのドライブ文字、ボリューム マウント ポイント、または GUID ベースのボリューム名を使用して、ボリュームのパスを指定できます。 GUID ベースのボリューム名を使用する場合、円記号で終了する必要があります (\)します。 ファイルへのパスを指定するときに、ファイル名にワイルドカード文字 (*) を使用することができます。 -Backuptarget パラメーターを使用する場合にのみ使用する必要があります。|
|-除外|Windows Server 2008 R2 以降では、バックアップから除外する項目のコンマ区切りリストを指定します。 ファイル、フォルダー、またはボリュームを除外することができます。 ボリュームのドライブ文字、ボリューム マウント ポイント、または GUID ベースのボリューム名を使用して、ボリュームのパスを指定できます。 GUID ベースのボリューム名を使用する場合、円記号で終了する必要があります (\)します。 ファイルへのパスを指定するときに、ファイル名にワイルドカード文字 (*) を使用することができます。|
|-nonRecurseExclude|Windows Server 2008 R2 以降では、再帰的に、バックアップから除外する項目のコンマ区切りの一覧を指定します。 ファイル、フォルダー、またはボリュームを除外することができます。 ボリュームのドライブ文字、ボリューム マウント ポイント、または GUID ベースのボリューム名を使用して、ボリュームのパスを指定できます。 GUID ベースのボリューム名を使用する場合、円記号で終了する必要があります (\)します。 ファイルへのパスを指定するときに、ファイル名にワイルドカード文字 (*) を使用することができます。|
|-hyperv|バックアップに含まれるコンポーネントのコンマ区切りリストを指定します。 識別子は、コンポーネントの名前または GUID (中かっこの有無にかかわらず) のコンポーネント。|
|-systemState|Windows ° 7 および Windows Server 2008 R2 の後で、使用して指定したその他の項目だけでなく、システム状態を含むバックアップを作成し、 **-含める**パラメーター。 システム状態には、Windows レジストリ、SYSVOL (グループ ポリシーおよびログオン スクリプト)、Active Directory および NTDS COM の設定を含むブート ファイル (Boot.ini、NDTLDR、NTDetect.com など) が含まれています。ドメイン コント ローラー上で DIT と、証明書サービスがインストールされている場合、証明書を格納します。 サーバーにインストールされている Web サーバーの役割がある場合は、IIS メタディレクトリが含まれます。 サーバーがクラスターの一部である場合は、クラスター サービスの情報が含まれることもします。|
|-allCritical|すべての重要なボリューム (オペレーティング システムの状態を含むボリューム) が、バックアップに含まれることを指定します。 このパラメーターは、完全なシステムまたはシステム状態の回復のバックアップを作成する場合に便利です。 -Backuptarget を指定した場合にのみ使用する必要があります、それ以外の場合、コマンドは失敗します。 使用できる、 **-含める**オプション。</br>ヒント:重要なボリュームのバックアップ ターゲット ボリュームがローカルのドライブを指定できますが、バックアップに含まれているボリュームのいずれかにすることはできません。|
|-vssFull|Windows Server 2008 R2 以降で実行完全なバックアップ ボリューム シャドウ コピー サービス (VSS) を使用します。 すべてのファイルのバックアップをそれがバックアップされ、以前のバックアップのログが切り捨てられることを反映するように各ファイルの履歴が更新されます。 このパラメーターを使用しない場合は、wbadmin start backup はバックアップ、コピーを作成しますが、バックアップされるファイルの履歴は更新されません。</br>注意:Windows Server バックアップ以外の製品を使用すると、現在のバックアップに含まれるボリューム上にあるアプリケーションをバックアップしている場合は、このパラメーターを使用しないでください。 行うは、可能性のある破損する可能性が、増分、差分バックアップ、または他の種類をバックアップするデータ量が見つからないことを確認する依存している履歴とそれらが完全なを実行するために、その他のバックアップ製品を作成しているバックアップのバックアップ不必要にします。|
|-vssCopy|Windows Server 2008 R2 以降では、VSS を使用、コピー バックアップを実行します。 すべてのファイルがバックアップされますが、変更、削除、および、どのファイルに、すべての情報のほか、アプリケーションのログ ファイルを保持するため、バックアップ中のファイルの履歴は更新されません。 この種類のバックアップを使用しても、このバックアップ コピーの独立した可能性がある増分バックアップと差分バックアップのシーケンスには影響しません。 これが既定値です。</br>警告:増分または差分バックアップまたは復元は、コピー バックアップを使用できません。|
|-ユーザー|Windows Server 2008 R2 以降では、(リモート共有フォルダーの場合) に、バックアップの保存先に書き込みアクセス許可を持つユーザーを指定します。 ユーザーは、Administrators グループまたは Backup Operators グループにバックアップするコンピューターのメンバーである必要があります。|
|-パスワード|Windows Server 2008 R2 以降では、パラメーターで指定されたユーザー名のパスワードを指定のユーザー。|
|-通知の停止|ユーザーにプロンプトなしで、サブコマンドを実行します。|
|-allowDeleteOldBackups|コンピューターのアップグレード前にすべてのバックアップを上書きします。|

## <a name="remarks"></a>注釈

ディスクのディスク識別子の値を表示するには、次のように入力します。 **wbadmin get ディスク**します。

## <a name="BKMK_examples"></a>例

次の例に示す方法、 **wbadmin には、バックアップが有効にする**コマンドは、さまざまなバックアップ シナリオで使用できます。

シナリオ 1
-   ハード ディスク ドライブのバックアップをスケジュール e:、d:\mountpoint、および\\ \\? \Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
-   ディスク Id のディスクにファイルを保存します。
-   午前 9時 00分に毎日のバックアップを実行します。 午後 6 時まで 
```
wbadmin enable backup -addtarget:DiskID -schedule:09:00,18:00 -include:e:,d:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
```
2 番目のシナリオ
-   ネットワークの場所にフォルダー d:\documents のバックアップをスケジュール\\ \\backupshare\backup1
-   バックアップ管理者、ネットワーク共有へのアクセスを認証する CONTOSOEAST ドメインのメンバーである Aaren Ekelund (aekel) のネットワーク資格情報を使用します。 Aaren のパスワードが *$3 hM 9 ^ 5lp*します。
-   午前 12時 00分に毎日のバックアップを実行します。 午後 7時 00分
```
wbadmin enable backup –addtarget:\\backupshare\backup1 –include: d:\documents –user:CONTOSOEAST\aekel –password:$3hM9^5lp –schedule:00:00,19:00
```
シナリオ 3
-   ドライブ h: にボリューム t: とフォルダーの d:\documents のバックアップはスケジュールが除外フォルダー d:\documents\~tmp
-   ボリューム シャドウ コピー サービスを使用して完全バックアップを実行します。
-   午前 1時 00分に毎日のバックアップを実行します。
```
wbadmin enable backup –addtarget:H: –include T:,D:\documents –exclude D:\documents\~tmp –vssfull –schedule:01:00
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)