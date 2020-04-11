---
title: bitsadmin reset
description: '**Bitsadmin reset**の Windows コマンドに関するトピックでは、現在のユーザーが所有している転送キュー内のすべてのジョブを取り消します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0e4f9d1d-072c-493f-8d7a-f6d713c3ef29
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b73bd3b9c66b24330a0f9444836b9c8bd1730722
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123080"
---
# <a name="bitsadmin-reset"></a>bitsadmin reset

現在のユーザーが所有している転送キュー内のすべてのジョブをキャンセルします。 >、ローカルシステムによって作成されたジョブをリセットすることはできません。 代わりに、管理者である必要があります。また、タスクスケジューラを使用して、ローカルシステムの資格情報を使用して、このコマンドをタスクとしてスケジュールする必要があります。

> [!NOTE]
> BITSAdmin 1.5 以前では、管理者特権を持っている場合、/reset スイッチによってキュー内のすべてのジョブが取り消されます。 また、/allusers オプションはサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /reset [/allusers]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| /allusers | 省略可。 現在のユーザーが所有しているキュー内のすべてのジョブをキャンセルします。 このパラメーターを使用するには、管理者特権が必要です。 |

## <a name="examples"></a>例

次の例では、現在のユーザーの転送キューにあるすべてのジョブを取り消します。

```
C:\>bitsadmin /reset
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)