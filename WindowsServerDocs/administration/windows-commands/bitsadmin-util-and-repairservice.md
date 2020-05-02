---
title: bitsadmin util および repairservice
description: Bitsadmin util と repairservice コマンドのリファレンストピック。これにより、さまざまなバージョンの BITS サービスの既知の問題が修正されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0104a3f2ace972821151bf5083f9b0795e427ff1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707653"
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

| パラメーター | [説明] |
| --------- | ----------- |
| /force | 任意。 サービスを削除してから再度作成します。|

> [!NOTE]
> BITS によってサービスが再度作成される場合、ローカライズされたシステムでもサービスの説明文字列が英語に設定されている可能性があります。

## <a name="examples"></a>例

BITS サービス構成を修復するには:

```
bitsadmin /util /repairservice
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin util コマンド](bitsadmin-util.md)

- [bitsadmin コマンド](bitsadmin.md)
