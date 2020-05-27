---
title: Scwcmd
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 188ae881-c7d4-4a7a-b967-8fdc79f5f345
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a8c002aa735b188fdd9ad75b0db7dbe06053516
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821162"
---
# <a name="scwcmd"></a>Scwcmd

> 適用対象: Windows Server 2012 R2、Windows Server 2012

セキュリティ構成ウィザード (SCW) に含まれている Scwcmd コマンドラインツールを使用して、次のタスクを実行できます。
-   SCW で生成されたポリシーを使用して 1 つまたは複数のサーバーを構成します。
-   SCW で生成されたポリシーを使用して 1 つまたは複数のサーバーを分析します。
-   HTML 形式では、分析結果を表示します。
-   SCW ポリシーをロールバックします。
-   グループ ポリシーによってサポートされているネイティブのファイル、SCW で生成されたポリシーに変換します。
-   SCW でセキュリティの構成データベースの拡張機能を登録します。

使用すると **scwcmd** 構成、分析、またはロールバックするには、リモート サーバー上 SCW のリモート サーバー上のポリシーをインストールします。

## <a name="syntax"></a>構文

```
scwcmd <command> [<subcommand>]
```

### <a name="parameters"></a>パラメーター

|サブコマンド|Description|
|----------|-----------|
|/analyze|コンピューターが、ポリシーに準拠しているかどうかを判断します。</br>参照してください [Scwcmd: 分析](scwcmd-analyze.md) 構文とオプションについてです。|
|/configure|SCW で生成されたセキュリティ ポリシーをコンピューターに適用されます。</br>参照してください [Scwcmd: 構成](scwcmd-configure.md) 構文とオプションについてです。|
|/register|拡張または役割、タスク、サービス、またはポートの定義を含むセキュリティの構成データベース ファイルを登録することにより、SCW のセキュリティ構成データベースをカスタマイズします。</br>参照してください [Scwcmd: 登録](scwcmd-register.md) 構文とオプションについてです。|
|/rollback|使用可能な最新のロールバックのポリシーを適用し、そのロールバックのポリシーを削除します。</br>参照してください [Scwcmd: ロールバック](scwcmd-rollback.md) 構文とオプションについてです。|
|/transform|Active Directory ドメイン サービスに新しいグループ ポリシー オブジェクト (GPO) に SCW を使用して、生成されたセキュリティ ポリシー ファイルを変換します。</br>参照してください [Scwcmd: 変換](scwcmd-transform.md) 構文とオプションです。|
|/view|指定した .xsl 変換を使用して .xml ファイルを表示します。</br>参照してください [Scwcmd: ビュー](scwcmd-view.md) 構文とオプションについてです。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
