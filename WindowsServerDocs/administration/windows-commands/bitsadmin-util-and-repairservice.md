---
title: bitsadmin util と repairservice
description: さまざまなバージョンの BITS サービスに関する既知の問題を修正するために使用される**bitsadmin util と repairservice**コマンドの Windows コマンドに関するトピック。
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 0ab06ac9c784cfa438eb285c28f0e661cf4b8302
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380279"
---
# <a name="bitsadmin-util-and-repairservice"></a>bitsadmin util と repairservice

BITS を起動できない場合は、このスイッチを使用して、さまざまなバージョンの BITS に関する既知の問題を修正します。

**BITSAdmin 1.5 以前:**   はサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /Util /RepairService [/Force]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Force|省略可能: サービスを削除して再作成します。|

## <a name="remarks"></a>コメント

このスイッチは、不適切なサービス構成と Windows サービス (LANManworkstation など) およびネットワークディレクトリの依存関係に関連するエラーを解決します。 このスイッチは、解決された問題が発生したかどうかを示す出力を生成します。

> [!NOTE]
> BITS がサービスを再作成する場合、ローカライズされたシステムでサービスの説明文字列が英語に設定されている可能性があります。

> [!IMPORTANT]
> このコマンドは、Windows Vista ではサポートされていません。

## <a name="BKMK_examples"></a>例

次の例では、BITS サービスの構成を修復します。
```
C:\>bitsadmin /Util /RepairService
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)