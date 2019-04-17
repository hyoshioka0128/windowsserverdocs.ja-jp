---
ms.assetid: 7671e0c9-faf0-40de-808a-62f54645f891
title: "Windows Server 2016 の AD FS へのアップグレード"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ce07398a2d624a1e9b004cd35eb9228d59dc2b5b
ms.sourcegitcommit: 76e57a5453d6ee9a04dcff6a8cca087132cb1d5f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2018
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-using-a-wid-database"></a>WID データベースを使用して Windows Server 2016 での AD FS へのアップグレード

>Windows Server 2016 の適用対象:


## <a name="moving-from-a-windows-server-2012-r2-ad-fs-farm-to-a-windows-server-2016-ad-fs-farm"></a>Windows Server 2012 R2 AD FS ファームから Windows Server 2016 の AD FS ファームへの移行  
次のドキュメントでは、WID データベースを使用しているときに、Windows Server 2016 での AD FS に、AD FS Windows Server 2012 R2 ファームをアップグレードする方法を示します。  

### <a name="upgrading-ad-fs-to-windows-server-2016-fbl"></a>AD FS を Windows Server 2016 FBL にアップグレードします。  
Windows Server 2016 の AD FS では、ファームの動作レベルの機能 (FBL) です。   この機能は、ファーム全体で AD FS ファームを使用できる機能を決定します。   既定では、Windows Server 2012 R2 AD FS ファームで FBL は Windows Server 2012 R2 FBL します。  

Windows Server 2012 R2 のファームに追加できる Windows Server 2016 の AD FS サーバーと Windows Server 2012 R2 として同じ FBL で動作します。  この方法で動作している Windows Server 2016 の AD FS サーバーがある場合は、ファームを「混在させること」と言います。  ただし、しないことができます、FBL が Windows Server 2016 に発生するまでの Windows Server 2016 の新機能を利用します。  混在ファームの場合。  

-   管理者は、新しい、既存の Windows Server 2012 R2 ファームにフェデレーション サーバーを Windows Server 2016 で追加できます。  その結果、ファーム「混在モード」では、Windows Server 2012 R2 ファームレベルの動作の動作します。  ファーム全体で一貫した動作を確認するには、Windows Server 2016 の新機能を構成またはこのモードで使用することはできません。  

-   すべての Windows Server 2012 R2 フェデレーション サーバーは、混在モード ファームから削除されているし、WID ファームの場合、新しい Windows Server 2016 のフェデレーション サーバーのいずれかに昇格されているプライマリ ノードの役割、管理者は、Windows Server 2012 R2 から Windows Server 2016 への FBL を増やすことができます。  その結果、新しい AD FS Windows Server 2016 機能し、構成して使用できます。  

-   その結果の混在ファームの機能、AD FS Windows Server 2012 R2 の Windows Server 2016 にアップグレードすると考えている組織は、まったく新しいファームを展開する必要はありません、エクスポートし、構成データをインポートします。  代わりに、それがオンライン中に、既存のファームに Windows Server 2016 のノードを追加できのみ FBL 上げるに関連する比較的短いダウンタイムが発生することができます。  

ファームが混在モードで、AD FS ファームがないことの新機能または Windows Server 2016 での AD FS で導入された機能対応に注意してください。  これは、新機能を試したい組織これができない、FBL が発生するまでことを意味します。  その場合は、組織が、FBL rasing する前に新しい機能をテストしようとして、これを行うに個別のファームを展開する必要があります。  

残りの部分は、ドキュメントが Windows Server 2012 R2 環境に Windows Server 2016 のフェデレーション サーバーを追加して、Windows Server 2016 に FBL を発生させるための手順を提供します。  次の手順は、次のアーキテクチャの図で説明されているテスト環境で実行されました。  

> [!NOTE]  
> Windows Server 2016 FBL AD FS に移動するにはすべての Windows 2012 R2 ノードを削除する必要があります。  Windows Server 2016 への Windows Server 2012 R2 の OS のアップグレードし、2016年ノードになることがあるだけできません。  それを削除 2016年の新しいノードを置き換える必要があります。
>
> 新しい管理データベース"AdfsConfigurationV3"を作成するには、SQL を使用して AD FS の構成を保存するときに、FBL をアップグレードします。

##### <a name="to-upgrade-your-ad-fs-farm-to-windows-server-2016-farm-behavior-level"></a>AD FS ファームを Windows Server 2016 ファーム動作レベルにアップグレードするには  

1.  Windows Server 2016 でサーバー マネージャーのインストール、Active Directory フェデレーション サービスの役割を使用してください。  

2.  AD FS 構成ウィザードを使用して、、既存の AD FS ファームを新しい Windows Server 2016 サーバーを参加させます。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_1.png)  

3.  Windows Server 2016 のフェデレーション サーバーでは、AD FS 管理を開きます。    ある何も表示されているこのフェデレーション サーバーは、プライマリ サーバーではないために注意してください。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_3.png)  

4.  PowerShell を開きへの参加準備が完了すると、Windows Server 2016 サーバーで、次のコマンドレットを実行しますセット AdfsSyncProperties-役割 PrimaryComputer。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_4.png)  

5.  元の AD FS Windows Server 2012 R2 サーバーで PowerShell を開き、次のコマンドレットを実行しますセット AdfsSyncProperties-役割 SecondaryComputer PrimaryComputerName {FQDN}。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_5.png)  

6.  Web アプリケーション プロキシ PowerShell を開き、次のコマンドレットを実行します Install-webapplicationproxy CertificateThumbprint {SSLCert} - fsname fsname TrustCred $trustcred。  

7.  今すぐ Windows Server 2016 のフェデレーション サーバーでは、AD FS 管理を開きます。  プライマリの役割がこのサーバーに転送されたためのすべてのノードが表示されることを確認します。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_6.png)  

8.  Windows Server 2016 のインストール メディア、コマンド プロンプトを開くし、support\adprep ディレクトリに移動します。  次のコマンド実行: adprep/forestprep します。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_7.png)  

9. Adprep/domainprep の実行が完了するとします。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_8.png)  

10. 今すぐ Windows Server 2016 サーバーで PowerShell を開き、次のコマンドレットを実行します呼び出す AdfsFarmBehaviorLevelRaise。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_9.png)  

11. 表示されたら、Y」と入力します。これにより、レベルを上げることが開始されます。  これが完了すると、FBL 正常が生成されます。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_10.png)  

> [!NOTE]  
> 場合は、AD FS サーバーでは、SQL を使用して、構成、新しい manamgement データベースが作成されました"AdfsConfiguraionV3"という名前のします。 

12. これで、AD FS の管理に移動した場合は、Windows Server 2016 の AD FS で追加された新しいノードが表示されます。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_12.png)  

13. 同様に、PowerShell コマンドレットを使用することができます。 現在 FBL を表示するには、Get-AdfsFarmInformation します。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_13.png)  
