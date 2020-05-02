---
title: セットのメタデータ
description: 設定メタデータのリファレンストピックでは、シャドウコピーをあるコンピューターから別のコンピューターに転送するために使用するシャドウ作成メタデータファイルの名前と場所を設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 67e6f60a-b42a-451a-95cf-b22ace7d50c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 683e54a7efc072d8709d6257771ba6bc5bde206e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721913"
---
# <a name="set-metadata"></a>セットのメタデータ

シャドウ コピーを別の 1 台のコンピューターに転送するために使用したシャドウの作成のメタデータ ファイルの場所と名前を設定します。 パラメーターを指定せずに使用する場合 **メタデータ設定** コマンド プロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
set metadata [<Drive>:][<Path>]<MetaData.cab>
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|[\<ドライブ>:][<Path>]|メタデータ ファイルを作成する場所を指定します。|
|\<メタデータ .cab>|シャドウの作成のメタデータを格納する cab ファイルの名前を指定します。|

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)