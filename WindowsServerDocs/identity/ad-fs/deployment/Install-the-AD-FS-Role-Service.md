---
ms.assetid: c28a1b8b-5bec-4eed-8c95-a1a29cfc957c
title: AD FS 役割サービスをインストールする
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 942d34cbfcd988820a54a4f85583ce4b424a415f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855395"
---
# <a name="install-the-ad-fs-role-service"></a>AD FS 役割サービスをインストールする

次の手順を使用して、Windows Server 2012 R2 を実行しているコンピューターに AD FS の役割サービスをインストールし、フェデレーションサーバーファームの最初のフェデレーションサーバー、または既存のフェデレーションサーバーファーム内のフェデレーションサーバーにすることができます。  
  
この手順を実行するには、ローカルコンピューターの**Administrators**、またはそれと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-install-the-ad-fs-server-role-via-the-add-roles-and-features-wizard"></a>役割と機能の追加ウィザードを介して AD FS サーバー ロールをインストールするには  
  
1.  サーバー マネージャーを開きます。 サーバーマネージャーを開くには、**スタート**画面で **サーバーマネージャー** をクリックするか、デスクトップのタスクバーの**サーバーマネージャー**  をクリックします。 **[ダッシュボード]** ページにある **[ようこそ]** タイルの **[クイック スタート]** タブで、 **[役割と機能の追加]** をクリックします。 または、 **[管理]** メニューの **[役割と機能の追加]** をクリックする方法もあります。  
  
2.  **[開始する前に]** ページで、 **[次へ]** をクリックします。  
  
3.  **[インストールの種類の選択]** ページで、[**役割\-ベース] または [機能\-ベースのインストール**] をクリックし、 **[次へ]** をクリックします。  
  
4.  **[宛先サーバーの選択]** ページで、 **[サーバー プールからサーバーを選択]** をクリックし、ターゲット コンピューターが選択されていることを確認してから、 **[次へ]** をクリックします。  
  
5.  **[サーバーの役割の選択]** ページで、 **[Active Directory フェデレーション サービス]** をクリックし、 **[次へ]** をクリックします。  
  
6.  **[機能の選択]** ページで **[次へ]** をクリックします。 必須の前提条件が事前に選択されています。 他の機能を選択する必要はありません。  
  
7.  **Active Directory フェデレーションサービス \(AD FS の\)**  ページで、**次へ** をクリックします。  
  
8.  **[インストール オプションの確認]** ページで情報を確認した後、 **[インストール]** をクリックします。  
  
9. **[インストールの進行状況]** ページで、すべてが正常にインストールされたことを確認し、 **[閉じる]** をクリックします。  
  
### <a name="to-install-the-ad-fs-server-role-via-windows-powershell"></a>Windows PowerShell を介して AD FS サーバー ロールをインストールするには  
  
1.  フェデレーションサーバーとして構成するコンピューターで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します: `Install-windowsfeature adfs-federation –IncludeManagementTools`。  
  
## <a name="see-also"></a>参照 

[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

