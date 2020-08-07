---
title: dfsutil
description: DFS 名前空間、サーバー、およびクライアントを管理する dfsutil コマンドのリファレンス記事です。
ms.topic: article
ms.assetid: ef5093a4-0d24-4b21-9d04-59933ad98e2c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f31af9f557271182980a367ebf5e2233788fcc31
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891026"
---
# <a name="dfsutil"></a>dfsutil

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Dfsutil コマンドは、DFS 名前空間、サーバー、およびクライアントを管理します。

## <a name="functionality-available-in-powershell"></a>PowerShell で使用可能な機能

[DFSN](/powershell/module/dfsn/?view=win10-ps) PowerShell モジュールは、次の dfsutil パラメーターと同等の機能を提供します。

| パラメーター | 説明 |
| --------- | ----------- |
| root | 名前空間のルートを表示、作成、削除、インポート、エクスポートします。 |
| link | フォルダー (リンク) を表示、作成、削除、または移動します。 |
| ターゲット (target) | フォルダーターゲットまたは名前空間サーバーを表示、作成、削除します。 |
| property | フォルダーターゲットまたは名前空間サーバーを表示または変更します。 |
| server | 名前空間の構成を表示または変更します。 |
| domain | ドメイン内のすべてのドメインベースの名前空間を表示します。 |

## <a name="functionality-available-only-in-dfsutil"></a>Dfsutil でのみ使用できる機能

次の機能は、dfsutil パラメーターとしてのみ使用できます。

| パラメーター | 説明 |
| --------- | ----------- |
| クライアント | クライアント情報またはレジストリキーを表示または変更します。 |
| 斜め | 診断を実行するか、dfs dirs/dfspath を表示します。 |
| cache | クライアントキャッシュを表示またはフラッシュします。 |

これらの各コマンドの詳細については、DFS 名前空間の管理ツールがインストールされているサーバーでコマンドプロンプトを開き、「」、「」、または「」と入力し `dfsutil client /?` `dfsutil diag /?` `dfsutil cache /?` ます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
