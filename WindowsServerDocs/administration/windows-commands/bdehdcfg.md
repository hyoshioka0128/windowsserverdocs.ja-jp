---
title: bdehdcfg
description: BitLocker ドライブ暗号化に必要なパーティションをハードドライブに準備する bdehdcfg コマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4c92cd74-188e-4fec-b7c4-fe4e8903e032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a8b926459f2d1fb96b9a48910c163eb9aaab02c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923350"
---
# <a name="bdehdcfg"></a>bdehdcfg

BitLocker ドライブ暗号化に必要なパーティションを使用してハードドライブを準備します。 BitLocker セットアップには、必要に応じてドライブを準備および再パーティションする機能が含まれているため、Windows 7 のほとんどのインストールでこのツールを使用する必要はありません。

> [!WARNING]
> **コンピューターの構成 \ 管理用テンプレート \Windows コンポーネント \Bitlocker ドライブ暗号化 \ 固定データドライブ**にある [グループポリシー **BitLocker で保護されていない固定ドライブへの書き込みアクセスを拒否する**] 設定との間に既知の競合があります。
>
>このポリシー設定を有効にしたときにコンピューターで bdehdcfg が実行されている場合は、次の問題が発生する可能性があります。
>
>- ドライブを圧縮してシステムドライブを作成しようとすると、ドライブサイズが正常に縮小され、未加工のパーティションが作成されます。 ただし、初期化されていないパーティションはフォーマットされていません。 次のエラーメッセージが表示されます。新しいアクティブドライブはフォーマットできません。 BitLocker 用にドライブを手動で準備することが必要になる場合があります。
>
>- 未割り当て領域を使用してシステムドライブを作成しようとすると、未加工のパーティションが作成されます。 ただし、初期化されていないパーティションはフォーマットされていません。 次のエラーメッセージが表示されます。新しいアクティブドライブはフォーマットできません。 BitLocker 用にドライブを手動で準備することが必要になる場合があります。
>
>- 既存のドライブをシステムドライブにマージしようとすると、システムドライブを作成するために必要なブートファイルがターゲットドライブにコピーされません。 次のエラーメッセージが表示されます: BitLocker セットアップでブートファイルをコピーできませんでした。 BitLocker 用にドライブを手動で準備することが必要になる場合があります。
>
>- このポリシー設定を適用する場合、ドライブは保護されているため、ハードドライブを再パーティション分割することはできません。 組織内のコンピューターを以前のバージョンの Windows からアップグレードする場合に、それらのコンピューターに1つのパーティションが構成されている場合は、そのコンピューターにポリシー設定を適用する前に、必要な BitLocker システムパーティションを作成する必要があります。

## <a name="syntax"></a>構文

```
bdehdcfg [–driveinfo <drive_letter>] [-target {default|unallocated|<drive_letter> shrink|<drive_letter> merge}] [–newdriveletter] [–size <size_in_mb>] [-quiet]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- |----------- |
| [bdehdcfg: driveinfo](bdehdcfg-driveinfo.md) | ドライブ文字、合計サイズ、最大空き領域、および指定されたドライブ上のパーティションのパーティション特性が表示されます。 有効なパーティションだけが一覧表示されます。 4つのプライマリパーティションまたは拡張パーティションが既に存在する場合、未割り当ての領域は表示されません。 |
| [bdehdcfg: ターゲット](bdehdcfg-target.md) | システムドライブとして使用するドライブの部分を定義し、その部分をアクティブにします。 |
| [bdehdcfg: newdriveletter](bdehdcfg-newdriveletter.md) | システムドライブとして使用されるドライブの部分に新しいドライブ文字を割り当てます。 |
| [bdehdcfg: サイズ](bdehdcfg-size.md) | 新しいシステムドライブを作成するときのシステムパーティションのサイズを決定します。 |
| [bdehdcfg: quiet](bdehdcfg-quiet.md) | コマンドラインインターフェイスにすべてのアクションとエラーが表示されないようにします。 bdehdcfg は、その後のドライブの準備中に発生する可能性のある Yes/No プロンプトに対して、Yes の答えを使用するように指示します。 |
| [bdehdcfg: 再起動](bdehdcfg-restart.md) | ドライブの準備が完了した後で、コンピューターを再起動するように指示します。 |
| /? | コマンド プロンプトでヘルプを表示します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
