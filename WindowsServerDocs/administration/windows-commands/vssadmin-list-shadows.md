---
title: Vssadmin リストの影
description: Vssadmin list shadows コマンドの説明です。
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: d3616902fa0b971969e5e906d6dbb200c633d15a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891800"
---
# <a name="vssadmin-list-shadows"></a>Vssadmin リストの影

> 適用対象: Windows 10、Windows 8.1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

指定したボリュームの既存のシャドウコピーをすべて一覧表示します。 パラメーターを指定せずにこのコマンドを使用すると、コンピューター上のすべてのボリュームシャドウコピーが、**シャドウコピーセット**によって指定された順序で表示されます。

## <a name="syntax"></a>構文

```PowerShell
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---|---|
|/for =\<ForVolumeSpec>|シャドウコピーが表示されるボリュームを指定します。|
|/シャドウ =\<ShadowID>|ShadowID によって指定されたシャドウコピーの一覧を表示します。 シャドウコピー ID を取得するには、 **vssadmin list shadows**コマンドを使用します。 シャドウコピー ID を入力するときは、次の形式を使用します。各*X*は16進文字を表します。<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX-XXXX-XXXX-XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|

## <a name="additional-references"></a>その他の参照情報

* [コマンドライン構文のキー](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)
