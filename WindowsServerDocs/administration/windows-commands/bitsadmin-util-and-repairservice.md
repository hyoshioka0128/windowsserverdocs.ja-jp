---
title: bitsadmin util と repairservice
description: Windows コマンド」のトピック**bitsadmin util と repairservice** -コマンドさまざまなバージョンの BITS サービスに関する既知の問題を解決するために使用します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc5101378a389c865f5753146b711be0d15c6785
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852093"
---
# <a name="bitsadmin-util-and-repairservice"></a>bitsadmin util と repairservice

ビットが起動しない場合は、さまざまなバージョンのビットに関する既知の問題を解決するこのスイッチを使用します。

**1.5 およびそれ以前の BITSAdmin:** はサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /Util /RepairService [/Force]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Force|省略可能: 削除し、サービスを再作成されます。|

## <a name="remarks"></a>注釈

このスイッチは、エラーに関連する不適切なサービスの構成と LANManworkstation) などの Windows サービスへの依存関係ネットワーク ディレクトリを解決します。 このスイッチを示す出力を生成するかどうか、問題が解決されました。

> [!NOTE]
> BITS では、サービスが再作成場合、サービスの説明文字列をローカライズされたシステムで英語に設定できます。

> [!IMPORTANT]
> このコマンドは、Windows Vista ではサポートされていません。

## <a name="BKMK_examples"></a>例

次の例では、BITS サービス構成を修復します。
```
C:\>bitsadmin /Util /RepairService
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)