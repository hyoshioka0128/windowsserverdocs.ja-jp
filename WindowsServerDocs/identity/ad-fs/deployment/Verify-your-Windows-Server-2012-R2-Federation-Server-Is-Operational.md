---
ms.assetid: 1115d276-00f6-4c23-9278-eedcc31295d8
title: Windows Server 2012 R2 フェデレーションサーバーが動作していることを確認する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 82cad5a13478986208f5f19d1905290fb0097655
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940866"
---
# <a name="verify-your-windows-server-2012-r2-federation-server-is-operational"></a>Windows Server 2012 R2 フェデレーションサーバーが動作していることを確認する



以下の手順を使用して、フェデレーション サーバーが動作可能であること (つまり、同じネットワーク上のクライアントから新しいフェデレーション サーバーにアクセスできること) を確認します。

この手順を実行するには、少なくとも **Users**、**Backup Operators**、**Power Users**、または **Administrators** グループのメンバーであるか、そのメンバーと同等の権限が必要になります。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。

### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>手順 1: フェデレーションサーバーが動作可能であることを確認するには

1.  フェデレーションサーバーでインターネットインフォメーションサービス IIS が正しく構成されていることを確認するには \( \) 、フェデレーションサーバーと同じフォレストにあるクライアントコンピューターにログオンします。

2.  ブラウザーウィンドウを開き、アドレスバーにフェデレーションサーバーの DNS ホスト名を入力し、 \/ \/ \/ 新しいフェデレーションサーバーに adfs fs federationserverservice を追加します。次に例を示します。

    **https: \/ \/ fs1.fabrikam.com \/ adfs \/ fs \/ federationserverservice**

3.  Enter キーを押し、フェデレーション サーバー コンピューターの次の手順を完了します。 [**この web サイトのセキュリティ証明書に問題があり**ます] というメッセージが表示された場合は、[**このサイトの使用を続行する**] をクリックします。

    期待される表示出力は、サービス内容に関する XML ドキュメントです。 このページが表示されたら、フェデレーション サーバーの IIS は動作可能であり、正常にページを提供します。

この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。

### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>手順 2: フェデレーションサーバーが動作可能であることを確認するには

1.  管理者として新しいフェデレーション サーバーにログオンします。

2.  **スタート**画面で、「**イベントビューアー**」と入力し、enter キーを押します。

3.  詳細ウィンドウで、 \- [**アプリケーションとサービスログ**] をダブルクリックし、[AD FS イベント] をダブルクリックして、[ \- **管理者**] をクリックします。 **AD FS Eventing**

4.  [**イベント id** ] 列で、イベント id 100 を探します。 フェデレーションサーバーが適切に構成されている場合は、イベントビューアーのアプリケーションログに、イベント ID 100 の新しいイベントが表示されます。 このイベントにより、フェデレーション サーバーがフェデレーション サービスと正常に通信できたことが確認されます。

## <a name="see-also"></a>参照

[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)

[Windows Server 2012 R2 AD FS の展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)

[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)



