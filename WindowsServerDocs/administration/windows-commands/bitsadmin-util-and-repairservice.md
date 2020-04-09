---
title: bitsadmin util と repairservice
description: Bitsadmin util と repairservice の Windows コマンドに関するトピックでは、さまざまなバージョンの BITS サービスの既知の問題を修正しました。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aaaa6edab22031dc53d266984bb669634e3bb362
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848895"
---
# <a name="bitsadmin-util-and-repairservice"></a>bitsadmin util と repairservice

BITS を起動できない場合は、このスイッチを使用して、さまざまなバージョンの BITS の既知の問題を修正します。

**BITSAdmin 1.5 以前:**  サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /Util /RepairService [/Force]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Force|省略可能: サービスを削除して再作成します。|

## <a name="remarks"></a>コメント

このスイッチは、不適切なサービス構成と Windows サービス (LANManworkstation など) およびネットワークディレクトリの依存関係に関連するエラーを解決します。 このスイッチは、解決された問題が発生したかどうかを示す出力を生成します。

> [!NOTE]
> BITS がサービスを再作成する場合、ローカライズされたシステムでサービスの説明文字列が英語に設定されている可能性があります。

> [!IMPORTANT]
> このコマンドは、Windows Vista ではサポートされていません。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、BITS サービスの構成を修復します。
```
C:\>bitsadmin /Util /RepairService
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)