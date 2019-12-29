---
title: wbadmin delete カタログ
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3041407-4577-4716-a39f-2c8ab48818d1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 58b8bc6043437755675af28c084257ba0d8b176d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362533"
---
# <a name="wbadmin-delete-catalog"></a>wbadmin delete カタログ



ローカル コンピューターに格納されているバックアップ カタログを削除します。 このコマンドを使用してバックアップ カタログが壊れているを使用してそれを復元することはできませんと **wbadmin restore catalog**します。

このサブコマンドでバックアップ カタログを削除するには、メンバーである、 **バックアップ オペレーター** グループ、または **管理者** グループ、またはをされている必要が適切なアクセス許可を委任します。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、 **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします)。

## <a name="syntax"></a>構文

```
wbadmin delete catalog
[-quiet]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-通知の停止|ユーザーにプロンプトを表示せずにサブコマンドを実行します。|

## <a name="remarks"></a>コメント

コンピューターのバックアップ カタログを削除した場合の Windows Server バックアップ スナップインを使用してそのコンピューターで作成されたバックアップにアクセスすることができなきます。 この場合、別のバックアップ場所にアクセスする場合は、使用 **wbadmin restore catalog** をその場所からカタログのバックアップを復元します。 バックアップ カタログを削除した後は、新しいバックアップを作成する必要があります。

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBCatalog](https://technet.microsoft.com/library/jj902445.aspx)