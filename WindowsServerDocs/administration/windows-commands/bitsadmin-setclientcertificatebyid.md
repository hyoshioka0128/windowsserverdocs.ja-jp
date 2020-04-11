---
title: bitsadmin setclientcertificatebyid
description: '**Bitsadmin setclientcertificatebyid**の Windows コマンドに関するトピック。 HTTPS (SSL) 要求でクライアント認証に使用するクライアント証明書の識別子を指定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8585a7a1-7472-437b-b04a-a11925782a3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 376bb850664a5ed569488634029cb7384856f158
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123042"
---
# <a name="bitsadmin-setclientcertificatebyid"></a>bitsadmin setclientcertificatebyid

HTTPS (SSL) 要求でクライアント認証に使用するクライアント証明書の識別子を指定します。

## <a name="syntax"></a>構文

```
bitsadmin /setclientcertificatebyid <job> <store_location> <store_name> <hexadecimal_cert_id>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |
| store_location | 次のような、証明書の検索に使用するシステムストアの場所を指定します。<ul><li>CURRENT_USER</li><li>LOCAL_MACHINE</li><li>CURRENT_SERVICE</li><li>サービス</li><li>ユーザー</li><li>CURRENT_USER_GROUP_POLICY</li><li>LOCAL_MACHINE_GROUP_POLICY</li><li>LOCAL_MACHINE_ENTERPRISE。</li></ul> |
| store_name | 証明書ストアの名前 (以下を含む)。<ul><li>CA (証明機関の証明書)</li><li>MY (個人用証明書)</li><li>ルート (ルート証明書)</li><li>SPC (ソフトウェア発行元証明書)。</li></ul> |
| hexadecimal_cert_id | 証明書のハッシュを表す16進数。 |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブに対する HTTPS (SSL) 要求でクライアント認証に使用するクライアント証明書の識別子を指定します。

```
C:\>bitsadmin /setclientcertificatebyid myDownloadJob BG_CERT_STORE_LOCATION_CURRENT_USER MY A106B52356D3FBCD1853A41B619358BD
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)