---
title: Web ブラウザーと GitHub を使用して既存の Windows Server の記事を編集します。
description: マイクロソフトの従業員として、web ブラウザーと GitHub を使用して既存の Windows Server のドキュメントにクイック編集を加える方法。
author: eross-msft
ms.author: lizross
ms.date: 05/02/2019
ms.openlocfilehash: d4574de7774a43092815a3d154020559c50fdcf9
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624589"
---
# <a name="update-existing-windows-server-articles-using-a-web-browser-and-github"></a>Web ブラウザーと GitHub を使用して既存の Windows Server の記事を更新します。

Windows Server の技術的なコンテンツを保持する 2 つの別々 の場所があります。 パブリックの場所のいずれか (windowsserverdocs)、もう一方はプライベート (windowsserverdocs pr)。 ユーザーに協力する位置を決定します。

- **Microsoft の従業員わかりません。** Microsoft 以外の従業員としては、パブリックな場所に協力する必要があります。 その方法については、次を参照してください。、[ある contributing.md をご覧](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md)ファイル。

- **私はマイクロソフトの従業員です。** マイクロソフトの従業員としてを実行しているに基づいてのオプションがあります。

    - **新しい記事を作成します。** 新しい記事を作成するには、GitHub アカウントとツールの作成と設定、windowsserverdocs-pr リポジトリのフォークと複製、リモート ブランチの設定、記事の作成をする必要があり、最後に承認および発行するための新しいプル要求を作成します。これらの手順については、「[Create new Windows Server articles using GitHub and Visual Studio Code (GitHub および Visual Studio Code を使用した新しい Windows Server の記事の作成)](create-new-using-github.md)」の記事を参照してください。

    - **既存のアーティクルに大きな変化を作成します。** 既存の記事に大幅な変更するには、手順を利用できる、 [GitHub および Visual Studio Code を使用して、既存の Windows Server の記事を編集](edit-existing-using-github.md)記事。

    - **既存の記事に軽微な変更を行います。** 既存の記事に軽微な変更を加えるには、この記事の手順に従います。

    > [!IMPORTANT]
    > Docs.microsoft.com に公開されるすべてのリポジトリを採用して、 [Microsoft オープン ソース倫理規定](https://opensource.microsoft.com/codeofconduct/)または[.NET Foundation 倫理](https://dotnetfoundation.org/code-of-conduct)します。 詳細については、次を参照してください。、 [FAQ の実施コード](https://opensource.microsoft.com/codeofconduct/faq/)します。 お問い合わせくださいまたは[ opencode@microsoft.com ](mailto:opencode@microsoft.com)、または[ conduct@dotnetfoundation.org ](mailto:conduct@dotnetfoundation.org)質問またはコメントにします。
    >

    > パブリック リポジトリのドキュメントとコードの例に対する軽微な修正または説明は、「[docs.microsoft.com - 使用条件](https://docs.microsoft.com/legal/termsofuse)」で取り上げられています。新規または大幅な変更がある場合は、プル要求でコメントが生成され、オンラインの貢献者使用許諾契約書 (CLA) を送信するよう求められます (Microsoft の従業員でない場合)。プル要求を受け入れるには、オンライン フォームを完了していただく必要があります。


## <a name="quick-edits-to-existing-articles-using-github-and-a-web-browser"></a>GitHub と web ブラウザーを使用して既存の記事へのクイック編集

クイック編集は、報告してドキュメントに軽度のエラーや未入力を修正するプロセスを合理化します。 すべての作業や小規模の文法、スペル ミスに関係なく_は_公開されたドキュメントに利用できるようします。

1. [https://partnercenter.microsoft.com/partner/support](https://github.com/MicrosoftDocs/windowsserverdocs-pr/tree/master/WindowsServerDocs ) に移動します。

2. 編集する記事に移動して選択し、**このファイルを編集**ボタンをクリックします。

   ![ファイルは、このボタンを編集します。](media/github-browser-updates/edit-this-file.png)

3. このトピックを編集し、一番下までスクロール、変更を簡単に説明し選択して**変更をコミット**します。

    ![タイトル情報に変更をコミットします。](media/github-browser-updates/commit-changes.png)

## <a name="submit-the-pull-request"></a>プル要求を送信します。

プル要求を作成した後の承認と発行のために送信する必要があります。

### <a name="to-submit-your-pull-request"></a>プル リクエストを送信するには

1. **プル要求を開く**ページで、PR のより適切なコミット メッセージを更新 例: 最初の段落では、入力ミスを修正します。

2. コミットと含まれるはずのファイルのみが含まれることを確認します。 (通常は)、PR がアップ ストリーム リポジトリのいずれかのマスターに適切なブランチに移動するチェックもまたはリリース ブランチ (場合によっては)。


3. 右側ペインの **[レビュー担当者]** 領域で歯車アイコンを選択し、_windowsservercontent_ を入力します。エイリアスのメンバーは、変更内容を確認し、プル要求をマージするか、マージする前に変更する内容に関するコメントを追加する立場にあります。


4. **[プル要求の作成]** を選択します。新しい PR は、フォークの作業ブランチにリンクされます。PR がマージされるまで、フォークの同じ作業ブランチに対してプッシュする新しいコミットはすべて自動的に PR に含められます。**do-not-merge** と書かれたプル要求に新しいラベルが追加されます。これは単に、コンテンツが進行中であり、レビューもライブ サイトへのプッシュも行うべきではないことを示します。


5. エイリアス内のだれかにコンテンツをレビューしてもらう準備ができたら、コメントに **#sign-off** というテキストを追加する必要があります。このコメントの効果:

   - プル要求のラベルを **do-not-merge** から **ready-to merge** に更新します。


    - エイリアスとライターのコンテンツのレビューする準備ができたことを知ることができます。

    - により、管理者があること、承認後、コンテンツ準備 go live です。
