---
ms.assetid: 7e195f5b-b194-40f3-a26d-5cf4ade5fc4d
title: CA のバックアップと復元の Windows PowerShell コマンドレット
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 796c10d36428e088f3c1fffe293fc7c414993eb2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389958"
---
# <a name="ca-backup-and-restore-windows-powershell-cmdlets"></a>CA のバックアップと復元の Windows PowerShell コマンドレット

> 適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012
> 
> **作成者**:Justin 書籍、シニアサポートエスカレーションエンジニア (Windows グループ)  
> 
> [!NOTE]
> この内容は Microsoft カスタマー サポート エンジニアによって作成され、TechNet が通常提供しているトピックよりも詳細な Windows Server 2012 R2 の機能やソリューションの技術的説明を求めている、経験豊かな管理者とシステム設計者を対象としています。 ただし、TechNet と同様の編集過程は実施されていないため、言語によっては通常より洗練されていない文章が見られる場合があります。  
  
## <a name="overview"></a>概要  
ADCSAdministration Windows PowerShell モジュールは、Windows Server 2012 で導入されました。  Windows Server 2012 R2 では、CA のバックアップと復元をサポートするために、このモジュールに2つの新しいコマンドレットが追加されました。  
  
-   Backup-CARoleService  
  
-   Restore-CARoleService  
  
## <a name="backup-caroleservice"></a>Backup-CARoleService  
**Table SEQ テーブル \\ @ no__t: 2 アラビア 17:Windows PowerShell コマンドレットのバックアップと復元 @ no__t-0  
  
@no__t 0ADCSAdministration コマンドレット:Backup-caroleservice @ no__t-0  
  
|引数-**太字**の引数が必要です|説明|  
|------------------------------------------------|---------------|  
|**-Path**|-String-バックアップを保存する場所<br />-唯一の名前のないパラメーターです。<br />-位置指定パラメーター<br /><br />**例:**<br /><br />Backup-caroleservice.-Path c:\ adcsbackup1<br /><br />バックアップ-Backup-caroleservice c:\ adcsbackup2|  
|-KeyOnly|-データベースを使用せずに CA 証明書をバックアップする<br /><br />**例:**<br /><br />バックアップ-Backup-caroleservice c:\ adcsbackup3-KeyOnly|  
|-Password|-CA 証明書と秘密キーを保護するためのパスワードを指定します。<br />-セキュリティで保護された文字列である必要があります<br />--DatabaseOnly パラメーターと共に使用することはできません。<br /><br />例:<br /><br />バックアップ-Backup-caroleservice c:\ adcsbackup4-Password (読み取りホスト-プロンプト "Password:"-AsSecureString)<br /><br />バックアップ-Backup-caroleservice c:\ adcsbackup5-Password (Convertto-html-SecureString "Pa55w0rd!" -AsPlainText-Force)|  
|-DatabaseOnly|-CA 証明書を使用せずにデータベースをバックアップします。<br /><br />バックアップ-Backup-caroleservice c:\ adcsbackup6-DatabaseOnly|  
|-Force|1. -Path パラメーターで指定した場所に存在するバックアップを上書きすることを許可します。<br /><br />バックアップ-Backup-caroleservice c:\ adcsbackup1-Force|  
|-増分|-増分バックアップを実行します<br /><br />バックアップ-Backup-caroleservice c:\ adcsbackup7-増分|  
|-KeepLog|1. ログファイルを保持するようにコマンドに指示します。 スイッチが指定されていない場合、増分のシナリオ以外では、ログファイルは既定で切り捨てられます。<br /><br />バックアップ-Backup-caroleservice c:\ adcsbackup7-KeepLog|  
  
### <a name="-password-secure-string"></a>-Password <Secure String>  
-Password パラメーターを使用する場合、指定するパスワードはセキュリティで保護された文字列である必要があります。  **Read Host**コマンドレットを使用して、セキュリティで保護されたパスワードの入力を求める対話型プロンプトを起動するか、 **convertto-html**コマンドレットを使用してパスワードをインラインで指定します。  
  
次の例を確認します。  
  
**読み取りホストを使用してパスワードパラメーターにセキュリティで保護された文字列を指定する**  
  
```powershell  
Backup-CARoleService c:\adcsbackup4 -Password (Read-Host -prompt "Password:" -AsSecureString)  
```  
  
**Convertto-html を使用して Password パラメーターにセキュリティで保護された文字列を指定する-SecureString**  
  
```powershell  
Backup-CARoleService c:\adcsbackup5 -Password (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText -Force)  
```  
  
## <a name="restore-caroleservice"></a>Restore-CARoleService  
@no__t 0ADCSAdministration コマンドレット:Backup-caroleservice @ no__t-0  
  
|引数-**太字**の引数が必要です|説明|  
|------------------------------------------------|---------------|  
|**-Path**|-文字列-バックアップの復元元の場所<br />-唯一の名前のないパラメーターです。<br />-位置指定パラメーター<br /><br />**例:**<br /><br />Backup-caroleservice.-Path c:\ adcsbackup1-Force<br /><br />復元-Backup-caroleservice c:\ adcsbackup2-Force|  
|-KeyOnly|-データベースを使用せずに CA 証明書を復元する<br />--KeyOnly オプションを使用してバックアップを実行した場合は、を指定する必要があります。<br /><br />**例:**<br /><br />Backup-caroleservice c:\ adcsbackup3-KeyOnly-Force|  
|-Password|-CA 証明書と秘密キーのパスワードを指定します。<br />-セキュリティで保護された文字列である必要があります<br /><br />**例:**<br /><br />Backup-caroleservice c:\ adcsbackup4-Password (read-host-prompt "Password:"-AsSecureString)-Force<br /><br />Backup-caroleservice c:\ adcsbackup5-Password (Convertto-html-SecureString "Pa55w0rd!" -AsPlainText-Force)-Force|  
|-DatabaseOnly|-CA 証明書を使用せずにデータベースを復元します。<br /><br />復元-Backup-caroleservice c:\ adcsbackup6-DatabaseOnly|  
|-Force|-既存のキーを上書きすることを許可します。<br />-省略可能なパラメーターですが、インプレースで復元する場合は、<br /><br />復元-Backup-caroleservice c:\ adcsbackup1-Force|  
  
### <a name="issues"></a>Issues  
パスワードで保護されていないバックアップは、Convertto-html SecureString 関数が-Password パラメーターを指定して Backup-caroleservice を使用して失敗した場合に実行されます。  
  
![CA のバックアップと復元](media/CA-Backup-and-Restore-Windows-PowerShell-cmdlets/GTR_ADDS_BackupCARole.gif)  
  
**Table SEQ テーブル \\ @ no__t: 2 アラビア 18:一般的なエラー @ no__t-0  
  
|操作|Error|解説|  
|----------|---------|-----------|  
|**復元-Backup-caroleservice C:\ adcsbackup**|Backup-caroleservice:プロセスは、別のプロセスによって使用されているため、ファイルにアクセスできません。 (HRESULT からの例外:<br /><br />0x80070020|Backup-caroleservice コマンドレットを実行する前に、Active Directory Certificate Services サービスを停止します。|  
|**復元-Backup-caroleservice C:\ adcsbackup**|Backup-caroleservice:ディレクトリが空ではありません。 (HRESULT からの例外: 0x80070091)|-Force パラメーターを使用して、既存のキーを上書きする|  
|**Backup-caroleservice C:\ adcsbackup-Password (Read-Host-Prompt "Password:"-AsSecureString)-DatabaseOnly**|Backup-caroleservice:指定された名前付きパラメーターを使用してパラメーターセットを解決することはできません。|-Password パラメーターは、秘密キーをパスワードで保護するためにのみ使用されます。したがって、バックアップしていない場合は無効になります。|  
|**Backup-caroleservice C:\ adcsback15-Password (読み取りホスト-プロンプト "Password:"-AsSecureString)-DatabaseOnly**|Backup-caroleservice:指定された名前付きパラメーターを使用してパラメーターセットを解決することはできません。|-Password パラメーターは、秘密キーのパスワード保護にのみ使用されます。そのため、パスワードを復元しない場合は無効になります。|  
|**Backup-caroleservice C:\ adcsback14-Password (読み取りホスト-プロンプト "Password:"-AsSecureString)**|Backup-caroleservice:指定されたファイルが見つかりません。 (HRESULT からの例外: 0x80070002|指定されたパスには、有効なデータベースバックアップが含まれていません。  パスが無効であるか、または-KeysOnly オプションを使用してバックアップが実行された可能性があります。|  
  
## <a name="additional-resources"></a>その他のリソース  
[Active Directory 証明書サービス移行ガイド](https://technet.microsoft.com/library/ee126170(v=ws.10).aspx)  
  
[CA データベースおよび秘密キーのバックアップ](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_BackUpDB)  
  
[移行先サーバーでの CA データベースおよび構成の復元](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_RestoreCA)  
  
## <a name="try-this-backup-the-ca-in-your-lab-using-windows-powershell"></a>次のことを試してみてください。Windows PowerShell を使用してラボで CA をバックアップする  
  
1.  このレッスンのコマンドを使用して、パスワードで保護された CA データベースと秘密キーをバックアップします。  
  
2.  現時点では、CA の復元を停止します。  
  


