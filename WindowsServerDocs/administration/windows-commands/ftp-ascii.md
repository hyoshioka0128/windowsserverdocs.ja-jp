---
title: ftp ascii
description: Ftp ascii コマンドの参照記事。ファイル転送の種類を ASCII に設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 523be48e-eab0-4237-8fb5-ca222824f0b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e3ba10ba6498b48a19aacf6235c84a890c7db63a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933323"
---
# <a name="ftp-ascii"></a>ftp ascii

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイル転送の種類を ASCII に設定します。 **Ftp**コマンドでは、ascii (既定) とバイナリイメージファイル転送の両方がサポートされていますが、テキストファイルを転送するときは ascii を使用することをお勧めします。 ASCII モードでは、ネットワークの標準の文字セットとの間の文字変換が実行されます。 たとえば、行末の文字は、対象のオペレーティングシステムに基づいて必要に応じて変換されます。

## <a name="syntax"></a>構文

```
ascii
```

### <a name="examples"></a>例

ファイル転送の種類を ASCII に設定するには、次のように入力します。

```
ascii
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ftp バイナリコマンド](ftp-binary.md)

- [追加の FTP ガイダンス](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
