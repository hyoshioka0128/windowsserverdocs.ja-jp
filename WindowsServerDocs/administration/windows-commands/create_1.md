---
title: 作成
description: 現在のコンテキストとオプションの設定を使用して、シャドウコピーの作成プロセスを開始する Windows コマンドトピックを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 837aa449-9b60-41ae-9ef1-ef67af6e5918
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d29285517ca678a15828079c95663fc4d501eaf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846835"
---
# <a name="create"></a>作成

現在のコンテキストとオプションの設定を使用して、シャドウコピーの作成プロセスを開始します。 シャドウコピーセットに少なくとも1つのボリュームが必要です。

## <a name="syntax"></a>構文

```
create
```

## <a name="remarks"></a>コメント

-   **Create**コマンドを使用する前に、 **[ボリュームの追加]** コマンドでボリュームを少なくとも1つ追加する必要があります。
-   **[バックアップの開始]** コマンドを使用すると、コピーバックアップではなく完全バックアップを指定できます。
-   **Create**コマンドを実行した後、 **exec**コマンドを使用して、シャドウコピーからバックアップ用の複製スクリプトを実行できます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)