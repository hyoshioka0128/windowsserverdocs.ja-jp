---
ms.assetid: c28a1b8b-5bec-4eed-8c95-a1a29cfc957c
title: AD FS 役割サービスをインストールする
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ffa9b20d4d7b5c84b0e29ac446b8aa6f3a932850
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192111"
---
# <a name="install-the-ad-fs-role-service"></a>AD FS 役割サービスをインストールする

次の手順を使用すると、Windows Server 2012 R2 フェデレーション サーバー ファーム内の最初のフェデレーション サーバーまたはフェデレーション サーバーを既存のフェデレーション サーバー ファームで実行されているコンピューターで AD FS 役割サービスをインストールします。  
  
メンバーシップ**管理者**、またはこの手順を実行する最小要件は、ローカル コンピューターのそれと同等です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-install-the-ad-fs-server-role-via-the-add-roles-and-features-wizard"></a>役割と機能の追加ウィザードを使用して、AD FS サーバーの役割をインストールするには  
  
1.  サーバー マネージャーを開きます。 サーバー マネージャーを開くには、次のようにクリックします。**サーバー マネージャー**で、**開始** 画面で、または**サーバー マネージャー**デスクトップ タスク バーにします。 **[ダッシュボード]** ページにある **[ようこそ]** タイルの **[クイック スタート]** タブで、 **[役割と機能の追加]** をクリックします。 または、 **[管理]** メニューの **[役割と機能の追加]** をクリックすることもできます。  
  
2.  **[開始する前に]** ページで、 **[次へ]** をクリックします。  
  
3.  **インストールの種類を選択します**] ページで [**ロール\-ベースまたは機能\-ベースのインストール**、順にクリックします**次**。  
  
4.  **[対象サーバーの選択]** ページで、 **[サーバー プールからサーバーを選択]** をクリックし、ターゲット コンピューターが選択されていることを確認してから、 **[次へ]** をクリックします。  
  
5.  **[サーバーの役割の選択]** ページで、 **[Active Directory フェデレーション サービス]** をクリックし、 **[次へ]** をクリックします。  
  
6.  **[機能の選択]** ページで **[次へ]** をクリックします。 必要な前提条件が選択されています。 その他の機能を選択する必要はありません。  
  
7.  **Active Directory フェデレーション サービス\(AD FS\)**  ] ページで [**次**します。  
  
8.  情報を確認した後、**インストール オプションの確認**] ページで [**インストール**します。  
  
9. **[インストールの進行状況]** ページで、すべてが正常にインストールされたことを確認し、 **[閉じる]** をクリックします。  
  
### <a name="to-install-the-ad-fs-server-role-via-windows-powershell"></a>Windows PowerShell を使用して、AD FS サーバーの役割をインストールするには  
  
1.  をフェデレーション サーバーとして構成するコンピューターに Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します:`Install-windowsfeature adfs-federation –IncludeManagementTools`します。  
  
## <a name="see-also"></a>関連項目 

[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイドします。](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

