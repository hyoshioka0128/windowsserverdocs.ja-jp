---
ms.assetid: d555041a-709e-42c7-920a-8dfd2c7e0488
title: フェデレーション サーバー プロキシが正常に動作していることを確認する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 4550934c56b4406ea7aff9b90509a205014dd95d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940961"
---
# <a name="verify-that-a-federation-server-proxy-is-operational"></a>フェデレーション サーバー プロキシが正常に動作していることを確認する


フェデレーションサーバープロキシが Active Directory フェデレーションサービス (AD FS) AD FS のフェデレーションサービスと通信できることを確認するには、次の手順に従い \( \) ます。 **AD FS フェデレーションサーバープロキシ構成ウィザード**を実行して、フェデレーションサーバープロキシの役割で実行されるようにコンピューターを構成した後に、この手順を実行します。 このウィザードの実行方法の詳細については、「 [Configure a Computer for The Federation Server Proxy Role](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)」を参照してください。

> [!IMPORTANT]
> このテスト結果は、フェデレーション サーバー プロキシ コンピューターのイベント ビューアーに、特定の成功イベントとして生成されます。

この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。

### <a name="to-verify-that-a-federation-server-proxy-is-operational"></a>フェデレーションサーバープロキシが動作可能であることを確認するには

1.  フェデレーションサーバープロキシに管理者としてログオンします。

2.  **スタート**画面で、「**イベントビューアー**」と入力し、enter キーを押します。

3.  詳細ウィンドウで、 \- [**アプリケーションとサービスログ**] をダブルクリックし、[AD FS イベント] をダブルクリックして、[ \- **管理者**] をクリックします。 **AD FS Eventing**

4.  [**イベント ID**] 列で、イベント ID 198 を見つけます。

    フェデレーションサーバープロキシが適切に構成されている場合は、イベントビューアーのアプリケーションログにイベント ID 198 の新しいイベントが表示されます。 このイベントは、フェデレーションサーバープロキシサービスが正常に開始され、現在はオンラインになっていることを確認します。

## <a name="additional-references"></a>その他の参照情報
[チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)


