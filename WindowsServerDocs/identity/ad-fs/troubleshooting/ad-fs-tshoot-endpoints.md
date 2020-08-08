---
title: AD FS トラブルシューティング-AD FS エンドポイント
description: このドキュメントでは AD FS エンドポイントのトラブルシューティングの方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.openlocfilehash: 7739093e483e8f797e87259c176ff3c92514903d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954168"
---
# <a name="ad-fs-troubleshooting---ad-fs-metadata-endpoints"></a>AD FS トラブルシューティング-AD FS メタデータエンドポイント
エンドポイントは、フェデレーションメタデータの公開など、AD FS のフェデレーションサーバー機能へのアクセスを提供します。  AD FS サーバーが web 要求に応答していることを確認するには、さまざまなエンドポイントを確認します。


## <a name="federation-metadata-test"></a>フェデレーションメタデータテスト
パッシブフェデレーションとは、ブラウザーが AD FS サインインページにリダイレクトされるシナリオを指します。  メタデータエンドポイントをテストすることで、AD FS サーバーがこれらのパッシブなシナリオで web 要求に応答しているかどうかを判断できます。  エンドポイントをテストするには、次の手順に従います。

1.  Web ブラウザーを使用して、AD FS フェデレーションメタデータエンドポイントに移動します。  次に例を示します。https://sts.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml
2. Xml ファイルは、ローカルコンピューターにダウンロードする必要があります。
3. それを開き、次のような情報が含まれていることを確認します。 ![ パッシブ情報](media/ad-fs-tshoot-endpoints/meta2.png)

## <a name="ws-mex-test-active-test"></a>WS-ATOMICTRANSACTION テスト (アクティブなテスト)
Ws-metadataexchange は web サービスプロトコルであり、WS-FEDERATION ロードマップに含まれています。  SOAP メッセージを使用してメタデータを要求します。  エンドポイントをテストすることで、AD FS サーバーが Ws-metadataexchange の web 要求に応答しているかどうかを判断できます。  エンドポイントをテストするには、次の手順に従います。
1.  Web ブラウザーを使用して、AD FS フェデレーションメタデータエンドポイントに移動します。  次に例を示します。https://sts.contoso.com/adfs/services/trust/mex
2. Xml ファイルは、ブラウザーに自動的に表示されます。  出力は下の図のようになります。

![アクティブ](media/ad-fs-tshoot-endpoints/meta3.png)


## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)