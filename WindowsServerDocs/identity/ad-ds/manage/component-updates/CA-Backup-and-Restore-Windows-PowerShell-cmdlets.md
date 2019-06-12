---
ms.assetid: 7e195f5b-b194-40f3-a26d-5cf4ade5fc4d
title: CA のバックアップと復元の Windows PowerShell コマンドレット
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 6055d9b694f72a6a874acdcb5135fde61bcf0d76
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442751"
---
# <a name="ca-backup-and-restore-windows-powershell-cmdlets"></a>CA のバックアップと復元の Windows PowerShell コマンドレット

> 適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012
> 
> **作成者**:Justin Turner、シニア サポート エスカレーション エンジニア、Windows グループ  
> 
> [!NOTE]
> この内容は Microsoft カスタマー サポート エンジニアによって作成され、TechNet が通常提供しているトピックよりも詳細な Windows Server 2012 R2 の機能やソリューションの技術的説明を求めている、経験豊かな管理者とシステム設計者を対象としています。 ただし、TechNet と同様の編集過程は実施されていないため、言語によっては通常より洗練されていない文章が見られる場合があります。  
  
## <a name="overview"></a>概要  
ADCSAdministration Windows PowerShell モジュールは、Window Server 2012 で導入されました。  2 つの新しいコマンドレットは、バックアップと CA の復元をサポートするために、Window Server 2012 R2 では、このモジュールに追加されました。  
  
-   Backup-CARoleService  
  
-   Restore-CARoleService  
  
## <a name="backup-caroleservice"></a>Backup-CARoleService  
**SEQ テーブル\\\*アラビア語の 17。バックアップと復元の Windows PowerShell コマンドレット**  
  
**ADCSAdministration コマンドレット:Backup-caroleservice**  
  
|引数 -**太字**引数は必須です|説明|  
|------------------------------------------------|---------------|  
|**-Path**|-文字列 - バックアップを保存する場所<br />-無名のパラメーターこれは、唯一<br />位置指定パラメーター<br /><br />**例:**<br /><br />バックアップ-CARoleService-パス c:\adcsbackup1。<br /><br />Backup-CARoleService c:\adcsbackup2|  
|-KeyOnly|-データベースがない場合、CA 証明書をバックアップします。<br /><br />**例:**<br /><br />Backup-CARoleService c:\adcsbackup3 -KeyOnly|  
|-Password|-CA 証明書と秘密キーを保護するパスワードを指定します。<br />でセキュリティで保護された文字列なければなりません<br />の-DatabaseOnly パラメーター場合は無効です。<br /><br />以下に例を示します。<br /><br />Backup-CARoleService c:\adcsbackup4 -Password (Read-Host -prompt "Password:" -AsSecureString)<br /><br />Backup-caroleservice c:\adcsbackup5-パスワード (Convertto-securestring"Pa55w0rd!" -AsPlainText -Force)|  
|-DatabaseOnly|-CA 証明書がないデータベースをバックアップします。<br /><br />Backup-CARoleService c:\adcsbackup6 -DatabaseOnly|  
|-Force|1. 指定した場所に preexists バックアップを上書きすることができます、-path パラメーターで<br /><br />Backup-CARoleService c:\adcsbackup1 -Force|  
|-増分|-増分バックアップを実行します。<br /><br />Backup-CARoleService c:\adcsbackup7 -Incremental|  
|-KeepLog|1. ログ ファイルを保持するコマンドに指示します。 スイッチが指定されていない場合、増分のシナリオでの既定以外によってログ ファイルが切り捨てられます<br /><br />Backup-CARoleService c:\adcsbackup7 -KeepLog|  
  
### <a name="-password-secure-string"></a>-Password <Secure String>  
場合は、パスワード パラメーターを使用すると、指定されたパスワードはセキュリティで保護された文字列である必要があります。  使用して、 **Read-host**コマンドレットをセキュリティで保護されたパスワードの入力の対話型のプロンプトを起動またはを使用して、 **Convertto-securestring** -行のパスワードを指定するコマンドレットです。  
  
次の例を確認してください。  
  
**読み取りホストを使用するパスワード パラメーターのセキュリティで保護された文字列を指定します。**  
  
```powershell  
Backup-CARoleService c:\adcsbackup4 -Password (Read-Host -prompt "Password:" -AsSecureString)  
```  
  
**セキュリティで保護された文字列を Convertto-securestring を使用して、パスワード パラメーターを指定します。**  
  
```powershell  
Backup-CARoleService c:\adcsbackup5 -Password (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText -Force)  
```  
  
## <a name="restore-caroleservice"></a>Restore-CARoleService  
**ADCSAdministration コマンドレット:Restore-caroleservice**  
  
|引数 -**太字**引数は必須です|説明|  
|------------------------------------------------|---------------|  
|**-Path**|-文字列 - バックアップから復元する場所<br />-無名のパラメーターこれは、唯一<br />位置指定パラメーター<br /><br />**例:**<br /><br />Restore-CARoleService.-Path c:\adcsbackup1 -Force<br /><br />Restore-CARoleService c:\adcsbackup2 -Force|  
|-KeyOnly|-データベースがない場合、CA 証明書を復元します。<br />の-KeyOnly オプションを使用して、バックアップが作成されたかどうかは指定必要があります。<br /><br />**例:**<br /><br />Restore-CARoleService c:\adcsbackup3 -KeyOnly -Force|  
|-Password|-CA 証明書と秘密キーのパスワードを指定します。<br />でセキュリティで保護された文字列なければなりません<br /><br />**例:**<br /><br />Restore-CARoleService c:\adcsbackup4 -Password (read-host -prompt "Password:" -AsSecureString) -Force<br /><br />Restore-caroleservice c:\adcsbackup5-パスワード (Convertto-securestring"Pa55w0rd!" -AsPlainText -Force) -Force|  
|-DatabaseOnly|-CA 証明書がないデータベースを復元します。<br /><br />Restore-CARoleService c:\adcsbackup6 -DatabaseOnly|  
|-Force|-既存のキーを上書きする許可します。<br />-は、オプションのパラメーターがインプレースを復元する場合は、必要な可能性があります。<br /><br />Restore-CARoleService c:\adcsbackup1 -Force|  
  
### <a name="issues"></a>Issues  
Convertto-securestring 関数は、Backup-caroleservice の使用中に失敗した場合に非パスワード保護されているバックアップが実行されますパスワード パラメーターを使用します。  
  
![CA のバックアップと復元](media/CA-Backup-and-Restore-Windows-PowerShell-cmdlets/GTR_ADDS_BackupCARole.gif)  
  
**SEQ テーブル\\\*アラビア語の 18。一般的なエラー**  
  
|アクション|エラー|Comment|  
|----------|---------|-----------|  
|**Restore-CARoleService C:\ADCSBackup**|Restore-caroleservice:プロセスはファイルにアクセスできません。 (HRESULT からの例外:<br /><br />0x80070020)|Restore-caroleservice コマンドレットを実行する前に Active Directory Certificate Services サービスを停止します|  
|**Restore-CARoleService C:\ADCSBackup**|Restore-caroleservice:ディレクトリが空ではありません。 (HRESULT からの例外: 0x80070091)|使用して既存のキーを上書きする-force パラメーター|  
|**Backup-CARoleService C:\ADCSBackup -Password (Read-Host -Prompt "Password:" -AsSecureString) -DatabaseOnly**|Backup-caroleservice:パラメーター セットを解決できない、指定した名前付きパラメーター。|パスワード パラメーターは、秘密キーを保護し、有効でないためをバックアップしているないときにのみパスワードを使用|  
|**Restore-CARoleService C:\ADCSBack15 -Password (Read-Host -Prompt "Password:" -AsSecureString) -DatabaseOnly**|Restore-caroleservice:パラメーター セットを解決できない、指定した名前付きパラメーター。|パスワード パラメーターは、秘密キーを保護し、有効でないために復元しない場合にのみパスワードを使用|  
|**Restore-CARoleService C:\ADCSBack14 -Password (Read-Host -Prompt "Password:" -AsSecureString)**|Restore-caroleservice:指定されたファイルが見つかりません。 (HRESULT からの例外: 0x80070002)|指定されたパスに有効なデータベースのバックアップが含まれていません。  おそらく、パスが無効または -KeysOnly オプションを使用して、バックアップが作成されたか。|  
  
## <a name="additional-resources"></a>その他のリソース  
[Active Directory 証明書サービス移行ガイド](https://technet.microsoft.com/library/ee126170(v=ws.10).aspx)  
  
[CA データベースおよび秘密キーのバックアップ](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_BackUpDB)  
  
[移行先サーバーでの CA データベースおよび構成の復元](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_RestoreCA)  
  
## <a name="try-this-backup-the-ca-in-your-lab-using-windows-powershell"></a>これを試してください。Windows PowerShell を使用してラボ内の CA をバックアップします。  
  
1.  このレッスンではコマンドを使用して、CA データベースと、パスワードで保護されている秘密キーをバックアップします。  
  
2.  この時点で、CA の復元を留保します。  
  


