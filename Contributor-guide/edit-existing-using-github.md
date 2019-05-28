---
title: GitHub および Visual Studio Code を使用して、既存の Windows Server の記事を編集します。
description: 既存 Windows Server 関連の記事は、GitHub および Visual Studio Code を使用して、マイクロソフトの従業員としてを編集する方法。
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: d2d95cc28089ceb74bf9690f6bd78611e7d9a27a
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624580"
---
# <a name="edit-an-existing-windows-server-article-using-github-and-visual-studio-code"></a>GitHub および Visual Studio Code を使用して、既存の Windows Server の記事を編集します。

Windows Server の技術的なコンテンツを保持する 2 つの別々 の場所があります。 パブリックの場所のいずれか (windowsserverdocs)、もう一方はプライベート (windowsserverdocs pr)。 ユーザーに協力する位置を決定します。

- **私はマイクロソフトの従業員です。** マイクロソフトの従業員としてを実行しているに基づいてのオプションがあります。

    - **新しい記事を作成します。** 新しい記事を作成するには、作成する必要があり、GitHub アカウントとツールを設定すると、フォークと複製 windowsserverdocs pr リポジトリでは、独自のリモート ブランチを設定、アーティクルを作成および最後に、新しいプル要求の承認および発行を作成します。 手順については、これらの手順を利用できる、 [GitHub および Visual Studio Code を使用して新しい Windows Server の記事を作成](create-new-using-github.md)記事。

    - **既存のアーティクルに大きな変化を作成します。** 既存の記事に大幅な変更を加えるには、この記事の手順に従います。

    - **既存の記事に軽微な変更を行います。** 既存の記事に軽微な変更するには、手順を利用できる、 [web ブラウザーと GitHub を使用して既存の Windows Server の記事を更新](github-browser-updates.md)記事。

- **Microsoft の従業員わかりません。** Microsoft 以外の従業員としては、パブリックな場所に協力する必要があります。 その方法については、次を参照してください。、 [Windows Server 技術ドキュメントに貢献する](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md)記事。

## <a name="switch-your-repo-and-create-a-new-branch"></a>リポジトリを切り替えるし、新しいブランチを作成

既存の記事を編集するこれらの手順に従います。

### <a name="create-a-new-branch-and-locate-the-file-you-want-to-update"></a>新しいブランチを作成し、更新するファイルを見つけます

コンテンツに作業を開始する前に、まず windowsserverdocs pr リポジトリに変更してし更新する記事を検索する必要があります。

#### <a name="to-create-a-new-branch-in-git-bash"></a>Git Bash で新しいブランチを作成するには

- Git Bash を開き、(1 つずつ) のコマンドを入力します。

    ```markdown
    cd windowsserverdocs-pr

    git checkout –B <name_of_your_new_branch>

    git push origin <name_of_your_new_branch>
    ```

    >[!Note]
    >後でもう一度検索できるように独自のブランチを何か明らかで、一意な名前を強くお勧めします。

    コマンドが完了すると、新たなブランチであるし、ファイルを編集する準備が完了します。

#### <a name="to-locate-your-article-and-make-your-edits"></a>あなたの記事を見つけて、編集を行う

1. Visual Studio Code を開きに移動**ファイル**、**フォルダーを開く**、し編集するアーティクルがあるフォルダーの GitHub の場所に移動します。

2. **エクスプ ローラー**ウィンドウで、ファイルを選択します。

3. ページで、情報を更新し、**ファイル** > **保存**します。

### <a name="preview-your-text"></a>テキストをプレビューします。

テキストを更新した後は、正しく表示されるかどうかを確認する変更をプレビューする必要があります。

#### <a name="to-preview-your-text"></a>テキストをプレビューするには

1. Visual Studio Code でのいずれかを選択、**プレビュー**右上隅のボタン。

    ![プレビュー ボタン アイコン](media/create-new-using-github/preview-button-full-page.png):コンテンツのページ全体のプレビューに切り替えます。

    ![プレビュー ボタン アイコン](media/create-new-using-github/preview-button-side-by-side.png):サイド バイ サイドでの作業ページの横にある [プレビュー] ページが開きます。

2. 記事では、期待を検索することを確認します。

    適切に表示されることを確認したら、変更をコミットし、パブリケーションのプル要求を作成できます。

### <a name="commit-your-changes"></a>変更をコミットします。

テキストが適切なことを確認したら、リポジトリのローカル バージョンに変更をコミットすることができます。

#### <a name="to-commit-your-changes"></a>変更をコミットします。

- Git Bash を開き、コマンド (省略可能なタグを削除して、一度に 1 つずつ) を入力します。

    ```markdown
    OPTIONAL: git status

    git add .

    git commit -m “public comment about what change is”

    OPTIONAL: git pull upstream master

    git push origin <name_of_your_new_branch>

    ```

    省略可能な git status コマンドは、このコミットの一部として変更されたファイルを示します。 省略可能な git では、アップ ストリームのマスター プル ダウン プライマリ マスター コンテンツをローカル コンテンツを同期 MicrosoftDocs マスター ブランチから最新のコンテンツの変更をプルします。 これにより、PR の段階に到達する前に修正できるようにを事前に潜在的なマージの競合を表示します。

### <a name="submit-a-pull-request-for-review-and-publication"></a>レビューとパブリケーションのプル要求を送信します。

更新が完了したら、お使いのライターから承認を取得する必要があります (この時間を許可する) パブリケーション。

#### <a name="to-submit-your-pull-request"></a>プル要求を送信するには

1. 移動して https://github.com/MicrosoftDocs/windowsserverdocs-prを選択し、**プル要求**タブ。

2. **レビュー担当者**右側のペインの領域は、歯車アイコンを選択し、入力、 _windowsservercontent_エイリアスを確認します。

    メンバー、 _windowsservercontent_エイリアスは変更内容を確認または発生することがマージ前に変更する必要がありますのようなことについてのコメントを追加します。

3. 型 **#sign オフ**コメントに、レビュー担当者が認識できるようにする入稿のレビューおよび発行の両方。 **#Sign オフ**コメント。

    - プル要求からのラベルを更新**do not-マージ**に**マージの準備完了に**します。

    - エイリアスとライターのコンテンツのレビューする準備ができたことを知ることができます。

    - により、管理者があること、承認後、コンテンツ準備 go live です。

    >[!Important]
    >#Sign からコメントを追加した後、windowsservercontent チームのメンバーは、テキストを確認し、プッシュが次に出て行くようにをマスターにスケジュールされたライブ (10時 30分 am と平日の午後 3時 30分) に発行します。
    >
    >PR に最終コメントとして #sign を追加しないでください場合、でも、コンテンツはマスターにプッシュされることがなく、キューに残りますが、最終的にライブにします。

## <a name="related-information"></a>関連情報

GitHub と markdown の言語の詳細についてを参照してください。

### <a name="git-concepts"></a>Git の概念

- [GitHub ガイド-Git ハンドブックの概要](https://guides.github.com/introduction/git-handbook/)

- [プロジェクトの GitHub ガイド フォーク](https://guides.github.com/activities/forking/)

- [GitHub ガイドについて、GitHub のフロー](https://guides.github.com/introduction/flow/)

- [Git のブランチ機能について説明します。](https://learngitbranching.js.org/ (visual 学習器に適しています。))

### <a name="markdown"></a>Markdown

- [内部の markdown ガイダンス](https://review.docs.microsoft.com/help/contribute/markdown-reference?branch=master)

- [外部、GitHub のチュートリアル](https://www.markdowntutorial.com/)