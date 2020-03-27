---
title: Windows Server Essentials での SharePoint Online の管理
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 282f3634-6de6-4691-803c-df6c3c16660d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 92552d3beff58edfffe119d1490fefd646479775
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311082"
---
# <a name="manage-sharepoint-online-in-windows-server-essentials"></a>Windows Server Essentials での SharePoint Online の管理

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Office 365 を Windows Server Essentials サーバーと統合している場合は、Office 365 にサインインしなくても、ダッシュボードから SharePoint Online ライブラリとチームサイトを管理できます。 Office 365 のビジネスプランを使用して、SharePoint Online ライブラリとチームサイトを取得します。 [Office 365 とサーバーを統合する方法を確認します。](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
 おまけとして、ユーザーは My Server 2012 R2 アプリを使用して、モバイルデバイスまたは Windows phone を使用して、任意の場所から SharePoint Online ライブラリ内のファイルにアクセスできるようになります。 [My Server アプリはどこで入手できますか。](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)  
  
 SharePoint を試してみましたか。 [今すぐ実行できる操作](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/get-started-with-sharepoint-2013-HA102772778.aspx)  
  
## <a name="where-on-the-dashboard-will-i-manage-my-libraries-and-team-sites"></a>ダッシュボードのどこでマイ ライブラリとチーム サイトを管理しますか  
 新しい **[Sharepoint online]** タブを使用します。これは、Office 365 をサーバーと統合して sharepoint online のリソースを管理するときに、ダッシュボードの**ストレージ**領域に追加されます。  

  
## <a name="what-can-i-manage-from-the-dashboard"></a>ダッシュボードで何を管理できますか。  
  
### <a name="manage-your-online-libraries"></a>オンライン ライブラリの管理  
   
|-|-|  
|ライブラリを追加する | **[SharePoint ライブラリ]** タブで、 **[ライブラリの追加]** を使用します。 通常の選択肢をすべて選択可能です。<br /><br /> -チームサイトとライブラリの種類を選択します。<br />-バージョン管理を使用するかどうかを決定します。<br />-アクセス許可を割り当てます。<br /><br /> **ヒント:** アクセス許可を割り当てない場合にライブラリが継承するチームサイトのアクセス許可を確認するには、「**サイトのアクセス許可を表示**する」を参照してください。  
|ライブラリを開く |ライブラリの内容を操作するには、Office 365 でライブラリを開く必要があります。 ライブラリを選択して **[ライブラリを開く]** をクリックします。 コンテンツでできることは、SharePoint Online へのサインインに使用する資格情報によって異なります |。  
|バージョン管理またはアクセス許可の変更 |[ライブラリの**プロパティの表示**] を使用すると、ライブラリのバージョン管理またはアクセス許可を表示または変更できます |。  
|ライブラリを削除する |**警告:** SharePoint Online ライブラリを削除する前に、残しておく必要のあるファイルを別の場所に保存してください。 SharePoint からライブラリを削除すると、すべてが完全に削除されます。 復旧する方法はありません。<br /><br /> 後で必要になるものがライブラリに格納されていないことを確認したら、ライブラリを選択し、 **[ライブラリの削除]** をクリックします。 |  
  
### <a name="manage-your-team-sites"></a>チームのサイトの管理  
 
|-|-|  
|SharePoint チームサイトの管理 | **[チームサイトの管理]** アクションを使用すると、Office 365 にサインインし、SharePoint Online チームサイトを管理できます。 Office 365 でできることは、サインインに使用するオンラインアカウントによって決まります。<br /><br /> Office 365 を閉じて、ダッシュボードに戻ったら、[**最新**の状態に更新] をクリックして変更を表示します。 |チームサイトのアクセス許可を表示または変更する |既定では、ライブラリはチームサイトからアクセス許可を継承するため、チームサイトに簡単にアクセスできるようにすると便利です。 チームサイトのアクセス許可を表示または変更するには、チームサイトまたはそのいずれかのライブラリを選択し、 **[サイトのアクセス許可の表示]** をクリックします。<br /><br /> **ヒント:** SharePoint チームサイトのアクセス許可の詳細については、ヘルプを参照してください。 チーム サイトのアクセス許可については、便利な [ [詳細](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/introduction-control-user-access-with-permissions-HA102771919.aspx?CTT=5&origin=HA102771924) ] リンクがあります。  
  
## <a name="tips"></a>ヒント  
  
-   **Office 365 ポータルで行われた最新の変更を表示するには、[最新の状態に更新] をクリックします。** SharePoint Online を管理するには、Office 365 を開いた後で表示を更新する必要があります。 ダッシュボードを長時間、開いたままにしておく場合は、 **[更新]** をクリックして、必ず最新の変更内容を表示します。  
  
-   **SharePoint Online でできることは、ダッシュボードと Office 365 のどちらで作業しているかによって異なります。** ダッシュボードでは、Office 365 統合の管理者アカウントを使用して SharePoint Online の変更が行われます。 ただし、ダッシュボードから Office 365 にサインインすると、使用するオンラインアカウントのアクセス許可によって、実行できる操作が決まります。  
  
     Office 365 統合の管理者アカウントを確認するには、ダッシュボードの **[office 365]** タブを開きます。  
  
## <a name="other-things-you-might-want-to-do"></a>その他の推奨操作  
  
-   [My Server アプリを使用して任意の場所から SharePoint Online ライブラリを操作する](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)  
  
-   [SharePoint チームサイトのアクセス許可の割り当てに関する詳細情報](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/introduction-control-user-access-with-permissions-HA102771919.aspx?CTT=5&origin=HA102771924)  
  
-   [SharePoint 機能でできることを確認する](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/get-started-with-sharepoint-2013-HA102772778.aspx)  
  
-   [使用可能な Office 365 ビジネスプランを確認する](https://office.microsoft.com/business/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_what-is-office-365-for_Text)  
  
-   [Office 365 をサーバーと統合する](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
-   [ダッシュボードから他の Microsoft オンラインサービスを管理する](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)
