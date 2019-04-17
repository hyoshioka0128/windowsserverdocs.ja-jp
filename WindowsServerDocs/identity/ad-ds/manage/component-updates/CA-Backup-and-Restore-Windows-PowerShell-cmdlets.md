---
ms.assetid: 7e195f5b-b194-40f3-a26d-5cf4ade5fc4d
title: "CA のバックアップと復元の Windows PowerShell のコマンドレット"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: aba86ed080cc0b4043805531f0a2138b1b1d3cf8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ca-backup-and-restore-windows-powershell-cmdlets"></a>CA のバックアップと復元の Windows PowerShell のコマンドレット

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012
>
**作成者**: Windows グループに Justin チューナー シニア サポート エスカレーション エンジニア  
  
> [!NOTE]  
> このコンテンツが、Microsoft カスタマー サポート エンジニアによって書き込まれるあり、経験豊富な管理者と TechNet の通常のトピックよりも機能と Windows Server 2012 R2 で解決策の詳細な技術的説明を求めているシステム アーキテクトです。 ただし、実施されていません、同様の編集過程のため、TechNet の「新機能が見つかった通常より洗練されて、言語によってように見える場合があります。  
  
## <a name="overview"></a>概要  
ADCSAdministration Windows PowerShell モジュールは、ウィンドウ Server 2012 で導入されました。  2 つの新しいコマンドレットは、バックアップと CA の復元をサポートするために、ウィンドウ Server 2012 R2 では、このモジュールに追加されました。  
  
-   Backup-CARoleService  
  
-   Restore-CARoleService  
  
## <a name="backup-caroleservice"></a>Backup-CARoleService  
**SEQ テーブル \\\ * ARABIC 17: バックアップし、復元の Windows PowerShell コマンドレット**  
  
**ADCSAdministration コマンドレット: Backup-CARoleService**  
  
|引数 -**太字**引数は必須|説明|  
|------------------------------------------------|---------------|  
|**パス**|文字列のバックアップを保存する場所<br />-このされている唯一の無名のパラメーター<br />-位置指定パラメーター<br /><br />**例:**<br /><br />Backup-CARoleService-パス c:\adcsbackup1。<br /><br />Backup-CARoleService c:\adcsbackup2|  
|-KeyOnly|-データベースがない場合、CA 証明書をバックアップします。<br /><br />**例:**<br /><br />Backup-CARoleService c:\adcsbackup3 - KeyOnly|  
|パスワード|-CA 証明書と秘密キーを保護するためのパスワードを指定します。<br />-セキュリティで保護された文字列をある必要があります。<br />-無効と - DatabaseOnly パラメーター<br /><br />例:<br /><br />Backup-CARoleService c:\adcsbackup4-パスワード (Read-Host-プロンプト"パスワード:"- AsSecureString)<br /><br />Backup-CARoleService c:\adcsbackup5-パスワード (ConvertTo-SecureString"Pa55w0rd!" -AsPlainText - Force)|  
|-DatabaseOnly|-CA 証明書がないデータベースをバックアップします。<br /><br />Backup-CARoleService c:\adcsbackup6 - DatabaseOnly|  
|フォース|1 を使用すると指定した場所に preexists バックアップを上書きするには、Path パラメーターで。<br /><br />Backup-CARoleService c:\adcsbackup1-Force|  
|-増分|-増分バックアップを実行します。<br /><br />Backup-CARoleService c:\adcsbackup7-増分|  
|-KeepLog|1。 コマンドは、ログ ファイルを保持するように指示します。 既定では除く増分のシナリオでは、ログ ファイルが切り捨てられて、スイッチが指定されていない場合<br /><br />Backup-CARoleService c:\adcsbackup7 - KeepLog|  
  
### <a name="-password-secure-string"></a>パスワード<Secure String>  
場合は、パスワードのパラメーターが使用される、指定されたパスワードはセキュリティで保護された文字列である必要があります。  使用して、 **Read-host**コマンドレットをセキュリティで保護されたパスワードの入力の対話的なプロンプトを起動する、またはを使用して、 **Convertto-securestring** - 行でパスワードを指定するコマンドレットです。  
  
次の例を確認します。  
  
**Read-Host を使用して、パスワードのパラメーターのセキュリティで保護された文字列を指定します。**  
  
```powershell  
Backup-CARoleService c:\adcsbackup4 -Password (Read-Host -prompt "Password:" -AsSecureString)  
```  
  
**セキュリティで保護された文字列を ConvertTo-SecureString を使用して、パスワードのパラメーターを指定します。**  
  
```powershell  
Backup-CARoleService c:\adcsbackup5 -Password (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText -Force)  
```  
  
## <a name="restore-caroleservice"></a>Restore-CARoleService  
**ADCSAdministration コマンドレット: Restore-CARoleService**  
  
|引数 -**太字**引数は必須|説明|  
|------------------------------------------------|---------------|  
|**パス**|文字列の場所からのバックアップを復元するには<br />-このされている唯一の無名のパラメーター<br />-位置指定パラメーター<br /><br />**例:**<br /><br />Restore-CARoleService - パス c:\adcsbackup1 - Force。<br /><br />Restore-CARoleService c:\adcsbackup2-Force|  
|-KeyOnly|-データベースがない場合、CA 証明書を復元します。<br />の-KeyOnly オプションを使用して、バックアップが取得されたかどうかは指定必要があります。<br /><br />**例:**<br /><br />Restore-CARoleService c:\adcsbackup3 - KeyOnly-Force|  
|パスワード|-CA 証明書と秘密キーのパスワードを指定します。<br />-セキュリティで保護された文字列をある必要があります。<br /><br />**例:**<br /><br />Restore-CARoleService c:\adcsbackup4-パスワード (ホスト-読み取り - プロンプト"パスワード:"- AsSecureString)-Force<br /><br />Restore-CARoleService c:\adcsbackup5-パスワード (ConvertTo-SecureString"Pa55w0rd!" -AsPlainText - Force)-Force|  
|-DatabaseOnly|-CA 証明書がない、データベースを復元します。<br /><br />Restore-CARoleService c:\adcsbackup6 - DatabaseOnly|  
|フォース|-を使用すると、既存のキーを上書きするには<br />-は、省略可能なパラメーターが、インプレースを復元するには、必要な可能性があります。<br /><br />Restore-CARoleService c:\adcsbackup1-Force|  
  
### <a name="issues"></a>問題  
Backup-CARoleService の使用中に ConvertTo-SecureString 関数が失敗した場合、非パスワード保護されているバックアップが実行されたパスワード パラメーターを使用します。  
  
![CA のバックアップと復元](media/CA-Backup-and-Restore-Windows-PowerShell-cmdlets/GTR_ADDS_BackupCARole.gif)  
  
**SEQ テーブル \\\ * ARABIC 18: 一般的なエラー**  
  
|アクション|エラー|コメント|  
|----------|---------|-----------|  
|**Restore-CARoleServiceC:\ADCSBackup**|Restore-CARoleService: プロセスは、ファイルにアクセスできません。 (HRESULT からの例外。<br /><br />0x80070020)|Restore-CARoleService コマンドレットを実行する前に Active Directory Certificate Services サービスを停止します。|  
|**Restore-CARoleServiceC:\ADCSBackup**|Restore-CARoleService: ディレクトリは空ではありません。 (HRESULT からの例外: 0x80070091)|使用する既存のキーを上書きするには、Force パラメーター|  
|**Backup-CARoleServiceC:\ADCSBackup-パスワード (Read-Host-プロンプト"パスワード:"- AsSecureString) - DatabaseOnly**|Backup-CARoleService: 指定された名前付きパラメーターを使用して、パラメーター セットを解決することはできません。|パスワード パラメーターは、秘密キーを保護し、無効なためをバックアップするしていない場合にのみにパスワードを使用|  
|**Restore-CARoleServiceC:\ADCSBack15-パスワード (Read-Host-プロンプト"パスワード:"- AsSecureString) - DatabaseOnly**|Restore-CARoleService: 指定された名前付きパラメーターを使用して、パラメーター セットを解決することはできません。|パスワード パラメーターは、秘密キーを保護し、無効なためしないファイルを復元するときにのみにパスワードを使用|  
|**Restore-CARoleServiceC:\ADCSBack14-パスワード (Read-Host-プロンプト"パスワード:"- AsSecureString)**|Restore-CARoleService: システムは、指定されたファイルを見つけることができません。 (HRESULT からの例外: 0x80070002)|指定されたパスでは、有効なデータベースのバックアップは含まれません。  おそらく、パスが正しくないか、-KeysOnly オプションを使用して、バックアップが取得されたか。|  
  
## <a name="additional-resources"></a>その他のリソース  
[Active Directory 証明書サービス移行ガイド](https://technet.microsoft.com/library/ee126170(v=ws.10).aspx)  
  
[CA データベースと秘密キーをバックアップします。](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_BackUpDB)  
  
[CA データベースと、移行先サーバー上の構成を復元します。](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_RestoreCA)  
  
## <a name="try-this-backup-the-ca-in-your-lab-using-windows-powershell"></a>Windows PowerShell を使用して、ラボ内の CA をバックアップしてください。  
  
1.  この演習のレッスンのコマンドを使用して、CA データベースと秘密キーのパスワードで保護されたバックアップを作成します。  
  
2.  この時点で、CA の復元は保留されます。  
  


