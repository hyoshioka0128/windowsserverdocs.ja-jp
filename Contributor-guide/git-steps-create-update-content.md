<properties pageTitle="新しいアーティクルの作成または既存の記事を更新するための Git コマンド" description="作成および WindowsServerDocs pr 内のアーティクルの更新手順を実行します。" metaKeywords="" services="" solutions="" documentationCenter="" authors="Kathy Davies" videoId="" scriptId="" manager="dongill" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="08/24/16" ms.author="kathydav" />

# <a name="git-commands-to-create-or-update-an-article"></a>Git コマンドを作成または更新記事

>!注:これらのコマンドと Github からのファイルをプルする既定のリポジトリを指定するように構成しました。 Github からのファイルをプルする用語は、*上流*します。 ファイルをプッシュするは、*原点*します。 当社のリポジトリとワークフローの設計方法に基づき、アップ ストリームに設定して、リポジトリには、Microsoft の組織の下にある https://github.com/Microsoft/WindowsServerDocs-prと配信元には、独自の Github アカウントでこのリポジトリのフォークする必要があります。 たとえば、Kathy は https://github.com/KBDAzure/WindowsServerDocs-pr 

>設定を確認するには、次のように入力します。```git config -l```します。 目的の場所を参照しているかどうかを確認する Url を確認します。

## <a name="add-or-update-an-article"></a>追加または更新記事

ローカル ブランチを作成、変更内容を保存およびそれらをリモート フォークにプッシュする方法を次に示します。

1. Git Bash (または Git を使用するコマンド ライン ツール) を起動します。

2. WindowsServerDocs pr に変更します。

        cd WindowsServerDocs-pr

3. ローカル マスターを保持することをお勧めブランチとリモートのマスター分岐フォーク リポジトリのマスターとの同期に分岐します。 こうと、保存する多くのストレスと時間--を紛失する可能性が高くなりますの問題を早期に発見し、既知の動作状態にしておきます。 次のコマンドを実行します。

        git checkout master
        git pull upstream master
        git push origin master

4. 実行する分岐を作成する準備ができたので、毎日または成果物ベースで動作します。 リリース ブランチからローカル作業ブランチを作成する最善の方法では、使用して実行します。

        git checkout upstream/upstream-branch-name -b your-local-branch-name

   これは、アップ ストリーム ブランチから直接ローカル ブランチを作成し、間違ったファイルを新しいローカル ブランチにマージを防ぐことができます。 たとえば、ga しきい値ブランチに基づいて作業ブランチを作成するには、このようなコマンドを実行します。
      
        git checkout upstream/master -b working-11-18

   コンテンツがブランチにマージする必要がありますで作業している場合         

5. ローカル作業ブランチをフォークに追加します。

        git push origin <working branch>

6. 新しい記事を作成または既存のアーティクルに変更を加えます。 Windows エクスプ ローラーを使用して、マークダウン ファイル、およびファイルを作成、編集したり、markdown エディターを開きます。 基本的な書式設定のヘルプを参照してください[記事](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)Github でします。

7. 必要なメタデータとバージョンについては、追加による[メタデータおよび製品のバージョン管理](metadata-OSversioning-and-trademarks.md)します。

8. 状態を確認し、追加および変更をコミットします。

        git status

   表示されているファイルを変更したかどうかを確認する結果を確認します。 すべてのファイル正確な場合は、すべてのファイルを追加するには、このコマンドを実行します。

        git add .
        git commit –m "<comment>"

   特定のファイルのみを追加する (場合など、```git status```を送信するファイルを一覧表示されます)、代わりに実行する必要があります。

        git add <file path>
        git commit –m "<comment>"

   >[!IMPORTANT]
   >コマンドは、```git add .```によって報告されたすべての保留中の変更を追加します。```git status```します。 つまり、```git status```を追加、使用する追跡対象でない更新プログラムを示しています。```git add <file path>```代わりにします。  

9. アップ ストリームからの変更で、ローカル作業ブランチを更新します。

        git pull upstream master

10. GitHub のフォークに変更をプッシュします。

        git push origin <working branch>

## <a name="submit-your-changes"></a>変更を送信します。

ステージング環境、検証、および発行のコンテンツを送信する準備ができたらは、GitHub UI を使用して、プル要求を作成します。 

プル要求 (PR) を開始するときに、プロジェクトをビルドします、および、内部ステージング サイトを発行このテストの成功をトリガーします。 テスト パスを取得し、ステージング サイトで、更新プログラムを確認する方法は、このため、マージが準備できていない状態をプル要求を開くことができます。 PR に、ビルド詳細とステージング リンクのコメントとしてからポストバックされます。 

以下を実行する責任が**マージ変更を依頼する前に**:
  - ビルドのエラーがないかどうかを確認する詳細をレビューします。 
  - ステージング サイトの更新プログラムを確認します。

これが完了したら後、は、いずれかで指定します。
- PR を「準備完了-マージ」ラベルを追加します。 \(クリックして**ラベル**または PR コメントのストリームの右側にある歯車アイコン)
- 準備完了/マージをコメントとして追加して、WSSC プルのレビュー担当者の別名に電子メールを送信: wssc pra

PR レビュー担当者は、変更を確認し、問題や質問がある場合を除き、PR を受け入れます。 フィードバックや問題を修正する要求は、コメントとして追加されます。 確認[品質基準のプル要求レビュー](contributor-guide-pr-criteria.md)については何が必要です。

## <a name="publishing"></a>公開

- 約 10:00 と午後 3時 00分に記事が公開された太平洋標準時, 月曜日 ~ 金曜日です。 プル要求レビュー担当者が時間を確認して同意する前に、変更をマージする必要があることに留意してください。 スケジュールされた次回の発行で取得すべき変更をマージする必要があります。 特定のパブリケーションのサイクルのパブリッシュされたアーティクルを必要がある場合は、前もって知るプル要求レビュー担当者を使用できます。 PR が受け入れられたときに、変更は、リポジトリにマージされ、実行 [次へ] の時間パブリケーションに含めることは。 記事オンライン発行後に表示するには、最大で 30 分かかることができます。 
