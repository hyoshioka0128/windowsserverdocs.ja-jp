---
title: GitHub で使用するための一般的な Git Bash コマンド
description: GitHub を使用する場合、Git Bash で最もよく使用されるコマンドの一部の一覧。
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: 210acaf2b7911892bcfd81b6bbe1975f141308a1
ms.sourcegitcommit: 7e54a1bcd31cd2c6b18fd1f21b03f5cfb6165bf3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65461687"
---
# <a name="common-git-bash-commands"></a>一般的な Git Bash コマンド

これらは、Git Bash をコンテンツの作成に使用するときに基づいており、編集プロセスで最も使用頻度のコマンドの一部です。

## <a name="master-branch-related"></a>マスター ブランチに関連します。

いずれかの新しい分岐のベースとしてマスターを常に使用する必要があります。

| コマンド | 説明 |
|---------|-------------|
| `git checkout master` | 他のブランチからマスターを切り替える |
| `git pull upstream master` | 運用環境のリポジトリから master のローカル コピーを更新します。 |

## <a name="branch-related"></a>ブランチに関連します。

| コマンド | 説明 |
|---------|-------------|
| `git branch` | 既存の分岐を参照してください。 |
| `git checkout -B <name-of-branch>` | 新しいブランチを作成します。 |
| `git checkout <name-of-branch>` | 別の分岐に変更します。 |
| `git status` | 分岐で何が起こってを確認します。 |
| `git branch -D <name-of-branch>` | (これではないことを確認するため)、既存のブランチを削除します。 |

## <a name="check-in-related-done-as-a-group-in-order"></a>関連チェックで (実行の順序でのグループ)

| コマンド | 説明 |
|---------|-------------|
| `git add --all` | 作業内容を保存した後、ブランチに追加します。 |
| `git commit -m “public comment, including quotes”` | 独自のブランチに変更をコミットします。 |
| `git pull upstream master` | 運用環境のリポジトリから master のローカル コピーを更新します。 |
| `git push origin <name-of-branch>` | リモートのバージョンのローカル ブランチにプッシュします。 |