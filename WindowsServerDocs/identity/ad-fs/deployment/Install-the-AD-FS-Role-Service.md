---
ms.assetid: c28a1b8b-5bec-4eed-8c95-a1a29cfc957c
title: "AD FS 役割サービスをインストールします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9851134d1ad73092ee44c34c99bc2d873d20ca07
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="install-the-ad-fs-role-service"></a>AD FS 役割サービスをインストールします。

>適用対象: Windows Server 2016、Windows Server 2012 R2

次の手順を使用して、既存のフェデレーション サーバー ファームにフェデレーション サーバー ファームに最初のフェデレーション サーバーが Windows Server 2012 R2 またはフェデレーション サーバーを実行しているコンピューターに AD FS 役割サービスをインストールすることができます。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を実行する最小要件またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-install-the-ad-fs-server-role-via-the-add-roles-and-features-wizard"></a>追加の役割と機能のウィザードを使用して、AD FS サーバーの役割をインストールするには  
  
1.  サーバー マネージャーを開きます。 サーバー マネージャーを開くにはクリックして**サーバー マネージャー**で、**開始**] 画面で、または**サーバー マネージャー**デスクトップ タスク バーのします。 **クイック スタート**のタブ、**ようこそ**タイルで、**ダッシュ ボード**ページで、[**役割と機能の追加**します。 また、クリックすることができます**追加の役割と機能**上、**管理**メニュー。  
  
2.  **開始する前に**] ページで [**次**します。  
  
3.  **インストールの種類の選択**] ページで [**役割ベースまたは機能ベースのインストール**、] をクリックし、**[次へ]**します。  
  
4.  **対象サーバーの選択**] ページで [**サーバー プールからサーバーを選択**、対象のコンピューターが選択されていることを確認] をクリックし、**[次へ]**します。  
  
5.  **サーバーの役割の選択**] ページで [ **Active Directory フェデレーション サービス**、] をクリックし、**[次へ]**します。  
  
6.  **機能の選択**] ページで [**次**します。 必要な前提条件が選択されています。 その他の機能を選択する必要はありません。  
  
7.  **Active Directory フェデレーション サービス \(AD FS\)** ] ページで [**次**します。  
  
8.  情報を確認した後、**インストール オプションの確認**] ページで [**インストール**します。  
  
9. **インストールの進行状況**] ページで、正しくすべてインストールされていることを確認してをクリックして**閉じる**します。  
  
### <a name="to-install-the-ad-fs-server-role-via-windows-powershell"></a>Windows PowerShell を使用して、AD FS サーバーの役割をインストールするには  
  
1.  フェデレーション サーバーとして構成する場合、コンピューター上、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。`Install-windowsfeature adfs-federation –IncludeManagementTools`します。  
  
## <a name="see-also"></a>参照してください。 

[AD FS の展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイドします。](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームを展開します。](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

