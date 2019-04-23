---
title: AD FS のトラブルシューティング - AD FS のエンドポイント
description: このドキュメントは、AD FS エンドポイントのトラブルシューティングを行う方法を説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 13b830c0317341280bd87499e3abd8dcd1a33fc2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857563"
---
# <a name="ad-fs-troubleshooting---ad-fs-metadata-endpoints"></a>AD FS のトラブルシューティング - AD FS のメタデータ エンドポイント
エンドポイントは、フェデレーション メタデータの公開などの AD FS のフェデレーション サーバーの機能へのアクセスを提供します。  AD FS サーバーが web 要求に応答していることを確認するには、私たちには、さまざまなエンドポイントを確認できます。


## <a name="federation-metadata-test"></a>フェデレーション メタデータのテスト
パッシブ フェデレーションは、ブラウザー、AD FS サインイン ページにリダイレクトするシナリオを指します。  メタデータ エンドポイントをテストして、AD FS サーバーがパッシブのシナリオではこれらの web 要求に応答してかどうかを判断できます。  エンドポイントをテストするには、次の手順を使用します。

1.  Web ブラウザーを使用して、AD FS のフェデレーション メタデータ エンドポイントに移動します。  例えば：  https://sts.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml
2. Xml ファイルは、コンピューターにローカルにダウンロードする必要があります。
3. それを開き、次の情報のような情報が含まれていることを確認します。![パッシブ](media/ad-fs-tshoot-endpoints/meta2.png)

## <a name="ws-mex-test-active-test"></a>WS-MEX テスト (アクティブなテスト)
Ws-metadataexchange は、web サービス プロトコルでは Ws-federation ロードマップの一部です。  メタデータを要求するのに SOAP メッセージを使用します。  エンドポイントをテストして、ws-metadataexchange、AD FS サーバーが web 要求に応答しているを判断できます。  エンドポイントをテストするには、次の手順を使用します。
1.  Web ブラウザーを使用して、AD FS のフェデレーション メタデータ エンドポイントに移動します。  例えば：  https://sts.contoso.com/adfs/services/trust/mex
2. Xml ファイルは、ブラウザーで自動的に表示する必要があります。  次の図のようになります。

![Active](media/ad-fs-tshoot-endpoints/meta3.png)


## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)