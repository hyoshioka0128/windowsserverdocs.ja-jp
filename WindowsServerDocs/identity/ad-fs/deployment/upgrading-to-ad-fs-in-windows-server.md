---
ms.assetid: 7671e0c9-faf0-40de-808a-62f54645f891
title: Windows Server 2016 での AD FS へのアップグレード
description: ''
author: billmath
manager: femila
ms.date: 04/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c8e72f1075b984506f9f992cd45cf853b50bddeb
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191920"
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-using-a-wid-database"></a>WID データベースを使用した、Windows Server 2016 での AD FS へのアップグレード



## <a name="upgrading-a-windows-server-2012-r2-or-2016-ad-fs-farm-to-windows-server-2019"></a>Windows Server 2019 に、Windows Server 2012 R2 または 2016年の AD FS ファームをアップグレードします。
次のドキュメントは、WID データベースを使用しているときに、Windows Server 2019 の AD FS を AD FS ファームをアップグレードする方法について説明します。  

### <a name="ad-fs-farm-behavior-levels-fbl"></a>AD FS ファーム動作レベル (FBL)  
Windows Server 2016 の AD FS ファーム動作レベル (FBL) が導入されました。 これは、ファーム全体の設定、機能、AD FS ファームで使用できるかを決定します。

次の表は、Windows Server のバージョンで FBL 値を示します。
| Windows Server のバージョン  | FBL | AD FS 構成データベース名 |
| ------------- | ------------- | ------------- |
| 2012 R2  | 1  | AdfsConfiguration |
| 2016  | 3  | AdfsConfigurationV3 |
| 2019  | 4  | AdfsConfigurationV4 |

> [!NOTE]  
> 新しい AD FS 構成データベースを作成、FBL をアップグレードします。  各バージョンの Windows Server AD FS と FBL 値用の構成データベースの名前は、上の表を参照してください。

### <a name="new-vs-upgraded-farms"></a>新しい vs ファームのアップグレード
既定では、新しい AD FS ファームで FBL はインストールされている最初のファーム ノードの Windows Server のバージョンの値と一致します。  

以降のバージョンの AD FS サーバーは、AD FS 2012 R2 または 2016 ファームに参加させるし、ファームは、既存のノードとして同じ FBL で動作します。 FBL 値、最小バージョンの同じファームで動作している Windows Server のバージョンが複数ある場合は、ファームは「混在」と言います。 ただし、FBL が発生するまで、以降のバージョンの機能を利用することはできません。 混合ファーム。  

-   管理者は、既存の Windows Server 2012 R2 または 2016年ファームに新しい Windows Server 2019 フェデレーション サーバーを追加できます。 結果として、ファームでは、「混合モード」では、し、元のファームと同じファーム動作レベルで動作します。 ファーム全体で一貫した動作を確認するには、新しい Windows Server AD FS のバージョンの機能を構成または使用することはできません。  

- FBL が発生する前に、管理者は、ファームから Windows Server の以前のバージョンの AD FS ノードを削除する必要があります。  WID ファームの場合はこれが必要である新しい Windows Server 2019 フェデレーション サーバー tp のいずれかに注意してください、ファーム内のプライマリ ノードの役割に昇格します。

-   ファーム内のすべてのフェデレーション サーバーは、Windows Server のバージョンが同じでは後、FBL を発生させることができます。  結果として、新しい AD FS Windows Server 2019 機能するように構成し、使用します。

ファームが混在モードで AD FS ファームがいないできる新機能、または Windows Server 2019 で AD FS で導入された機能を認識します。 これは、新しい機能を試す必要があることはできません、FBL が発生するまでことを意味します。 その場合は、組織が、FBL rasing する前に新しい機能をテストしようとして、これを行う別のファームをデプロイする必要があります。  

残りの部分は、Windows Server 2016 または 2012 R2 環境に Windows Server 2019 のフェデレーション サーバーを追加し、Windows Server 2019 に FBL を上げる方法の手順を説明します。 これらの手順は、次のアーキテクチャの図で概説されているテスト環境で実行されました。  

> [!NOTE]  
> AD FS Windows Server 2019 FBL を移動するには、Windows Server 2016 のすべてまたは 2012 R2 ノードを削除する必要があります。 Windows Server 2019 に、Windows Server 2016 または 2012 R2 の OS をアップグレードおよび 2019年ノードになることがあるだけできません。 解除して、新しい 2019年ノードに置き換える必要があります。



##### <a name="to-upgrade-your-ad-fs-farm-to-windows-server-2019-farm-behavior-level"></a>Windows Server 2019 ファーム動作レベルに、AD FS ファームをアップグレードするには  

1.  Windows Server の 2019 に Active Directory フェデレーション サービスの役割をインストールするサーバー マネージャーを使用して、

2.  AD FS 構成ウィザードを使用して、、既存の AD FS ファームを新しい Windows Server 2019 サーバーを参加させます。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_1.png)  

3.  Windows Server 2019 のフェデレーション サーバーで AD FS の管理を開きます。 このフェデレーション サーバーがプライマリ サーバーではないためには、管理機能が使用できないことに注意してください。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_3.png)  

4.  Windows Server 2019 サーバーでは、管理者特権の PowerShell コマンド ウィンドウを開き、次のコマンドレットを実行しています。 `Set-AdfsSyncProperties -Role PrimaryComputer`

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_4.png)  

5.  以前にプライマリとして構成された、AD FS サーバーでは、管理者特権の PowerShell コマンド ウィンドウを開き、次のコマンドレットを実行しています。 `Set-AdfsSyncProperties -Role SecondaryComputer -PrimaryComputerName {FQDN} `

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_5.png)  

6.  これで、Windows Server 2016 のフェデレーション サーバーでは、AD FS 管理を開きます。 プライマリ ロールがこのサーバーに転送されているため、すべての管理機能に表示されますに注意してください。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_6.png)  

7.  ファームのアップグレードがある AD スキーマを必要と 2016 または 2019 を 2012 R2 AD FS ファームをアップグレードする場合に少なくとも 85 をレベルします。  スキーマ名、Windows Server 2016 のインストール メディアをアップグレードするには、コマンド プロンプトを開き、support\adprep ディレクトリに移動します。 次を実行します。  `adprep /forestprep`

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_7.png)  

    実行が完了します。 `adprep/domainprep`
    >[!NOTE]
    >次の手順を実行する前に、設定から Windows Update を実行して、Windows Server が現在確認してください。 更新の必要がなくなるまで、このプロセスを続けます。
    >

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_8.png)  

8. Windows Server 2016 で PowerShell を開き、次のコマンドレットを実行します。
    >[!NOTE]
    > 2012 R2 のすべてのサーバーは、次の手順を実行する前に、ファームから削除する必要があります。

    `Invoke-AdfsFarmBehaviorLevelRaise`  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_9.png)  

9. 入力を求められたら、Y を入力します。これにより、レベルを上げることが開始されます。 これが完了すると、FBL 正常が発生します。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_10.png)  

10. これで、AD FS の管理に移動すると表示されます以降の AD FS のバージョンの新機能が追加されました

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_12.png)  

11. 同様に、PowerShell コマンドレットを使用することができます:`Get-AdfsFarmInformation`現在 FBL を表示します。  

    ![アップグレード](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_13.png)  

12. WAP サーバーを各 Web アプリケーション プロキシを最新のレベルにアップグレードするには、管理者特権でのウィンドウで、次の PowerShell コマンドを実行して、WAP を再構成します。  
    ```powershell
    $trustcred = Get-Credential -Message "Enter Domain Administrator credentials"
    Install-WebApplicationProxy -CertificateThumbprint {SSLCert} -fsname fsname -FederationServiceTrustCredential $trustcred  
    ```
    クラスターから以前のサーバーを削除して、のみ WAP 最新のサーバー バージョンを実行しているサーバー上で、次の Powershell コマンドレットを実行して再構成されたを保持します。
    ```powershell
    Set-WebApplicationProxyConfiguration -ConnectedServersName WAPServerName1, WAPServerName2
    ```
    Get WebApplicationProxyConfiguration commmandlet を実行して、WAP の構成を確認します。 ConnectedServersName 前のコマンドからを実行するサーバーが反映されます。
    ```powershell
    Get-WebApplicationProxyConfiguration
    ```
    WAP サーバーの ConfigurationVersion をアップグレードするには、次の Powershell コマンドを実行します。
    ```powershell
    Set-WebApplicationProxyConfiguration -UpgradeConfigurationVersion
    ```
    WAP サーバーのアップグレードを完了します。
