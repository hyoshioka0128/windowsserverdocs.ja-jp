---
title: bitsadmin util と repairservice
description: '**Bitsadmin util と repairservice**の Windows コマンドに関するトピックでは、さまざまなバージョンの BITS サービスの既知の問題を修正しました。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 164a402e7cbfc0a9223a97f4246eac84f0797aed
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122516"
---
# <a name="bitsadmin-util-and-repairservice"></a>bitsadmin util と repairservice

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
| /force | 省略可。 サービスを削除してから再度作成します。|

> [!NOTE]
> BITS によってサービスが再度作成される場合、ローカライズされたシステムでもサービスの説明文字列が英語に設定されている可能性があります。

## <a name="examples"></a>例

次の例では、BITS サービスの構成を修復します。

```
C:\>bitsadmin /util /repairservice
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)