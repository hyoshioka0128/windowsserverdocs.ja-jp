---
title: Vssadmin delete シャドウ
description: Vssadmin delete shadows コマンドの説明。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 83074017e4ae412cf0aec654f6ab5901ad8039e2
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "63706627"
---
# <a name="vssadmin-delete-shadows"></a>Vssadmin delete シャドウ

>適用対象:Windows 10、Windows 8.1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

指定したボリュームのシャドウ コピーを削除します。

## <a name="syntax"></a>構文

```PowerShell
vssadmin delete shadows /for=<ForVolumeSpec> [/oldest | /all | /shadow=<ShadowID>] [/quiet]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---|---|
|/=\<指定せず >|ボリュームのシャドウ コピーが削除されますを指定します。|
|最も古い/|最も古いシャドウ コピーのみを削除します。|
|/all|指定したボリュームのシャドウ コピーをすべて削除します。|
|/shadow=\<ShadowID>|ShadowID で指定されたシャドウ コピーを削除します。 シャドウ コピー ID を取得する、 **vssadmin 一覧 shadows**コマンド。 シャドウ コピー ID を入力すると、次の形式を使用して、各*X* 16 進数の文字を表します。<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|
|/quiet|コマンドが実行中にメッセージが表示されないよう指定します。|

## <a name="remarks"></a>注釈

シャドウ コピーは、クライアントからアクセス可能な型でのみ削除できます。

## <a name="examples"></a>例

C のボリュームの最も古いシャドウ コピーを削除するには、このコマンドを入力します。

```PowerShell
vssadmin delete shadows /for=c: /oldest
```

## <a name="additional-references"></a>その他の参照情報

* [コマンドライン構文キー](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [vssadmin](vssadmin.md)
* [Vssadmin 一覧の影](vssadmin-list-shadows.md)