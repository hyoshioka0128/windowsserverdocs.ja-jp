---
title: wbadmin start backup
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 09b2ffabcea414dd4717a2ffa1f6e860a17f3653
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871703"
---
# <a name="wbadmin-start-backup"></a>wbadmin start backup



指定されたパラメーターを使用してバックアップを作成します。 パラメーターが指定されていないスケジュールされた毎日のバックアップを作成した場合、このサブコマンドは、スケジュールされたバックアップの設定を使用して、バックアップを作成します。 パラメーターが指定されている場合、ボリューム シャドウ コピー サービス (VSS) のバックアップ コピーを作成しがバックアップされているファイルの履歴は更新されません。

このサブコマンドで 1 回限りのバックアップを作成する、 **Backup Operators**グループまたは**管理者**グループ、またはをされている必要が適切なアクセス許可を委任します。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (を開き、管理者特権でコマンド プロンプトを右クリック**コマンド プロンプト**し**管理者として実行**)。

このサブコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

## <a name="syntax"></a>構文

Windows ° Vista および Windows Server 2008 の構文:
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
Windows ° 7 と Windows Server 2008 R2 の構文とそれ以降。
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
|-backuptarget|このバックアップの格納場所を指定します。 ハード ディスク ドライブ文字 (f:) の形式で、ボリューム GUID に基づくパスが必要で\\ \\? \Volume{GUID}、またはリモート共有フォルダーへの汎用名前付け規則 (UNC) パス (\\\\\<servername >\<sharename >\)します。 既定で、バックアップが保存されます: \\ \\ <servername> \<sharename >\** WindowsImageBackup * *\\<ComputerBackedUp>\.</br>重要:リモート共有フォルダーにバックアップを保存する場合は、同じコンピューターを再度バックアップを同じフォルダーを使用する場合にそのバックアップが上書きされます。 さらに、バックアップ操作が失敗した場合が最終的にバックアップが存在、古いバックアップが上書きされますが、新しいバックアップは使用できません。 バックアップを整理するリモート共有フォルダーのサブフォルダーを作成してこれを回避できます。 これを行うと、サブフォルダーは、親フォルダーと 2 倍の容量を必要があります。|
|-が含まれます|Windows ° Vista および Windows Server 2008、ボリュームのドライブ文字、ボリューム マウント ポイント、またはバックアップに含めるには、GUID ベースのボリューム名のコンマ区切りリストを指定します。 このパラメーターを使用する場合にのみ、 **-backuptarget**パラメーターを使用します。</br>Windows ° 7 および Windows Server 2008 R2 にし、後で、バックアップに含める項目のコンマ区切りリストを指定します。 複数のファイル、フォルダー、またはボリュームを含めることができます。 ボリュームのドライブ文字、ボリューム マウント ポイント、または GUID ベースのボリューム名を使用して、ボリュームのパスを指定できます。 GUID ベースのボリューム名を使用する場合、円記号で終了する必要があります (\\)。 ワイルドカード文字を使用することができます (\*) ファイルへのパスを指定するときに、ファイル名にします。 使用する場合にのみ、 **-backuptarget**パラメーターを使用します。|
|-除外|Windows ° 7 および Windows Server 2008 R2 にし、後で、バックアップから除外する項目のコンマ区切りリストを指定します。 ファイル、フォルダー、またはボリュームを除外することができます。 ボリュームのドライブ文字、ボリューム マウント ポイント、または GUID ベースのボリューム名を使用して、ボリュームのパスを指定できます。 GUID ベースのボリューム名を使用する場合、円記号で終了する必要があります (\\)。 ワイルドカード文字を使用することができます (\*) ファイルへのパスを指定するときに、ファイル名にします。 使用する場合にのみ、 **-backuptarget**パラメーターを使用します。|
|-nonRecurseInclude|Windows ° 7 および Windows Server 2008 R2 の後で、再帰的に、バックアップに含める項目のコンマ区切りの一覧を指定します。 複数のファイル、フォルダー、またはボリュームを含めることができます。 ボリュームのドライブ文字、ボリューム マウント ポイント、または GUID ベースのボリューム名を使用して、ボリュームのパスを指定できます。 GUID ベースのボリューム名を使用する場合、円記号で終了する必要があります (\\)。 ワイルドカード文字を使用することができます (\*) ファイルへのパスを指定するときに、ファイル名にします。 使用する場合にのみ、 **-backuptarget**パラメーターを使用します。|
|-nonRecurseExclude|Windows ° 7 および Windows Server 2008 R2 の後で、再帰的に、バックアップから除外する項目のコンマ区切りの一覧を指定します。 ファイル、フォルダー、またはボリュームを除外することができます。 ボリュームのドライブ文字、ボリューム マウント ポイント、または GUID ベースのボリューム名を使用して、ボリュームのパスを指定できます。 GUID ベースのボリューム名を使用する場合、円記号で終了する必要があります (\\)。 ワイルドカード文字を使用することができます (\*) ファイルへのパスを指定するときに、ファイル名にします。 使用する場合にのみ、 **-backuptarget**パラメーターを使用します。|
|-allCritical|すべての重要なボリューム (オペレーティング システムの状態を含むボリューム) が、バックアップに含まれることを指定します。 このパラメーターは、ベア メタル回復のバックアップを作成する場合に便利です。 使用する場合にのみ **-backuptarget**が指定すると、それ以外の場合、コマンドは失敗します。 使用できる、 **-含める**オプション。</br>ヒント:重要なボリュームのバックアップ ターゲット ボリュームがローカルのドライブを指定できますが、バックアップに含まれているボリュームのいずれかにすることはできません。|
|-systemState|Windows ° 7 および Windows Server 2008 R2 の後で、使用して指定したその他の項目だけでなく、システム状態を含むバックアップを作成し、 **-含める**パラメーター。 システム状態には、Windows レジストリ、SYSVOL (グループ ポリシーおよびログオン スクリプト)、Active Directory および NTDS COM の設定を含むブート ファイル (Boot.ini、NDTLDR、NTDetect.com など) が含まれています。ドメイン コント ローラー上で DIT と、証明書サービスがインストールされている場合、証明書を格納します。 サーバーにインストールされている Web サーバーの役割がある場合は、IIS メタディレクトリが含まれます。 サーバーがクラスターの一部である場合は、クラスター サービスの情報も含まれます。|
|-noVerify|エラーのリムーバブル メディア (DVD など) に保存されているバックアップが検証されないことを指定します。 このパラメーターを使用しない場合は、エラーのリムーバブル メディアに保存されているバックアップが検証されます。|
|-ユーザー|バックアップは、リモート共有フォルダーに保存する場合は、フォルダーに対する書き込み権限を持つユーザー名を指定します。|
|-パスワード|パラメーターによって提供されるユーザー名のパスワードを示す **-ユーザー**します。|
|-noInheritAcl|によって提供される資格情報に対応するアクセス制御リスト (ACL) のアクセス許可を適用、 **-ユーザー**と **-パスワード**パラメーター \\ \\ \<servername >\<sharename > \WindowsImageBackup\<名 > \ (バックアップを含むフォルダー)。 後で、バックアップにアクセスするには、これらの資格情報を使用して、または Administrators グループまたはコンピューターの共有フォルダーで、Backup Operators グループのメンバーである必要があります。 場合 **- noInheritAcl**が使用されていないリモート共有フォルダーの ACL のアクセス許可に適用されます、\<名 > フォルダーが既定では、リモート共有フォルダーへのアクセス権を持つのすべての人が、バックアップにアクセスできるようにします。|
|-vssFull|ボリューム シャドウ コピー サービス (VSS) を使用しての完全バックアップを実行します。 すべてのファイルのバックアップをそれがバックアップされ、以前のバックアップのログが切り捨てられることを反映するように各ファイルの履歴が更新されます。 このパラメーターを使用しない場合**wbadmin start backup**コピー バックアップがバックアップされているは更新されていないファイルの履歴になります。</br>注意:Windows Server バックアップ以外の製品を使用すると、現在のバックアップに含まれるボリューム上にあるアプリケーションをバックアップしている場合は、このパラメーターを使用しないでください。 行うは、可能性のある破損する可能性が、増分、差分バックアップ、または他の種類をバックアップするデータ量が見つからないことを確認する依存している履歴とそれらが完全なを実行するために、その他のバックアップ製品を作成しているバックアップのバックアップ不必要にします。|
|-vssCopy|Windows 7 および Windows Server 2008 R2 し、後で VSS を使用、コピー バックアップを実行します。 すべてのファイルがバックアップされますが、変更、削除、および、どのファイルに、すべての情報のほか、アプリケーションのログ ファイルを保持するため、バックアップ中のファイルの履歴は更新されません。 この種類のバックアップを使用しても、このバックアップ コピーの独立した可能性がある増分バックアップと差分バックアップのシーケンスには影響しません。 これが既定値です。</br>警告:増分または差分バックアップまたは復元は、コピー バックアップを使用できません。|
|-通知の停止|ユーザーにプロンプトなしで、サブコマンドを実行します。|

## <a name="BKMK_examples"></a>例

次の例に示す方法、 **wbadmin start backup**コマンドは、さまざまなバックアップ シナリオで使用できます。

シナリオ 1
-   ボリュームのバックアップを作成 e:、d:\mountpoint、および\\ \\? \Volume{cc566d14-4410-11d9-9d93-806e6f6e6963}
-   ボリューム f: をバックアップを保存します。
```
wbadmin start backup -backupTarget:f: -include:e:,d:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
```
2 番目のシナリオ
-   1 回限りのバックアップを実行*f:\folder1*と*h:\folder2*ボリュームに*d:* します。
-   システム状態のバックアップ
-   通常のスケジュールの差分バックアップに影響が及ばないように、コピー バックアップを作成します。
```
wbadmin start backup –backupTarget:d: -include:g\folder1,h:\folder2 –systemstate -vsscopy
```
シナリオ 3
-   1 回限りのバックアップを実行*d:\folder1*非再帰的にバックアップする必要があります。
-   ネットワークの場所にフォルダーをバックアップ *\\ \\backupshare\backup1*
-   メンバーへのバックアップへのアクセス制限、**管理者**または**Backup Operators**グループ。
```
wbadmin start backup –backupTarget: \\backupshare\backup1 -noinheritacl -nonrecurseinclude:d:\folder1
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
