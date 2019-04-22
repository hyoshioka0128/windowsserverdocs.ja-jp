---
title: 復元をシミュレートします。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d883d94c-3cb1-4848-9d74-1b4378044b31
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 09b626939c13d4e38a983435b45d8c47ee2b93a4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817253"
---
# <a name="simulate-restore"></a>復元をシミュレートします。



発行することがなく、コンピューター上の復元のセッション内のライターをテスト **復元前** または **PostRestore** ライターへのイベントです。

## <a name="syntax"></a>構文

```
simulate restore
```

## <a name="remarks"></a>注釈

-   **復元をシミュレート** ライタ搭載の復元を成功させるために動作しているかどうかをテストするために使用します。
-   使用する前に **リストアをシミュレート**, を使用して、DiskShadow メタデータ ファイルを読み込む必要があります、 **メタデータの読み込み** コマンドです。 これには、選択されているライターと復元のコンポーネントが読み込まれます。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)