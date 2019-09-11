---
title: GitHub で使用するための一般的な Git Bash コマンド
description: GitHub を使用するときに、Git Bash で最もよく使用されるコマンドの一覧です。
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: 4ce5d4d8ce382e9ba421c20595715ec473cca241
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70864997"
---
# <a name="common-git-bash-commands"></a>一般的な Git Bash コマンド

これらは、コンテンツの作成と編集プロセスで使用するタイミングに基づいて、Git Bash で最も使用されているコマンドの一部です。

## <a name="master-branch-related"></a>Master ブランチ関連

新しいブランチのベースとして常に master を使用する必要があります。

| Command | 説明 |
|---------|-------------|
| `git checkout master` | 他のブランチからマスターに切り替える |
| `git pull upstream master` | 運用リポジトリからマスターのローカルコピーを更新する |

## <a name="branch-related"></a>ブランチ関連

| Command | 説明 |
|---------|-------------|
| `git branch` | 既存のブランチを見る |
| `git checkout -B <name-of-branch>` | 新しいブランチを作成する |
| `git checkout <name-of-branch>` | 別の分岐に変更する |
| `git status` | ブランチで何が起こっているかを確認する |
| `git branch -D <name-of-branch>` | 既存のブランチを削除します (存在していないことを確認します)。 |

## <a name="check-in-related-done-as-a-group-in-order"></a>チェックインに関連する (グループとして実行される)

| Command | 説明 |
|---------|-------------|
| `git add --all` | 作業内容を保存したら、それを分岐に追加します。 |
| `git commit -m “public comment, including quotes”` | ブランチへの変更をコミットする |
| `git pull upstream master` | 運用リポジトリからマスターのローカルコピーを更新する |
| `git push origin <name-of-branch>` | ローカルブランチのリモートバージョンにプッシュする |