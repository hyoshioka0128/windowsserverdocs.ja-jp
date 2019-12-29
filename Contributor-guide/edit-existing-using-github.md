---
title: GitHub と Visual Studio Code を使用した既存の Windows Server の記事の編集
description: GitHub と Visual Studio Code を使用して、Microsoft の従業員として、既存の Windows Server 関連記事を編集する方法について説明します。
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: d681d2fc2b69898e841932a95738b89515ffb51a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865083"
---
# <a name="edit-an-existing-windows-server-article-using-github-and-visual-studio-code"></a>GitHub と Visual Studio Code を使用した既存の Windows Server の記事の編集

Windows Server の技術コンテンツを保持する場所は2つあります。 一方の場所はパブリック (windowsserverdocs) で、もう一方はプライベート (windowsserverdocs-pr) です。 だれがどの場所に投稿するかを決定します。

- **私は Microsoft の従業員です。** Microsoft の従業員は、何をしようとしているかに応じて、オプションがあります。

    - **新しい記事を作成します。** 新しい記事を作成するには、GitHub アカウントとツールの作成と設定、windowsserverdocs-pr リポジトリのフォークと複製、リモート ブランチの設定、記事の作成をする必要があり、最後に承認および発行するための新しいプル要求を作成します。 これらの手順については、GitHub を使用した[新しい Windows Server の作成に関する記事と Visual Studio Code](create-new-using-github.md)に関する記事に記載されている手順に従ってください。

    - **既存の記事に大きな変更を加えます。** 既存の記事に大幅な変更を加えるには、この記事の手順に従ってください。

    - **既存のアーティクルに対して軽微な変更を行います。** 既存の記事に軽微な変更を加えるには、 [web ブラウザーと GitHub を使用した既存の Windows Server の更新に関する](github-browser-updates.md)記事に記載されている手順に従ってください。

- **Microsoft の従業員ではありません。** マイクロソフト以外の従業員は、公共の場所に投稿する必要があります。 その方法については、 [Windows Server のテクニカルドキュメントに](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md)関する記事を参照してください。

## <a name="switch-your-repo-and-create-a-new-branch"></a>リポジトリを切り替えて新しいブランチを作成する

既存の記事を編集するには、次の手順に従います。

### <a name="create-a-new-branch-and-locate-the-file-you-want-to-update"></a>新しいブランチを作成し、更新するファイルを指定します。

コンテンツの操作を開始する前に、まず windowsserverdocs-pr リポジトリに変更してから、更新するアーティクルを検索する必要があります。

#### <a name="to-create-a-new-branch-in-git-bash"></a>Git Bash で新しいブランチを作成するには

- Git Bash を開き、コマンド (一度に1つずつ) を入力します。

    ```markdown
    cd windowsserverdocs-pr

    git checkout –B <name_of_your_new_branch>

    git push origin <name_of_your_new_branch>
    ```

    >[!Note]
    >ブランチに明確で一意の名前を付けることを強くお勧めします。この場合、後でもう一度見つけることができます。

    コマンドが完了すると、新しいブランチに追加され、ファイルを編集できるようになります。

#### <a name="to-locate-your-article-and-make-your-edits"></a>記事を検索して編集を行うには

1. Visual Studio Code を開き、 **[ファイル]** 、 **[フォルダーを開く]** の順に選択してから、編集する記事があるフォルダーの GitHub の場所に移動します。

2. **[エクスプローラー]** ペインで、ファイルを選択します。

3. ページの情報を更新し、[**ファイル** > ] **[保存]** の順に選択します。

### <a name="preview-your-text"></a>テキストのプレビュー

テキストを更新した後は、変更内容をプレビューして、正しく表示されることを確認する必要があります。

#### <a name="to-preview-your-text"></a>テキストをプレビューするには

1. Visual Studio Code で、右上隅の**プレビュー**ボタンのいずれかを選択します。

    ![[プレビュー] ボタンアイコン](media/create-new-using-github/preview-button-full-page.png):コンテンツの全ページプレビューに切り替えます。

    ![[プレビュー] ボタンアイコン](media/create-new-using-github/preview-button-side-by-side.png):作業ページの横にあるプレビューページを横に並べて表示します。

2. 記事が期待どおりに表示されることを確認します。

    正しいことを確認したら、変更をコミットし、パブリケーションのプル要求を作成できます。

### <a name="commit-your-changes"></a>変更をコミットする

テキストが正しく表示されていることを確認したら、ローカルバージョンのリポジトリに変更をコミットできます。

#### <a name="to-commit-your-changes"></a>変更をコミットするには

- Git Bash を開き、コマンド (一度に1つずつ、オプションのタグを削除します) を入力します。

    ```markdown
    OPTIONAL: git status

    git add .

    git commit -m “public comment about what change is”

    OPTIONAL: git pull upstream master

    git push origin <name_of_your_new_branch>

    ```

    オプションの git status コマンドを実行すると、このコミットの一部として変更されたファイルが表示されます。 オプションの git pull 上流マスターは、Microsoft Docs master ブランチから最新のコンテンツ変更を取得し、ローカルコンテンツをプライマリマスターコンテンツと同期します。 これにより、潜在的なマージの競合を事前に示すことができます。これにより、PR ステージを開始する前に問題を修正できます。

### <a name="submit-a-pull-request-for-review-and-publication"></a>レビューおよび発行のためにプル要求を送信する

更新が完了したら、ライターから承認を取得する必要があります (このためにはしばらく時間がかかることがあります)。

#### <a name="to-submit-your-pull-request"></a>プル要求を送信するには

1. に https://github.com/MicrosoftDocs/windowsserverdocs-pr アクセスし、 **[プル要求]** タブを選択します。

2. 右側のウィンドウの **[レビュー担当者]** 領域で歯車アイコンを選択し、確認のために_windowsservercontent_エイリアスを入力します。

    _Windowsservercontent_エイリアスのメンバーは、変更内容を確認するか、マージを実行する前に変更する必要がある項目に関するコメントを追加します。

3. レビュー担当者がレビューと発行の両方でサインオフしていることを確認できるように、コメントに「 **#sign** 」と入力します。 **#Sign**のコメント:

    - プル要求のラベルを更新します。マージの**準備**ができ**ていません**。

    - コンテンツをレビューする準備ができたことを、エイリアスとライターに知らせます。

    - 承認後、コンテンツの準備ができたことを管理者に知らせます。

    >[!Important]
    >#Sign off コメントを追加すると、windowsservercontent チームのメンバーがテキストをレビューし、マスターにプッシュして、次にスケジュールされている発行先 (10: 30am、3: 5:30 平日) で作業を開始します。
    >
    >PR に最後のコメントとして #sign オフを追加していない場合、コンテンツは、マスターにプッシュされ、最終的にライブになることなく、キューに残ります。

## <a name="related-information"></a>関連情報

GitHub と markdown 言語の詳細については、以下を参照してください。

### <a name="git-concepts"></a>Git の概念

- [GitHub ガイド-Git ハンドブックの概要](https://guides.github.com/introduction/git-handbook/)

- [GitHub ガイド-プロジェクトのフォーク](https://guides.github.com/activities/forking/)

- [GitHub ガイド-GitHub フローについて](https://guides.github.com/introduction/flow/)

- [Git の分岐について学習]する(https://learngitbranching.js.org/ (視覚的な学習役に最適です。))

### <a name="markdown"></a>Markdown

- [Microsoft 社内 markdown のガイダンス](https://review.docs.microsoft.com/help/contribute/markdown-reference?branch=master)

- [外部、GitHub チュートリアル](https://www.markdowntutorial.com/)