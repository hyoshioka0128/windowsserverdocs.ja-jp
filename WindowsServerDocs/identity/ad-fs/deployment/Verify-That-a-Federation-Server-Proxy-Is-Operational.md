---
ms.assetid: d555041a-709e-42c7-920a-8dfd2c7e0488
title: フェデレーション サーバー プロキシが正常に動作していることを確認する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3e74af4a63476040ca44522ceb7c0ae22e914fec
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855855"
---
# <a name="verify-that-a-federation-server-proxy-is-operational"></a>フェデレーション サーバー プロキシが正常に動作していることを確認する


フェデレーションサーバープロキシが Active Directory フェデレーションサービス (AD FS) \(AD FS\)のフェデレーションサービスと通信できることを確認するには、次の手順に従います。 **AD FS フェデレーションサーバープロキシ構成ウィザード**を実行して、フェデレーションサーバープロキシの役割で実行されるようにコンピューターを構成した後に、この手順を実行します。 このウィザードの実行方法の詳細については、「 [Configure a Computer for The Federation Server Proxy Role](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)」を参照してください。  
  
> [!IMPORTANT]  
> このテスト結果は、フェデレーション サーバー プロキシ コンピューターのイベント ビューアーに、特定の成功イベントとして生成されます。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-verify-that-a-federation-server-proxy-is-operational"></a>フェデレーションサーバープロキシが動作可能であることを確認するには  
  
1.  フェデレーションサーバープロキシに管理者としてログオンします。  
  
2.  **スタート**画面で、「**イベントビューアー**」と入力し、enter キーを押します。  
  
3.  詳細ウィンドウで、**アプリケーションとサービスログ** をダブル\-クリックし、**イベント AD FS**の\-をダブルクリックして、**管理者** をクリックします。  
  
4.  **[イベント ID]** 列で、イベント ID 198 を見つけます。  
  
    フェデレーションサーバープロキシが適切に構成されている場合は、イベントビューアーのアプリケーションログにイベント ID 198 の新しいイベントが表示されます。 このイベントは、フェデレーションサーバープロキシサービスが正常に開始され、現在はオンラインになっていることを確認します。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

