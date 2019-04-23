---
title: bitsadmin setclientcertificatebyname
description: Windows コマンド」のトピック**bitsadmin setclientcertificatebyname** -HTTPS (SSL) 要求でクライアント認証を使用するクライアント証明書のサブジェクト名を指定します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 76150ccb34693eb692d27efbd6538f5363ba1c26
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871313"
---
# <a name="bitsadmin-setclientcertificatebyname"></a>bitsadmin setclientcertificatebyname



HTTPS (SSL) 要求でクライアント認証を使用するクライアント証明書のサブジェクト名を指定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetClientCertificateByID <Job> <store_location> <store_name> <subject_name>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|Store_location|証明書の検索に使用するシステム ストアの場所を示します。 有効な値は次のとおりです。</br>1 (CURRENT_USER)</br>2 (LOCAL_MACHINE)</br>3 (CURRENT_SERVICE)</br>4 (サービス)</br>5 (ユーザー)</br>6 (CURRENT_USER_GROUP_POLICY)</br>7 (LOCAL_MACHINE_GROUP_POLICY)</br>8 (LOCAL_MACHINE_ENTERPRISE)|
|ストア名|証明書ストアの名前。 有効な値は次のとおりです。</br>CA (証明機関の証明書)</br>(個人証明書)</br>ルート (ルート証明書)</br>SPC (ソフトウェア発行元の証明書)|
|Subject_name|証明書の名前|

## <a name="BKMK_examples"></a>例

次の例では、クライアント証明書の名前を指定します。 *myCertificate*という名前のジョブの HTTPS (SSL) 要求でクライアント認証に使用する*myJob*します。
```
C:\>bitsadmin Bitsadmin /SetClientCertificateByName myJob 1 MY myCertificate 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)