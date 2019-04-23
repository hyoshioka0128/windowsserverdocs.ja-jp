---
title: Scwcmd
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 188ae881-c7d4-4a7a-b967-8fdc79f5f345
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 19d631f97c194a78819491f32955e391d3be5a70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883883"
---
# <a name="scwcmd"></a>Scwcmd

> 適用先:Windows Server 2012 R2、Windows Server 2012

次のタスクを実行するセキュリティ構成ウィザード (SCW) に含まれている Scwcmd.exe コマンド ライン ツールを使用できます。
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

## <a name="parameters"></a>パラメーター

|サブコマンド|説明|
|----------|-----------|
|/analyze|コンピューターが、ポリシーに準拠しているかどうかを判断します。</br>参照してください [Scwcmd: 分析](scwcmd-analyze.md) 構文とオプションについてです。|
|/configure|SCW で生成されたセキュリティ ポリシーをコンピューターに適用されます。</br>参照してください [Scwcmd: 構成](scwcmd-configure.md) 構文とオプションについてです。|
|/register|拡張または役割、タスク、サービス、またはポートの定義を含むセキュリティの構成データベース ファイルを登録することにより、SCW のセキュリティ構成データベースをカスタマイズします。</br>参照してください [Scwcmd: 登録](scwcmd-register.md) 構文とオプションについてです。|
|/rollback|使用可能な最新のロールバックのポリシーを適用し、そのロールバックのポリシーを削除します。</br>参照してください [Scwcmd: ロールバック](scwcmd-rollback.md) 構文とオプションについてです。|
|/transform|Active Directory ドメイン サービスに新しいグループ ポリシー オブジェクト (GPO) に SCW を使用して、生成されたセキュリティ ポリシー ファイルを変換します。</br>参照してください [Scwcmd: 変換](scwcmd-transform.md) 構文とオプションです。|
|/view|指定した .xsl 変換を使用して .xml ファイルを表示します。</br>参照してください [Scwcmd: ビュー](scwcmd-view.md) 構文とオプションについてです。|
|/?|コマンド プロンプトにヘルプを表示します。|

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
