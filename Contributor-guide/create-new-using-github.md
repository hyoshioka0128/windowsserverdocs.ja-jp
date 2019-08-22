---
title: GitHub と Visual Studio Code を使用して新しい Windows Server の記事を作成する
description: GitHub と Visual Studio Code を使用して、Microsoft の従業員として、Windows Server 関連の新しい記事を作成する方法について説明します。
author: eross-msft
ms.author: lizross
ms.date: 05/02/2019
ms.openlocfilehash: f5e7e3d0cd17c64175fddaaac73c12daa2c2a32c
ms.sourcegitcommit: ffd9c42374c7448deb5f53f7a865cb427b5e4e9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69887948"
---
# <a name="create-new-windows-server-articles-using-github-and-visual-studio-code"></a>GitHub と Visual Studio Code を使用して新しい Windows Server の記事を作成する

Windows Server の技術コンテンツを保持する場所は2つあります。 一方の場所はパブリック (windowsserverdocs) で、もう一方はプライベート (windowsserverdocs-pr) です。 だれがどの場所に投稿するかを決定します。

- **私は Microsoft の従業員です。** Microsoft の従業員は、何をしようとしているかに応じて、オプションがあります。

    - **新しい記事を作成します。** 新しい記事を作成するには、GitHub アカウントとツールを作成して設定し、windowsserverdocs-pr リポジトリをフォークして複製し、リモートブランチを設定して、記事を作成し、最後に承認と発行のための新しいプル要求を作成する必要があります。 この手順については、この記事の内容をお読みください。

    - **既存の記事に大きな変更を加えます。** 既存の記事に大幅な変更を加えるには、GitHub を使用した[既存の Windows Server の編集に関する記事と Visual Studio Code](edit-existing-using-github.md)の記事の手順に従ってください。

    - **既存のアーティクルに対して軽微な変更を行います。** 既存の記事に軽微な変更を加えるには、 [web ブラウザーと GitHub を使用した既存の Windows Server の更新に関する](github-browser-updates.md)記事に記載されている手順に従ってください。

- **Microsoft の従業員ではありません。** マイクロソフト以外の従業員は、公共の場所に投稿する必要があります。 その方法については、 [Windows Server のテクニカルドキュメントに](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md)関する記事を参照してください。

## <a name="prerequisites"></a>前提条件

リポジトリで作業を開始する前に、GitHub アカウントを作成および設定し、2要素認証を設定して、必要なすべてのツールをインストールして構成する必要があります。 これを既に行っている場合は、この記事の[「リポジトリのフォーク」セクション](#fork-the-repository)に進むことができます。

1. [GitHub アカウントとプロファイルを作成する](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#create-a-github-account-and-set-up-your-profile)

2. [お客様のアカウントを Microsoft アカウントと Microsoft および Microsoft Docs の組織にリンクする](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#link-your-github-and-microsoft-accounts)

3. [2要素認証を有効にする](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#enable-two-factor-authentication-and-create-an-access-token)

4. [ビルドシステムによる GitHub アカウントへのアクセスの承認](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#authorize-the-ops-build-system-to-access-your-github-account)

5. [Visual Studio Code のインストール](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-visual-studio-code)

6. [GitHub とそのツールをインストールする](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-git-client-tools)

7. [Docs Authoring Pack をインストールする](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-the-docs-authoring-pack)

## <a name="set-up-your-own-version-of-the-repo"></a>独自のバージョンのリポジトリをセットアップする

GitHub アカウントとツールを作成して設定したら、リポジトリの個人バージョンを作成できます。 ここでブランチを作成し、すべての変更を行います。

### <a name="fork-the-repository"></a>リポジトリの分岐

ソースファイルのローカルコピーが必要であるため、フォークから運用リポジトリへのプル要求を作成できます。

#### <a name="to-fork-the-repository"></a>リポジトリをフォークするには

1. GitHub アカウントにサインインし、に https://github.com/microsoftdocs/windowsserverdocs-pr アクセスします。

2. **[フォーク]** を選択します。

    ![ページで強調表示されているフォークボタン](media/create-new-using-github/fork-button.png)

3. フォークの場所として GitHub アカウントを選択します。

    ![ページで強調表示されているフォークボタン](media/create-new-using-github/fork-location.png)

### <a name="clone-the-repository"></a>リポジトリのクローン

リポジトリを複製して、リポジトリのローカルコピーをローカルデバイスに取得する必要があります。

#### <a name="to-clone-the-repository"></a>リポジトリを複製するには

1. に https://github.com/settings/developers 移動し、左側のウィンドウから **[個人用アクセストークン]** を選択します。

2. **[新しいトークンの生成]** を選択し、トークンにわかりやすい一意の名前を付けて、使用可能なすべてのスコープを選択し、 **[トークンの生成]** を選択します。

3. トークンをコピーし、安全な場所に配置します。 この操作は、残りのプロセスで必要になります。ページを終了した後は、元に戻すことはできません。

4. Git Bash コマンドを開き、リポジトリを保存するディレクトリに移動します。 、を`C:\users\<your_name>\GitHub`使用することをお勧めします。

5. 特定の情報を使用して、リポジトリを複製し、リモートブランチを設定するために、次のコマンドを一度に1つずつ入力します。

    ```markdown

    git clone https://<your_github_username>:<your_personal_access_token>@github.com/<your_github_username>/windowsserverdocs-pr.git

    cd windowsserverdocs-pr

    git remote add upstream https://<your_github_username>:<your_personal_access_token>@github.com/MicrosoftDocs/windowsserverdocs-pr.git

    git fetch upstream master
    ```

6. 次のコマンドを実行して、リモートが適切に設定されていることを確認します。

    `git remote -v`

7. 次のような出力が表示できます。

    ```markdown
    $ git remote -v

    origin https://github.com/<your_github_username>/windowsserverdocs-pr.git (fetch)
    origin https://github.com/<your_github_username>/windowsserverdocs-pr.git (push)
    upstream https://github.com/MicrosoftDocs/windowsserverdocs-pr.git (fetch)
    upstream https://github.com/MicrosoftDocs/windowsserverdocs-pr.git (push)
    ```

    リモート出力が次のようにならない場合は、を最初に実行`git remote remove upstream`してみてください。

## <a name="create-a-branch-and-a-new-article"></a>ブランチと新しいアーティクルを作成する

記事を作成するには、次の手順に従います。

### <a name="create-a-new-branch-and-a-new-file"></a>新しいブランチと新しいファイルを作成する

コンテンツの操作を開始する前に、ローカルリポジトリに新しいブランチを作成する必要があります。

#### <a name="to-create-a-new-branch-in-git-bash"></a>Git Bash で新しいブランチを作成するには

- Git Bash を開き、コマンド (一度に1つずつ) を入力します。

    ```markdown
    cd windowsserverdocs-pr

    git checkout –B <name_of_your_new_branch>

    git push origin <name_of_your_new_branch>
    ```

    >[!Note]
    >ブランチに明確で一意の名前を付けることを強くお勧めします。この場合、後でもう一度見つけることができます。

    コマンドが完了すると、新しいブランチに追加され、新しいファイルを作成する準備が整います。 Git Bash のインスタンスごとに、windowsserverdocs-pr リポジトリを1回だけ変更する必要があります。 Git Bash を閉じた場合は、ディレクトリを開いた後でもう一度変更する必要があります。

#### <a name="to-create-a-new-file-in-your-branch"></a>ブランチに新しいファイルを作成するには

1. Windows エクスプローラーを開き、GitHub ディレクトリにアクセスして、フォルダー構造に新しいテキストファイルを作成します。 ファイル名はすべて小文字で、ハイフンで区切る必要があります。 たとえば、 _what-is-windows-server.md_のようになります。

     また、ファイル拡張子を .txt から md に変更する必要があります。 表示されるエラーメッセージで、[**はい]** を選択して、新しいファイル拡張子を持つファイルを保存します。

2. Visual Studio Code を開き、 **[ファイル]** に移動し、 **[フォルダーを開く]** を選択して、手順1で作成したファイルの GitHub の場所に移動します。

3. **[エクスプローラー]** ウィンドウで、新しいファイルを選択します。

4. テキストをページに追加します。 新しい記事を作成する場合は、必ず[必要なメタデータタグを Windows Server 関連の記事に追加](metadata-requirements-for-articles.md)してください。

5. [**ファイル** > の**保存**] を選択します。

### <a name="preview-your-text"></a>テキストのプレビュー

新しいファイルにテキストを追加した後は、変更内容をプレビューして、正しく表示されることを確認する必要があります。

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

記事を完了した後は、ライターから承認を取得する必要があります (このためには、しばらく時間がかかることがあります)。

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
