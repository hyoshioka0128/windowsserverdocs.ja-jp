# <a name="contributing-to-windows-server-technical-documentation"></a>Windows Server 技術ドキュメントへの投稿

Windows Server 技術ドキュメントにご関心をお寄せいただきありがとうございます。ドキュメントへのフィードバック、編集、追記に感謝いたします。Windows Server の技術的なコンテンツ保持のため、2 つの場所を別々にご用意しております。パブリック (windowsserverdocs) と、プライベート (windowsserverdocs pr) です。マイクロソフトの従業員であるかどうかによって、ご協力いただく場所が異なります。

- **私はマイクロソフトの従業員ではありません。** マイクロソフトの従業員ではない場合、パブリックな場所に貢献する必要があります。 その方法については、この記事を読み進めてください。


- **私はマイクロソフトの従業員です。** マイクロソフトの従業員としてを実行しているに基づいてのオプションがあります。

    - **新しい記事を作成します。** 新しい記事を作成するには、作成する必要があり、GitHub アカウントとツールを設定すると、フォークと複製 windowsserverdocs pr リポジトリでは、独自のリモート ブランチを設定、アーティクルを作成および最後に、新しいプル要求の承認および発行を作成します。 これらの手順については、次を参照してください。、 [GitHub および Visual Studio Code を使用して新しい Windows Server の記事を作成](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/Contributor-guide/create-new-using-github.md)記事。

    - **既存のアーティクルに大きな変化を作成します。** 既存の記事に大幅な変更するには、手順を利用できる、 [GitHub および Visual Studio Code を使用して、既存の Windows Server の記事を編集](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/Contributor-guide/edit-existing-using-github.md)記事。

    - **既存の記事に軽微な変更を行います。** 既存の記事に軽微な変更するには、手順を利用できる、 [web ブラウザーと GitHub を使用して既存の Windows Server の記事を更新](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/Contributor-guide/github-browser-updates.md)記事。

## <a name="sign-a-cla"></a>CLA に署名します。

すべての共同作成者である***いない***マイクロソフトの従業員である必要があります[Microsoft コントリビューション ライセンス契約 (CLA) に署名する](https://cla.microsoft.com/)任意の Microsoft リポジトリを編集する前にします。 以前は、これでは、Microsoft リポジトリ内で既に編集した場合!
この手順を既に完了しました。

## <a name="editing-topics"></a>トピックの編集

できるだけ単純に、既存のパブリック ファイルを編集できるようにしました。

### <a name="to-edit-a-topic"></a>トピックを編集するには

1. ページに移動 https://docs.microsoft.com/windows-server を更新し、選択する**編集**します。

    ![GitHub の Web、[編集] リンクを表示](media/contribute-link.png)

2. サインイン (またはサインアップ) GitHub アカウント。

    トピックを編集することができます ページにアクセスする GitHub アカウントが必要です。

3. 選択、**鉛筆**アイコン (赤いボックス) でコンテンツを編集します。

    ![GitHub の Web、赤いボックスで、鉛筆アイコンを表示](media/pencil-icon.png)

4. Markdown の言語を使用して、トピックに変更を加えます。 編集する方法については、マークダウンを使用してコンテンツを参照してください。

    - **GitHub の Microsoft 組織にリンクしている場合。** [Windows Server 共同作成者ガイド](https://github.com/MicrosoftDocs/windowsserverdocs-pr/tree/master/Contributor-guide)

    - **Microsoft の外部場合。** [Markdown をマスターします。](https://guides.github.com/features/mastering-markdown/)

5. クリックして、提案された変更を行って**変更のプレビュー**が正しいようになっていることを確認します。

    ![GitHub の Web、変更のプレビュー タブ](media/preview-changes.png)

6. 完了したら、トピックを編集するには、ページの下部までスクロールし、独自のフォークのわかりやすい名前を入力および順にクリックします**ファイルの変更提案**個人用の GitHub アカウントに、フォークを作成します。

    ![GitHub の Web、提案ファイルの変更 ボタンを表示](media/propose-file-change.png)

    **変化を比較する**は独自のフォークと元のコンテンツとの間の変更を表示する画面が表示されます。

7. **変化を比較する** 画面で、チェックインしているファイルを使用して問題があるかどうかは表示されます。

    問題がない場合は、メッセージが表示されます**をマージすることができ**します。

    ![GitHub の Web、比較を示す画面を変更します。](media/compare-changes.png)

8. 選択**プル要求の作成**です。

    プル要求の github リポジトリ内のブランチにプッシュした変更に関する他のユーザーの入力するようにします。 プル要求が開かれた後にについて説明しますコラボレーターとともに潜在的な変更を確認し、変更内容がベース ブランチにマージされる前に、フォロー アップのコミットを追加し、できます。 詳細については、次を参照してください[プル要求について。](https://help.github.com/articles/about-pull-requests)

9. タイトルと、承認者の要求の内容について適切なコンテキストを提供する説明を入力します。

10. 変更されたファイルのみがこのプル要求であることを確認する、ページの一番下までスクロールします。 それ以外の場合、他のユーザーからの変更を上書きする可能性があります。

11. 選択**プル要求の作成**実際には、プル要求を送信するには、もう一度です。

    プル要求は、トピックのライターに送信され、編集内容を確認します。 要求が受け入れられた場合は、更新プログラムが発行されます。

## <a name="resources"></a>参考資料

- Markdown の編集には、使い慣れたテキスト エディターを使用できます。 お勧め[Visual Studio Code](https://code.visualstudio.com/)、Microsoft から無料の軽量なオープン ソース エディター。
