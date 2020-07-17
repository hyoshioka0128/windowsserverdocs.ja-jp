---
title: create
description: 現在のコンテキストとオプションの設定を使用して、シャドウコピーの作成プロセスを開始する create のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 837aa449-9b60-41ae-9ef1-ef67af6e5918
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cfddbebd5744d8cd222d67e46690ce8b5d2e0fde
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716835"
---
# <a name="create"></a>create

現在のコンテキストとオプションの設定を使用して、シャドウコピーの作成プロセスを開始します。 シャドウコピーセットに少なくとも1つのボリュームが必要です。

## <a name="syntax"></a>構文

```
create
```

## <a name="remarks"></a>Remarks

-   **Create**コマンドを使用する前に、[**ボリュームの追加**] コマンドでボリュームを少なくとも1つ追加する必要があります。
-   [**バックアップの開始**] コマンドを使用すると、コピーバックアップではなく完全バックアップを指定できます。
-   **Create**コマンドを実行した後、 **exec**コマンドを使用して、シャドウコピーからバックアップ用の複製スクリプトを実行できます。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)