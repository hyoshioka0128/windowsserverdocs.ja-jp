---
title: bitsadmin getreplyfilename
description: '**Bitsadmin getreplyfilename**の Windows コマンドに関するトピックでは、ジョブのサーバーアップロード応答を含むファイルのパスを取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 85447184-1732-4816-a365-2e3599551bf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 541a6e60d641405b5da2e65fecbbbe87468c8702
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850495"
---
# <a name="bitsadmin-getreplyfilename"></a>bitsadmin getreplyfilename

ジョブのサーバーアップロード応答を含むファイルのパスを取得します。

> [!NOTE]
> このコマンドは、BITS 1.2 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /getreplyfilename <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |


## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブのアップロード応答ファイル名を取得します。

```
C:\>bitsadmin /getreplyfilename myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)