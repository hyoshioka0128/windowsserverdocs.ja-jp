---
title: bitsadmin setclientcertificatebyname
description: Bitsadmin setclientcertificatebyname コマンドの参照記事。 HTTPS (SSL) 要求でクライアント認証に使用するクライアント証明書のサブジェクト名を指定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f308a6d9-d0da-48be-ae41-eced14b3cccb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 86f314137b6ebc3e866fa91d1c86c1c5e8294f86
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927870"
---
# <a name="bitsadmin-setclientcertificatebyname"></a>bitsadmin setclientcertificatebyname

HTTPS (SSL) 要求でクライアント認証に使用するクライアント証明書のサブジェクト名を指定します。

## <a name="syntax"></a>構文

```
bitsadmin /setclientcertificatebyname <job> <store_location> <store_name> <subject_name>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| store_location | 証明書の検索に使用するシステムストアの場所を指定します。 指定できる値は、次のとおりです。<ul><li>1 (CURRENT_USER)</li><li>2 (LOCAL_MACHINE)</li><li>3 (CURRENT_SERVICE)</li><li>4 (サービス)</li><li>5 (ユーザー)</li><li>6 (CURRENT_USER_GROUP_POLICY)</li><li>7 (LOCAL_MACHINE_GROUP_POLICY)</li><li>8 (LOCAL_MACHINE_ENTERPRISE)</li></ul> |
| store_name | 証明書ストアの名前。 指定できる値は、次のとおりです。<ul><li>CA (証明機関の証明書)</li><li>MY (個人用証明書)</li><li>ルート (ルート証明書)</li><li>SPC (ソフトウェア発行元証明書)</li></ul> |
| subject_name | 証明書の名前。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの HTTPS (SSL) 要求でクライアント認証に使用するクライアント証明書*mycertificate*の名前を指定するには、次のようにします。

```
bitsadmin /setclientcertificatebyname myDownloadJob 1 MY myCertificate
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
