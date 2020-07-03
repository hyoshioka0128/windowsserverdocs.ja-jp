---
title: Web ブラウザーと GitHub を使用して既存の Windows Server の記事を編集する
description: Microsoft の従業員として、web ブラウザーと GitHub を使用して既存の Windows Server ドキュメントをすばやく編集する方法について説明します。
author: eross-msft
ms.author: lizross
ms.date: 07/02/2020
ms.openlocfilehash: 61ceb05b6cb9602faaa4d17b4dc2d978cb571ddb
ms.sourcegitcommit: d754f9e39fc28e4c8768b77bcc9d02ffe2fa6535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85911223"
---
# <a name="update-existing-windows-server-and-azure-stack-hci-articles-using-a-web-browser-and-github"></a>Web ブラウザーと GitHub を使用して、既存の Windows Server および Azure Stack HCI の記事を更新する

Windows Server の技術コンテンツを保持する場所は2つあります。 一方の場所はパブリック (windowsserverdocs) で、もう一方はプライベート (windowsserverdocs-pr) です。 だれがどの場所に投稿するかを決定します。

- **Microsoft の従業員ではありません。** マイクロソフト以外の従業員は、公共の場所に投稿する必要があります。 その方法については、 [Contributing.md](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md)ファイルを参照してください。

- **私は Microsoft の従業員です。** Microsoft の従業員は、何をしようとしているかに応じて、オプションがあります。

    - **新しい記事を作成します。** 新しい記事を作成するには、GitHub アカウントとツールを作成して設定し、windowsserverdocs-pr リポジトリをフォークして複製し、リモートブランチを設定して、記事を作成し、最後に承認と発行のための新しいプル要求を作成する必要があります。 これらの手順については、GitHub を使用した[新しい Windows Server の作成に関する記事と Visual Studio Code](create-new-using-github.md)に関する記事をご覧ください。

    - **既存の記事に大きな変更を加えます。** 既存の記事に大幅な変更を加えるには、GitHub を使用した[既存の Windows Server の編集に関する記事と Visual Studio Code](edit-existing-using-github.md)の記事の手順に従ってください。

    - **既存のアーティクルに対して軽微な変更を行います。** 既存の記事に軽微な変更を加えるには、この記事の手順に従ってください。

    > [!IMPORTANT]
    > docs.microsoft.com に公開されるすべてのリポジトリには、「[Microsoft Open Source Code of Conduct (Microsoft オープン ソース倫理規定)](https://opensource.microsoft.com/codeofconduct/)」または「[.NET Foundation Code of Conduct (.NET Foundation 倫理規定)](https://dotnetfoundation.org/code-of-conduct)」が適用されています。 詳細については、[倫理規定に関する FAQ](https://opensource.microsoft.com/codeofconduct/faq/) のページを参照してください。 または、ご質問やコメントがある場合は、[opencode@microsoft.com](mailto:opencode@microsoft.com) または [conduct@dotnetfoundation.org](mailto:conduct@dotnetfoundation.org) までご連絡ください。
    >
    > パブリック リポジトリにあるドキュメントおよびコード例に対する軽微な修正や明確化は、「[docs.microsoft.com - 使用条件](https://docs.microsoft.com/legal/termsofuse)」の対象になります。 お客様が Microsoft の従業員ではない場合、新規または大幅な変更を加えると、オンラインの貢献者使用許諾契約書 (CLA) のご提出をお願いするコメントが pull request 内に生成されます。 このオンライン フォームにご入力いただいてから、お客様の pull request に対するレビューや承認を実施いたします。

## <a name="quick-edits-to-existing-articles-using-github-and-a-web-browser"></a>GitHub と web ブラウザーを使用した既存の記事のクイック編集

クイック編集により、ドキュメント内の小さなエラーや漏れを報告および修正するプロセスが合理化されます。 さまざまな努力を重ねても、公開されたドキュメントには文法やスペルに関する小さな誤りが "_必ず_" 入り込みます。

1. [GitHub アカウントのセットアップ](https://review.docs.microsoft.com/en-us/help/contribute/contribute-get-started-setup-github?branch=master)に関する手順に従います。

1. [Windows Server](https://github.com/MicrosoftDocs/windowsserverdocs-pr/tree/master/WindowsServerDocs)または[Azure Stack HCI](https://github.com/MicrosoftDocs/azure-stack-docs-pr/tree/master/azure-stack/hci)プライベートリポジトリにアクセスします。 プライベートリポジトリはより頻繁に監視されるので、承認時間が短縮され、品質チェックが向上し、ライブサイトに表示されるようにステージング環境でコンテンツを表示できるようになります。

2. 編集する記事に移動し、[**このファイルを編集**] ボタンを選択します。

   ![[このファイルを編集] ボタン](media/github-browser-updates/edit-this-file.png)

3. トピックを編集し、下部までスクロールして変更内容を簡単に説明し、[**変更のコミット**] を選択します。

    ![タイトル情報で変更をコミットする](media/github-browser-updates/commit-changes.png)

## <a name="submit-the-pull-request"></a>プル要求を送信する

プル要求を作成したら、承認および発行のために送信する必要があります。

### <a name="to-submit-your-pull-request"></a>プル要求を送信するには

1. [**プル要求を開く**] ページで、コミットメッセージを更新して PR に適したものにします。 例: 最初の段落のスペルミスを修正します。

2. 含める予定のコミットとファイルのみが含まれていることを確認してください。 また、PR が上流リポジトリの正しいブランチであることを確認します。これは、master (通常は) またはリリースブランチ (ときどき) のいずれかです。

3. 右側のウィンドウの [**レビュー担当者**] 領域で歯車アイコンを選択し、「 _windowsservercontent_」と入力します。 エイリアスのメンバーは、変更をレビューするポイントになり、プル要求をマージするか、マージ前に変更する項目に関するコメントを追加します。

4. **[pull request の作成]** を選択します。 新しい PR は、フォーク内の作業ブランチにリンクされます。 PR がマージされるまで、フォーク内の同じ作業ブランチにプッシュする新しいコミットは、自動的に PR に含まれます。 新しいラベルがプル要求に追加されます。これには、**マージしないでください**。 これは、コンテンツがまだ進行中であるため、レビューまたはライブサイトへのプッシュを行わないことを意味します。

5. エイリアスから他のユーザーにコンテンツをレビューする準備ができたら、コメントに **#sign**テキストを追加する必要があります。 このコメント:

    - プル要求のラベルを更新します。マージの**準備**ができ**ていません**。

    - コンテンツをレビューする準備ができたことを、エイリアスとライターに知らせます。

    - 承認後、コンテンツの準備ができたことを管理者に知らせます。
