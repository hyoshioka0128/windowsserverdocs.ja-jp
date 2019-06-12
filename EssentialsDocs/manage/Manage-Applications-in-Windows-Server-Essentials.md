---
title: Windows Server Essentials でのアプリケーションの管理
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae89c46a-0afd-4858-9150-ec97650f45a4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1a60a9e7fd958d447b4770431a69546f0ad6f229
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433348"
---
# <a name="manage-applications-in-windows-server-essentials"></a>Windows Server Essentials でのアプリケーションの管理

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials
 
 サーバーで Windows Server Essentials ダッシュ ボードおよび Windows Server Essentials エクスペリエンス役割がインストールされた Windows Server 2012 R2 では、一般的な管理タスクを実行できます。 これらのタスクを実行するには、次の手順を参照してください。  
  
-   [ダッシュ ボードでのアプリケーション管理タスク](Manage-Applications-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [インストールまたはダッシュ ボードを使用してアドインを削除します。](Manage-Applications-in-Windows-Server-Essentials.md#BKMK_2)  
  
##  <a name="BKMK_1"></a> ダッシュ ボードでのアプリケーション管理タスク  
 ダッシュボードの **[アプリケーション]** 管理ページには、次の項目が表示されます。  
  
- 次の情報を含む、インストールされているアドインの一覧  
  
  -   オンライン サービスまたはアドインの名前  
  
  -   アドインの更新状態  
  
  -   アドインのサブスクリプション状態  
  
  -   アドインを利用可能にする会社または発行元の名前  
  
- 選択したアドインを管理するための一連のタスクが含まれる作業ウィンドウ  
  
- Microsoft Pinpoint からダウンロードしてインストールできるアドインの一覧  
  
  次の表は、サーバー ダッシュボードで利用できるさまざまなアドインの管理タスクについて説明しています。 一部のタスクはアドインに固有であり、一覧からアドインを選択した場合にのみ表示されます。  
  
|タスク名|説明|  
|---------------|-----------------|  
|アドインの削除|サーバーおよびネットワーク上の他のすべてのコンピューターから、選択したアドインを削除します。|  
|ネットワーク上のコンピューターへのアドインのインストール|ネットワーク上の他のすべてのコンピューターへの選択したアドインのインストールをスケジュールできます。|  
|アドインに関するヘルプの表示|インターネット ブラウザーから Web サイトを開き、問題の解決策を検索したり、選択したアドインに関する詳細情報を確認したりすることができます。|  
|アドインの更新|サーバーやネットワーク コンピューターにインストールされているアドインの更新プログラムをダウンロードしてインストールできます。|  
|アドインのサブスクリプションの更新|インターネット ブラウザーから Web サイトを開いて、アドインのサブスクリプションを更新できます。|  
|アドインのプライバシーに関する声明の確認|インターネット ブラウザーから Web サイトを開いて、プライバシーに関する声明を確認できます。|  
|インストールまたはすれば、アドインを削除しますか。|インターネット ブラウザーから Web ページを開いて、該当するヘルプ トピックを表示します。|  
  
##  <a name="BKMK_2"></a> インストールまたはダッシュ ボードを使用してアドインを削除します。  
 アドインは、サーバーに追加機能を提供するソフトウェア アプリケーションです。 Microsoft および他の独立系ソフトウェア ベンダー (ISV) から多数のアドインを利用できます。  
  
 アドインが提供する拡張機能を活用するには、サーバー上にアドインをインストールする必要があります。  
  
#### <a name="to-install-an-add-in-from-microsoft-pinpoint"></a>Microsoft Pinpoint からアドインをインストールするには  
  
1.  サーバー ダッシュボードで、 **[アプリケーション]** をクリックし、 **[Microsoft Pinpoint]** タブをクリックします。使用可能なアドインの一覧が表示されます。  
  
2.  インストールするアドインをクリックします。 アドインの情報ページが表示されます。  
  
3.  アドインの情報ページで、[ダウンロード] をクリックし、画面の指示に従ってアドインをダウンロードしてインストールします。  
  
4.  ウィザードの指示に従ってアドインをインストールします。  
  
5.  インストールが完了したら、ダッシュボードを再起動し、サーバー ダッシュボードで **[アプリケーション]** ページを開いて、インストールしたアドインが一覧に表示されていることを確認します。  
  
#### <a name="to-install-an-add-in-from-another-provider"></a>別のプロバイダーからのアドインをインストールするには  
  
1.  Windows エクスプローラーを開き、アドインのインストール ファイルの場所を参照します。  
  
2.  ファイルをダブルクリックして、インストール ウィザードを実行します。  
  
3.  ウィザードの指示に従ってアドインをインストールします。  
  
4.  インストールが完了したら、ダッシュボードを再起動して **[アプリケーション]** ページを開き、インストールしたアドインが一覧に表示されていることを確認します。  
  
#### <a name="to-remove-an-add-in"></a>アドインを削除するには  
  
1.  サーバー ダッシュボードを開きます。  
  
2.  **[アプリケーション]** タブをクリックします。  
  
3.  **[アドイン]** タブで、削除するアドインを選択し、 **[アドインの削除]** をクリックします。  
  
4.  **[アドインの削除]** ウィンドウで、 **[削除]** をクリックします。  
  
    > [!NOTE]
    >  アドインを完全に削除するには、ダッシュボードの再起動が必要な場合があります。  
  
## <a name="see-also"></a>関連項目  
  
-   [ダッシュ ボードの概要](Overview-of-the-Dashboard-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials の管理](Manage-Windows-Server-Essentials.md)
