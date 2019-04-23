---
title: bitsadmin setsecurityflags
description: Windows コマンド」のトピック**bitsadmin setsecurityflags** -フラグ セットのビット必要があります、証明書失効リスト、特定の証明書のエラーを無視するとするときに使用するポリシーを定義する HTTP サーバーHTTP 要求をリダイレクトします。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da5cbf5-5f7f-4833-bbbe-c4e8379a78ab
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a7f74146a26314ddb4fa92f85e5a40267d0f0d9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858623"
---
# <a name="bitsadmin-setsecurityflags"></a>bitsadmin setsecurityflags



HTTP ビット必要があります、証明書失効リスト、特定の証明書のエラーを無視すると、サーバーが HTTP 要求をリダイレクトするときに使用するポリシーを定義するのには、フラグを設定します。 値は、符号なし整数です。

## <a name="syntax"></a>構文

```
bitsadmin /SetSecurityFlags <Job> <Value>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|値|「解説」を参照してください。|

## <a name="remarks"></a>注釈

**値**パラメーターは、次の通知フラグの 1 つ以上含めることができます。

|アクション|バイナリ表現|
|------|---------------------|
|CRL チェックを有効にします。|最下位ビットを設定します。|
|サーバー証明書での無効な共通名を無視します。|右から 2 番目のビットを設定します。|
|サーバー証明書に無効な日付を無視します。|右から 3 番目のビットを設定します。|
|サーバー証明書内の無効な証明機関を無視します。|右から 4 番目のビットを設定します。|
|証明書の無効な使用法を無視します。|右から 5 番目のビットを設定します。|
|リダイレクト ポリシー|右から 9 日に 11 ビットで制御されます。</br>0,0,0 - リダイレクトが自動的に許可されます。</br>0,0,1 - リダイレクトが発生した場合、IBackgroundCopyFile インターフェイスのリモート名が更新されます。</br>0,1,0 - リダイレクトが発生する場合のビットには、ジョブが失敗します。|
|HTTPS から HTTP へのリダイレクトを許可します。|右から 12 のビットを設定します。|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの CRL チェックを有効にするセキュリティ フラグを設定する*myJob*します。
```
C:\>bitsadmin /SetSecurityFlags myJob 0x0001
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)