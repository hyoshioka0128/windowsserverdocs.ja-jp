---
title: Vssadmin delete の影
description: Vssadmin delete shadows コマンドの説明です。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: e18823c5c030aa1a7b8f032f820e415f36fd7827
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720270"
---
# <a name="vssadmin-delete-shadows"></a>Vssadmin delete の影

> 適用対象: Windows 10、Windows 8.1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

指定されたボリュームのシャドウコピーを削除します。

## <a name="syntax"></a>構文

```PowerShell
vssadmin delete shadows /for=<ForVolumeSpec> [/oldest | /all | /shadow=<ShadowID>] [/quiet]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---|---|
|/for =\<ForVolumeSpec>|削除するボリュームのシャドウコピーを指定します。|
|/最も古い|最も古いシャドウコピーだけを削除します。|
|/all|指定されたボリュームのシャドウコピーをすべて削除します。|
|/shadow =\<ShadowID>|ShadowID によって指定されたシャドウコピーを削除します。 シャドウコピー ID を取得するには、 **vssadmin list shadows**コマンドを使用します。 シャドウコピー ID を入力するときは、次の形式を使用します。各*X*は16進文字を表します。<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX-XXXX-XXXX-XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|
|/quiet|コマンドの実行中にメッセージを表示しないように指定します。|

## <a name="remarks"></a>Remarks

シャドウコピーを削除できるのは、クライアントからアクセス可能な型の場合のみです。

## <a name="examples"></a>例

ボリューム C の最も古いシャドウコピーを削除するには、次のコマンドを入力します。

```PowerShell
vssadmin delete shadows /for=c: /oldest
```

## <a name="additional-references"></a>その他の参照情報

* [コマンドライン構文のキー](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)
* [Vssadmin list shadows](vssadmin-list-shadows.md)