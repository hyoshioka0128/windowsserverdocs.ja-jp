---
title: AD FS トラブルシューティング-AD FS エンドポイント
description: このドキュメントでは AD FS エンドポイントのトラブルシューティングの方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 807b5c5de14bf6a43419d0b9d2d3a4e6953d0075
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366222"
---
# <a name="ad-fs-troubleshooting---ad-fs-metadata-endpoints"></a>AD FS トラブルシューティング-AD FS メタデータエンドポイント
エンドポイントは、フェデレーションメタデータの公開など、AD FS のフェデレーションサーバー機能へのアクセスを提供します。  AD FS サーバーが web 要求に応答していることを確認するには、さまざまなエンドポイントを確認します。


## <a name="federation-metadata-test"></a>フェデレーションメタデータテスト
パッシブフェデレーションとは、ブラウザーが AD FS サインインページにリダイレクトされるシナリオを指します。  メタデータエンドポイントをテストすることで、AD FS サーバーがこれらのパッシブなシナリオで web 要求に応答しているかどうかを判断できます。  エンドポイントをテストするには、次の手順に従います。

1.  Web ブラウザーを使用して、AD FS フェデレーションメタデータエンドポイントに移動します。  次に例を示します。 https://sts.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml
2. Xml ファイルは、ローカルコンピューターにダウンロードする必要があります。
3. それを開き、![パッシブ](media/ad-fs-tshoot-endpoints/meta2.png) のような情報が含まれていることを確認します。

## <a name="ws-mex-test-active-test"></a>WS-ATOMICTRANSACTION テスト (アクティブなテスト)
Ws-metadataexchange は web サービスプロトコルであり、WS-FEDERATION ロードマップに含まれています。  SOAP メッセージを使用してメタデータを要求します。  エンドポイントをテストすることで、AD FS サーバーが Ws-metadataexchange の web 要求に応答しているかどうかを判断できます。  エンドポイントをテストするには、次の手順に従います。
1.  Web ブラウザーを使用して、AD FS フェデレーションメタデータエンドポイントに移動します。  次に例を示します。 https://sts.contoso.com/adfs/services/trust/mex
2. Xml ファイルは、ブラウザーに自動的に表示されます。  次の図のようになります。

![Active](media/ad-fs-tshoot-endpoints/meta3.png)


## <a name="next-steps"></a>次のステップ

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)