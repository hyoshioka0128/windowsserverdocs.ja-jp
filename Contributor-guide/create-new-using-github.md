---
title: GitHub、Visual Studio Code を使用して新しい Windows Server の記事を作成します。
description: マイクロソフトの従業員として GitHub および Visual Studio Code を使用して、Windows Server に関連する新しい資料を作成する方法。
author: eross-msft
ms.author: lizross
ms.date: 05/02/2019
ms.openlocfilehash: d75bf135266a4783ab2617977b344782cea679ef
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624564"
---
# <a name="create-new-windows-server-articles-using-github-and-visual-studio-code"></a>GitHub、Visual Studio Code を使用して新しい Windows Server の記事を作成します。

Windows Server の技術的なコンテンツを保持する 2 つの別々 の場所があります。 パブリックの場所のいずれか (windowsserverdocs)、もう一方はプライベート (windowsserverdocs pr)。 ユーザーに協力する位置を決定します。

- **私はマイクロソフトの従業員です。** マイクロソフトの従業員としてを実行しているに基づいてのオプションがあります。

    - **新しい記事を作成します。** 新しい記事を作成するには、作成する必要があり、GitHub アカウントとツールを設定すると、フォークと複製 windowsserverdocs pr リポジトリでは、独自のリモート ブランチを設定、アーティクルを作成および最後に、新しいプル要求の承認および発行を作成します。 これらの手順については、この記事を続行します。

    - **既存のアーティクルに大きな変化を作成します。** 既存の記事に大幅な変更するには、手順を利用できる、 [GitHub および Visual Studio Code を使用して、既存の Windows Server の記事を編集](edit-existing-using-github.md)記事。

    - **既存の記事に軽微な変更を行います。** 既存の記事に軽微な変更するには、手順を利用できる、 [web ブラウザーと GitHub を使用して既存の Windows Server の記事を更新](github-browser-updates.md)記事。

- **Microsoft の従業員わかりません。** Microsoft 以外の従業員としては、パブリックな場所に協力する必要があります。 その方法については、次を参照してください。、 [Windows Server 技術ドキュメントに貢献する](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md)記事。

## <a name="prerequisites"></a>前提条件

リポジトリで作業を開始する前にする必要がありますを作成し、GitHub アカウントを設定する、2 要素の検証をセットアップおよびインストールし、必要なすべてのツールを構成します。 場合は、下に進んで、[フォーク リポジトリ セクション](#fork-the-repository)に改訂された記事。

1. [GitHub アカウントとプロファイルを作成します。](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#create-a-github-account-and-set-up-your-profile)

2. [Microsoft アカウントと Microsoft、MicrosoftDocs 組織アカウントをリンクします。](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#link-your-github-and-microsoft-accounts)

3. [2 要素認証を有効にします。](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#enable-two-factor-authentication-and-create-an-access-token)

4. [GitHub アカウントにアクセスするビルド システムを承認します。](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#authorize-the-ops-build-system-to-access-your-github-account)

5. [Visual Studio Code をインストールします。](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-visual-studio-code)

6. [GitHub とそのツールをインストールします。](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-git-client-tools)

7. [Docs Authoring Pack をインストールします。](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-the-docs-authoring-pack)

## <a name="set-up-your-own-version-of-the-repo"></a>リポジトリの独自のバージョンを設定します。

作成、GitHub アカウントとツールを設定したら後、は、リポジトリの個人のバージョンを作成できます。 これは、場所、分岐が作成され、すべての変更を行います。

### <a name="fork-the-repository"></a>リポジトリの分岐

運用リポジトリをフォークからプル要求を作成するようには、ソース ファイルのローカル コピーを作成する必要があります。

#### <a name="to-fork-the-repository"></a>リポジトリをフォークするには

1. GitHub アカウントにサインインしに移動 https://github.com/microsoftdocs/windowsserverdocs-prします。

2. 選択**フォーク**します。

    ![ページで強調表示された分岐のボタン](media/create-new-using-github/fork-button.png)

3. フォークの場所として、GitHub アカウントを選択します。

    ![ページで強調表示された分岐のボタン](media/create-new-using-github/fork-location.png)

### <a name="clone-the-repository"></a>リポジトリのクローン

リポジトリの取得、ローカル デバイスに、リポジトリのローカル コピーを複製する必要があります。

#### <a name="to-clone-the-repository"></a>リポジトリを複製するには

1. 移動して https://github.com/settings/developers、し、**個人用アクセス トークン**左側のウィンドウ。

2. 選択**新しいトークンの生成**および、トークンの一意なわかりやすい名前を付けて、すべての使用可能なスコープを選択し、**トークンの生成**します。

3. トークンをコピーし、安全な場所に配置します。 このプロセスの残りの部分で、必要になり、にそこへ戻ることはできませんが、ページを終了すると、します。

4. Git Bash コマンドを開き、リポジトリを格納するディレクトリを変更します。 使用して、ことをお勧めします。`C:\users\<your_name>\GitHub`します。

5. リポジトリを複製し、リモート ブランチを設定する 1 つずつ、独自の情報を使用して、次のコマンドを入力します。

    ```markdown

    git clone https://<your_github_username>:<your_personal_access_token>@github.com/<your_github_username>/windowsserverdocs-pr.git

    cd windowsserverdocs-pr

    git remote add upstream https://<your_github_username>:<your_personal_access_token>@github.com/MicrosoftDocs/windowsserverdocs-pr.git

    git fetch upstream master
    ```

6. リモコンが正しく設定されているかどうかを確認するには、このコマンドを実行します。

    `git remote -v`

7. この出力のようなものが表示されます。

    ```markdown
    $ git remote -v

    origin https://github.com/<your_github_username>/windowsserverdocs-pr.git (fetch)
    origin https://github.com/<your_github_username>/windowsserverdocs-pr.git (push)
    upstream https://github.com/MicrosoftDocs/windowsserverdocs-pr.git (fetch)
    upstream https://github.com/MicrosoftDocs/windowsserverdocs-pr.git (push)
    ```

    最初の実行を再度試行できる場合は、リモートの出力は、次のようになりますが、`git remote remove upstream`します。

## <a name="create-a-branch-and-a-new-article"></a>ブランチと、新しいアーティクルを作成します。

アーティクルを作成する次の手順に従います。

### <a name="create-a-new-branch-and-a-new-file"></a>新しいブランチと新しいファイルを作成します。

コンテンツに作業を開始する前に、ローカル リポジトリで新しいブランチを作成する必要があります。

#### <a name="to-create-a-new-branch-in-git-bash"></a>Git Bash で新しいブランチを作成するには

- Git Bash を開き、(1 つずつ) のコマンドを入力します。

    ```markdown
    cd windowsserverdocs-pr

    git checkout –B <name_of_your_new_branch>

    git push origin <name_of_your_new_branch>
    ```

    >[!Note]
    >後でもう一度検索できるように独自のブランチを何か明らかで、一意な名前を強くお勧めします。

    コマンドが完了すると、新たなブランチであるし、新しいファイルを作成する準備が完了します。 のみ、Git Bash のインスタンスごとに 1 回 windowsserverdocs pr リポジトリに変更する必要があります。 Git Bash を閉じた場合は、それを開いた後にもう一度ディレクトリを変更する必要があります。

#### <a name="to-create-a-new-file-in-your-branch"></a>独自のブランチで新しいファイルを作成するには

1. Windows エクスプ ローラーを開き、GitHub のディレクトリに移動して、フォルダー構造で新しいテキスト ファイルを作成します。 ファイル名は、すべて小文字とハイフンで区切られたである必要があります。 たとえば、 _what-、-windows-server.md_します。

     .Txt をファイル拡張子を変更することも必要があります。 md します。 エラー メッセージが表示されたら、次のように選択します。**はい**を新しいファイル拡張子を持つファイルを保存します。

2. Visual Studio Code を開きに移動**ファイル**、**フォルダーを開く**、GitHub の手順 1. で作成したファイルの場所に移動します。

3. **エクスプ ローラー**ウィンドウで、新しいファイルを選択します。

4. ページに、テキストを追加し、**ファイル** > **保存**します。

### <a name="preview-your-text"></a>テキストをプレビューします。

新しいファイルにテキストを追加した後は、正しく表示されるかどうかを確認する変更をプレビューする必要があります。

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

あなたの記事を完了すると、後に、ライターから承認を取得する必要があります (この時間を許可する) パブリケーション。

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
