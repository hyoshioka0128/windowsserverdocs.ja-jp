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
ms.openlocfilehash: 30415bc85fd8a4a4804946a3d4a168d6a7d1433a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845585"
---
# <a name="dfsutil"></a>dfsutil

>適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Dfsutil コマンドは、DFS 名前空間、サーバー、およびクライアントを管理します。 多くの場合、代わりに新しい DFS 名前空間の PowerShell コマンドレットを使用できますが、dfsutil を必要とするコマンドがいくつかあります。

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