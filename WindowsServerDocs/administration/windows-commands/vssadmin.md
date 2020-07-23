---
title: Vssadmin (英語の可能性あり)
description: Vssadmin コマンドの概要です。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: f3618841eb2f511323873d2ea962838f9ab777d0
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86954694"
---
# <a name="vssadmin"></a>Vssadmin (英語の可能性あり)

> 適用対象: Windows 10、Windows 8.1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

現在のボリュームシャドウコピーバックアップと、インストールされているすべてのシャドウコピーライターおよびプロバイダーを表示します。 次の表のコマンド名を選択して、コマンドの構文を確認します。

|コマンド|説明|可用性
|---|---|---
|[Vssadmin add shadowstorage](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc788051(v%3dws.11))|ボリュームシャドウコピーの記憶域の関連付けを追加します。| サーバーのみ
|[Vssadmin create shadow](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc788055(v%3dws.11))|新しいボリュームシャドウコピーを作成します。| サーバーのみ
|[Vssadmin delete の影](vssadmin-delete-shadows.md)|ボリュームシャドウコピーを削除します。| クライアントとサーバー
|[Vssadmin delete shadowstorage](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc785461(v%3dws.11))|ボリュームシャドウコピーの記憶域の関連付けを削除します。| サーバーのみ
|[Vssadmin list providers](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc788108(v%3dws.11))|登録済みのボリュームシャドウコピープロバイダーを一覧表示します。| クライアントとサーバー
|[Vssadmin list shadows](vssadmin-list-shadows.md)|既存のボリュームシャドウコピーを一覧表示します。| クライアントとサーバー
|[Vssadmin list shadowstorage](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc788045(v%3dws.11))|システム上のすべてのシャドウコピーの記憶域の関連付けを一覧表示します。| クライアントとサーバー
|[Vssadmin リストボリューム](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc788064(v%3dws.11))|シャドウコピーの対象となるボリュームを一覧表示します。| クライアントとサーバー
|[Vssadmin list writers](vssadmin-list-writers.md)|システム上のサブスクライブされているすべてのボリュームシャドウコピーライターの一覧を表示します。| クライアントとサーバー
|[Vssadmin resize shadowstorage](vssadmin-resize-shadowstorage.md)|シャドウコピーの記憶域の関連付けの最大サイズを変更します。| クライアントとサーバー
