---
title: SQL Server と Windows Server 2016 の AD FS へのアップグレード
description: ''
author: billmath
manager: mtillman
ms.date: 04/11/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 70f279bf-aea1-4f4f-9ab3-e9157233e267
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 59b761e69da5b1c1e27fea71b32447b19d2b83c6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812083"
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-with-sql-server"></a>SQL Server と Windows Server 2016 の AD FS へのアップグレード

>適用先:Windows Server 2016


## <a name="moving-from-a-windows-server-2012-r2-ad-fs-farm-to-a-windows-server-2016-ad-fs-farm"></a>Windows Server 2012 R2 AD FS ファームから Windows Server 2016 の AD FS ファームへの移行  
次のドキュメントは、AD FS データベースの SQL Server を使用しているときに、Windows Server 2016 での AD FS を AD FS Windows Server 2012 R2 ファームをアップグレードする方法について説明します。  

### <a name="upgrading-ad-fs-to-windows-server-2016-fbl"></a>AD FS を Windows Server 2016 FBL にアップグレードします。  
Windows Server 2016 の AD FS ではファーム動作レベル機能 (FBL) です。   この機能は、ファーム全体に適用し、AD FS ファームを使用する機能を決定します。   既定では、Windows Server 2012 R2 AD FS ファームで FBL は Windows Server 2012 R2 FBL します。  

Windows Server 2016 の AD FS サーバーは、Windows Server 2012 R2 ファームに追加でき、Windows Server 2012 R2 と同じ FBL で動作します。  このような方法で動作している Windows Server 2016 の AD FS サーバーがある場合は、ファームは「混在」と言います。  ただし、FBL は、Windows Server 2016 に発生するまで、Windows Server 2016 の新機能の利用することはできません。  混合ファーム。  

-   管理者は、新規、既存の Windows Server 2012 R2 ファームにフェデレーション サーバーを Windows Server 2016 で追加できます。  その結果、ファームでは、「混合モード」では、し、Windows Server 2012 R2 ファーム動作レベルに動作します。  ファーム全体で一貫した動作を確認するには、Windows Server 2016 の新機能を構成またはこのモードで使用することはできません。  

-   管理者が、Win から FBL を上げることができますし、混在モード ファームから削除されたすべての Windows Server 2012 R2 フェデレーション サーバーと、WID ファームの場合、新しい Windows Serve 2016 フェデレーション サーバーのいずれかが昇格されたプライマリ ノードの役割に、dows Server 2012 R2 を Windows Server 2016。  結果として、新しい AD FS Windows Server 2016 の機能するように構成し、使用します。  

-   結果として、AD FS Windows Server 2012 R2 の Windows Server 2016 にアップグレードする予定している組織が、まったく新しいファームをデプロイする必要はありません、混合ファーム機能のエクスポートし、構成データをインポートします。  代わりに、オンラインになっているときに、既存のファームに Windows Server 2016 ノードを追加できのみ FBL raise に関連する比較的簡単なダウンタイムが発生することができます。  

ファームが混在モードで AD FS ファームがいないできる新機能、または Windows Server 2016 での AD FS で導入された機能を認識します。  これは、新しい機能を試す必要があることはできません、FBL が発生するまでことを意味します。  その場合は、組織が、FBL rasing する前に新しい機能をテストしようとして、これを行う別のファームをデプロイする必要があります。  

残りの部分、ドキュメントでは、Windows Server 2012 R2 環境に Windows Server 2016 のフェデレーション サーバーを追加して、Windows Server 2016 に FBL を上げる方法の手順です。  これらの手順は、次のアーキテクチャの図で概説されているテスト環境で実行されました。  

> [!NOTE]  
> AD FS を Windows Server 2016 FBL を移動するには、すべての Windows 2012 R2 ノードを削除する必要があります。  Windows Server 2012 R2 の OS を Windows Server 2016 にアップグレードし、2016年のノードになることがあることはできませんだけです。  解除して、新しい 2016年ノードを置き換える必要があります。  

次のアーキテクチャ図を検証し、次の手順を記録するために使用されたセットアップを示しています。

![Architecture](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/arch.png) 


#### <a name="join-the-windows-2016-ad-fs-server-to-the-ad-fs-farm"></a>Windows 2016 の AD FS サーバーを AD FS ファームに参加させる

1.  Windows Server 2016 を Server Manager のインストール、Active Directory フェデレーション サービスの役割を使用してください。  

2.  AD FS 構成ウィザードを使用して、、既存の AD FS ファームを新しい Windows Server 2016 サーバーを参加させます。  **ようこそ**画面をクリック**次**します。
 ![ファームへの追加します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure1.png)  
3.  **Active Directory Domain Services に接続する** 画面で、s**管理者アカウントの指定、お**フェデレーション サービスの構成を実行し、をクリックしてアクセス許可を持つ**次へ**.
4.  **Specify Farm**画面で、SQL server とインスタンスの名前を入力してクリックして **[次へ]** します。
![ファームへの追加します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure3.png)
5.  **SSL 証明書の指定**画面で、証明書を指定してをクリックして**次**します。
![ファームへの追加します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure4.png)
6.  **サービス アカウントの指定**画面で、サービス アカウントを指定してをクリックして**次**します。 
7.  **オプションの確認**画面で、オプションをクリックします**次**します。 
8.  **の前提条件チェック**画面で、前提条件チェックのすべてが成功し、をクリックすることを確認、**構成**。
9.  **結果**画面で、そのサーバーが正常に構成されていることを確認してクリックして**閉じる**します。
 
   
#### <a name="remove-the-windows-server-2012-r2-ad-fs-server"></a>Windows Server 2012 R2 AD FS サーバーを削除します。

>[!NOTE]
>セット AdfsSyncProperties を使用して、プライマリ AD FS サーバーを設定する必要はありません-ロール、データベースとして SQL を使用する場合。  これは、この構成ではプライマリのすべてのノードと見なされるためにです。

1.  サーバー マネージャーの使用中の Windows Server 2012 R2 AD FS サーバーで**役割の削除と機能**  **管理**します。 
![サーバーを削除します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove1.png)
2.  **[開始する前に]** 画面で、**[次へ]** をクリックします。
3.  **サーバーの選択** 画面で、をクリックして**次**。
4.  **サーバーの役割**画面で、横にチェック ボックスをオフ**Active Directory フェデレーション サービス** をクリック**次**します。
![サーバーを削除します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove2.png)
5.  **機能** 画面で、をクリックして**次**します。
6.  **確認** 画面で、をクリックして**削除**します。
7.  これが完了すると、サーバーを再起動します。
     
#### <a name="raise-the-farm-behavior-level-fbl"></a>(FBL) ファーム動作レベルを上げる
この手順の前に、forestprep および domainprep が Active Directory 環境で実行されていることと、Active Directory は、Windows Server 2016 のスキーマであることを確認する必要があります。  このドキュメントでは、Windows 2016 のドメイン コント ローラーの使用を開始し、AD をインストールしたときに実行されたため、これらを実行する必要ありませんでした。

>[!NOTE]
>以下のプロセスを開始する前に、設定を Windows Update を実行して、Windows Server 2016 は現在を確認します。  更新の必要がなくなるまで、このプロセスを続けます。 

1. Windows Server 2016 サーバーのようになりましたで PowerShell を開き、次を実行して: **$cred = Get-credential**し、enter キーを押します。
2. SQL Server で管理者特権のある資格情報を入力します。
3. これで PowerShell では、次のように入力します。**Invoke-AdfsFarmBehaviorLevelRaise -Credential $cred**
2. 入力を求められたら入力**Y**します。これにより、レベルを上げることが開始されます。  これが完了すると、FBL 正常が発生します。  
![更新プログラムを終了します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish1.png)
3. ここで、AD FS の管理に移動する場合は、Windows Server 2016 の AD FS で追加された新しいノードが表示されます。  
4. 同様に、PowerShell コマンドレットを使用することができます。Get AdfsFarmInformation 現在 FBL を表示します。  
![更新プログラムを終了します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish2.png)
