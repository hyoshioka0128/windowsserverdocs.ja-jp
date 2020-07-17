---
title: bitsadmin util および repairservice
description: Bitsadmin util と repairservice コマンドのリファレンス記事。さまざまなバージョンの BITS サービスの既知の問題を修正します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cf62a9410765914187b6a60ff5376e8ff5aabe03
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927346"
---
# <a name="bitsadmin-util-and-repairservice"></a>bitsadmin util および repairservice

BITS の起動に失敗した場合、このスイッチは、Windows サービス (LANManworkstation など) およびネットワークディレクトリの不適切なサービス構成および依存関係に関連するエラーの解決を試みます。 また、このスイッチは、解決された問題があるかどうかを示す出力も生成します。

> [!NOTE]
> このコマンドは、BITS 1.5 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /util /repairservice [/force]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /force | 任意。 サービスを削除してから再度作成します。|

> [!NOTE]
> BITS によってサービスが再度作成される場合、ローカライズされたシステムでもサービスの説明文字列が英語に設定されている可能性があります。

## <a name="examples"></a>例

BITS サービス構成を修復するには:

```
bitsadmin /util /repairservice
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin util コマンド](bitsadmin-util.md)

- [bitsadmin コマンド](bitsadmin.md)
