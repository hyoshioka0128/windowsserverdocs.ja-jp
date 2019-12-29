---
title: bitsadmin setclientcertificatebyname
description: '**Bitsadmin setclientcertificatebyname**の Windows コマンドのトピック-HTTPS (SSL) 要求でクライアント認証に使用するクライアント証明書のサブジェクト名を指定します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f308a6d9-d0da-48be-ae41-eced14b3cccb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de2e84401673848ecc8823bb6dd3f91224d9a87e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380669"
---
# <a name="bitsadmin-setclientcertificatebyname"></a>bitsadmin setclientcertificatebyname



HTTPS (SSL) 要求でクライアント認証に使用するクライアント証明書のサブジェクト名を指定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetClientCertificateByID <Job> <store_location> <store_name> <subject_name>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|Store_location|証明書の検索に使用するシステムストアの場所を指定します。 有効な値は次のとおりです。</br>1 (CURRENT_USER)</br>2 (LOCAL_MACHINE)</br>3 (CURRENT_SERVICE)</br>4 (サービス)</br>5 (ユーザー)</br>6 (CURRENT_USER_GROUP_POLICY)</br>7 (LOCAL_MACHINE_GROUP_POLICY)</br>8 (LOCAL_MACHINE_ENTERPRISE)|
|Store_name|証明書ストアの名前。 有効な値は次のとおりです。</br>CA (証明機関の証明書)</br>MY (個人用証明書)</br>ルート (ルート証明書)</br>SPC (ソフトウェア発行元証明書)|
|Subject_name|証明書の名前|

## <a name="BKMK_examples"></a>例

次の例では、 *mycertificate*という名前のジョブに対する HTTPS (SSL) 要求でクライアント認証に使用するクライアント証明書*mycertificate*の名前を指定します。
```
C:\>bitsadmin Bitsadmin /SetClientCertificateByName myJob 1 MY myCertificate 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)