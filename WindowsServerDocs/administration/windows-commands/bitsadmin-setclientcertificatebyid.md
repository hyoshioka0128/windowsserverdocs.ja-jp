---
title: bitsadmin setclientcertificatebyid
description: Windows コマンド」のトピック**bitsadmin setclientcertificatebyid** HTTPS (SSL) 要求でクライアント認証を使用するクライアント証明書の識別子を指定します
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8585a7a1-7472-437b-b04a-a11925782a3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2424de18ee8aaec73b086207e8ef56d85df862fa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863933"
---
# <a name="bitsadmin-setclientcertificatebyid"></a>bitsadmin setclientcertificatebyid



HTTPS (SSL) 要求でクライアント認証を使用するクライアント証明書の識別子を指定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetClientCertificateByID <Job> <store_location> <store_name> hexa-decimal_cert_id>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|Store_location|証明書の検索に使用するシステム ストアの場所を示します。 有効な値は次のとおりです。</br>1 (CURRENT_USER)</br>2 (LOCAL_MACHINE)</br>3 (CURRENT_SERVICE)</br>4 (サービス)</br>5 (ユーザー)</br>6 (CURRENT_USER_GROUP_POLICY)</br>7 (LOCAL_MACHINE_GROUP_POLICY)</br>8 (LOCAL_MACHINE_ENTERPRISE)|
|ストア名|証明書ストアの名前。 有効な値は次のとおりです。</br>CA (証明機関の証明書)</br>(個人証明書)</br>ルート (ルート証明書)</br>SPC (ソフトウェア発行元の証明書)|
|Hexadecimal_cert_id|証明書のハッシュを表す 16 進数|

## <a name="BKMK_examples"></a>例

次の例では、HTTPS (SSL) 要求という名前のジョブでのクライアント認証を使用するクライアント証明書の識別子を指定する*myJob*します。
```
C:\>bitsadmin Bitsadmin /SetClientCertificateByID myJob BG_CERT_STORE_LOCATION_CURRENT_USER MY A106B52356D3FBCD1853A41B619358BD 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)