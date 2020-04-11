---
title: dfsutil
description: Windows コマンドに関するトピック。 dfsutil は、DFS 名前空間、サーバー、およびクライアントを管理します。 dfsutil コマンドでは、ほとんどのコマンドについて説明するように、更新された DFS 名前空間の用語を使用して、元の分散ファイルシステム用語を使用します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef5093a4-0d24-4b21-9d04-59933ad98e2c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 47d468ee122dc78cc880f4a9bc0705354e0b5214
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122554"
---
# <a name="dfsutil"></a>dfsutil

>適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Dfsutil コマンドは、DFS 名前空間、サーバー、およびクライアントを管理します。

>[!NOTE]
>**DFS 名前空間の PowerShell モジュール**では、一部の dfsutil パラメーターの置換が提供されますが、他のパラメーターでは dfsutil を使用する必要があります。 更新された PowerShell に関する詳細については、「 [DFSN](https://docs.microsoft.com/powershell/module/dfsn/?view=win10-ps)」を参照してください。

## <a name="parameters-available-in-powershell"></a>PowerShell で使用可能なパラメーター

PowerShell から次のパラメーターを使用できます。

| パラメーター | 説明 |
| --------- | ----------- |
| root | 名前空間のルートを表示、作成、削除、インポート、エクスポートします。 |
| link | フォルダー (リンク) を表示、作成、削除、または移動します。 |
| target | フォルダーターゲットまたは名前空間サーバーを表示、作成、削除します。 |
| property | フォルダーターゲットまたは名前空間サーバーを表示または変更します。 |
| &lt;サーバー&gt; | 名前空間の構成を表示または変更します。 |
| domain | ドメイン内のすべてのドメインベースの名前空間を表示します。 |

## <a name="parameters-only-available-in-dfsutil"></a>パラメーターは、dfsutil でのみ使用できます。

次のパラメーターは、dfsutil からのみ使用できます。

| パラメーター | 説明 |
| --------- | ----------- |
| クライアント | クライアント情報またはレジストリキーを表示または変更します。 |
| 斜め | 診断を実行するか、dfs dirs/dfspath を表示します。 |
| キャッシュ | クライアントキャッシュを表示またはフラッシュします。 |

これらの各コマンドの詳細については、DFS 名前空間の管理ツールがインストールされているサーバーでコマンドプロンプトを開き、「`dfsutil client /?`、`dfsutil diag /?`、または `dfsutil cache /?`」と入力します。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)