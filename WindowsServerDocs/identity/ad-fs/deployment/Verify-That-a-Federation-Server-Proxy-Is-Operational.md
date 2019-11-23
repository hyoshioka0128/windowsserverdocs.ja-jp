---
ms.assetid: d555041a-709e-42c7-920a-8dfd2c7e0488
title: フェデレーション サーバー プロキシが正常に動作していることを確認する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 24f4fe2a152244dc904be82c4c10abe71abffcc4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359969"
---
# <a name="verify-that-a-federation-server-proxy-is-operational"></a>フェデレーション サーバー プロキシが正常に動作していることを確認する


フェデレーションサーバープロキシが Active Directory フェデレーションサービス (AD FS) \(AD FS\)のフェデレーションサービスと通信できることを確認するには、次の手順に従います。 **AD FS フェデレーションサーバープロキシ構成ウィザード**を実行して、フェデレーションサーバープロキシの役割で実行されるようにコンピューターを構成した後に、この手順を実行します。 このウィザードの実行方法の詳細については、「 [フェデレーション サーバー プロキシの役割用にコンピューターを構成する](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)」を参照してください。  
  
> [!IMPORTANT]  
> このテスト結果は、フェデレーション サーバー プロキシ コンピューターのイベント ビューアーに、特定の成功イベントとして生成されます。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-verify-that-a-federation-server-proxy-is-operational"></a>フェデレーションサーバープロキシが動作可能であることを確認するには  
  
1.  フェデレーションサーバープロキシに管理者としてログオンします。  
  
2.  **スタート**画面で、「**イベントビューアー**」と入力し、enter キーを押します。  
  
3.  詳細ウィンドウで、**アプリケーションとサービスログ** をダブル\-クリックし、**イベント AD FS**の\-をダブルクリックして、**管理者** をクリックします。  
  
4.  **[イベント id]** 列で、イベント id 198 を探します。  
  
    フェデレーションサーバープロキシが適切に構成されている場合は、イベントビューアーのアプリケーションログにイベント ID 198 の新しいイベントが表示されます。 このイベントは、フェデレーションサーバープロキシサービスが正常に開始され、現在はオンラインになっていることを確認します。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

