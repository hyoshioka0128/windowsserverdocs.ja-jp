---
ms.assetid: 4baefbd3-038f-44c0-85ba-f24e9722b757
title: 付録 G-Active Directory での管理者グループのセキュリティ保護
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: cdea04e211b1873ff51c4bc3dc9ff24e746ead69
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408644"
---
# <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>付録 G: Active Directory の Administrators グループをセキュリティで保護する

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012


## <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>付録 G: Active Directory の Administrators グループをセキュリティで保護する  
Enterprise Admins (EA) グループおよび Domain Admins (DA) グループの場合と同様に、組み込みの管理者 (BA) グループのメンバーシップは、ビルドまたはディザスターリカバリーのシナリオでのみ必要になります。 [「付録 D: Active Directory での組み込みの管理者アカウントのセキュリティ保護](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)」の説明に従ってセキュリティ保護されている場合、管理者グループには毎日のユーザーアカウントがないことを考慮してください。  

管理者は、既定では、それぞれのドメイン内の AD DS オブジェクトのほとんどの所有者です。 このグループのメンバーシップは、所有権またはオブジェクトの所有権を取得する機能が必要なビルドまたはディザスターリカバリーのシナリオで必要になる場合があります。 さらに、DAs と EAs には、Administrators グループの既定のメンバーシップによって、多数の権限とアクセス許可が継承されています。 Active Directory の特権グループの既定のグループの入れ子を変更することはできません。また、各ドメインの管理者グループは、後の手順で説明されているようにセキュリティで保護する必要があります。  

フォレスト内の各ドメインの Administrators グループについて、次のようにします。  

1.  [「付録 D: Active Directory での組み込み管理者アカウントのセキュリティ保護](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)」の説明に従ってセキュリティ保護されている場合は、管理者グループからすべてのメンバーを削除します。  

2.  各ドメインのメンバーサーバーとワークステーションが含まれている Ou にリンクされた Gpo では、BA グループは、 **Computer Configuration\Policies\Windows 権利 Policies \ User Rights Assignment**の次のユーザー権利に追加する必要があります。  

    -   ネットワークからのこのコンピューターへのアクセスを拒否する  

    -   バッチ ジョブとしてのログオンを拒否  

    -   サービスとしてのログオンを拒否  

3.  フォレスト内の各ドメインのドメインコントローラー OU で、Administrators グループには次のユーザー権利が付与されている必要があります。  

    -   ネットワークからこのコンピューターにアクセスする  

    -   ローカル ログオンを許可  

    -   リモート デスクトップ サービスを使ったログオンを許可する  

4.  監査は、管理者グループのプロパティまたはメンバーシップに何らかの変更が加えられた場合にアラートを送信するように構成する必要があります。  

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-administrators-group"></a>管理者グループからすべてのメンバーを削除するための詳細な手順  

1.  **サーバーマネージャー**で、 **[ツール]** をクリックし、 **[Active Directory ユーザーとコンピューター]** をクリックします。  

2.  Administrators グループからすべてのメンバーを削除するには、次の手順を実行します。  

    1.  **[Administrators]** グループをダブルクリックし、 **[メンバー]** タブをクリックします。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_79.gif)  

    2.  グループのメンバーを選択し、 **[削除]** をクリックして、 **[はい]** をクリックし、 **[OK]** をクリックします。  

3.  管理者グループのすべてのメンバーが削除されるまで、手順 2. を繰り返します。  

#### <a name="step-by-step-instructions-to-secure-administrators-groups-in-active-directory"></a>Active Directory の管理者グループをセキュリティで保護するための詳細な手順  

1.  **サーバーマネージャー**で、 **[ツール]** をクリックし、 **[グループポリシーの管理]** をクリックします。  

2.  コンソールツリーで、[&lt;フォレスト&gt;\ ドメイン\\&lt;ドメイン&gt;] を展開し、**グループポリシーオブジェクト**(&lt;のフォレスト&gt; がフォレストの名前、&lt;ドメイン&gt; がグループポリシーを設定するドメインの名前である) を展開します。  

3.  コンソールツリーで、 **[グループポリシーオブジェクト]** を右クリックし、 **[新規]** をクリックします。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_80.gif)  

4.  **[新しい gpo]** ダイアログボックスで、「<GPO Name>」と入力し、 **[OK]** をクリックします ( *gpo 名*はこの gpo の名前です)。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_81.gif)  

5.  詳細ウィンドウで、 **<GPO Name>** を右クリックし、**編集** をクリックします。  

6.  **Computer Configuration\Policies\Windows** 権利 ポリシー に移動し、**ユーザー権利の割り当て** をクリックします。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_82.gif)  

7.  Administrators グループのメンバーがネットワーク経由でメンバーサーバーとワークステーションにアクセスするのを防ぐために、次の手順を実行してユーザーの権限を構成します。  

    1.  **[ネットワークからこのコンピューターへのアクセスを拒否する]** をダブルクリックし、 **[これらのポリシー設定を定義]** する を選択します。  

    2.  **[ユーザーまたはグループの追加]** をクリックし、 **[参照]** をクリックします。  

    3.  「 **Administrators**」と入力し、 **[名前の確認]** をクリックして、 **[OK]** をクリックします。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_83.gif)  

    4.  **[Ok]** をクリックし、もう一度 [ **ok]** をクリックします。  

8.  次の手順を実行して、Administrators グループのメンバーがバッチジョブとしてログオンしないようにするには、ユーザーの権限を構成します。  

    1.  **[バッチジョブとしてログオンを拒否する]** をダブルクリックし、 **[これらのポリシー設定を定義]** する を選択します。  

    2.  **[ユーザーまたはグループの追加]** をクリックし、 **[参照]** をクリックします。  

    3.  「 **Administrators**」と入力し、 **[名前の確認]** をクリックして、 **[OK]** をクリックします。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_84.gif)  

    4.  **[Ok]** をクリックし、もう一度 [ **ok]** をクリックします。  

9. 次の手順を実行して、Administrators グループのメンバーがサービスとしてログオンしないようにするには、ユーザーの権限を構成します。  

    1.  **[サービスとしてログオンを拒否する]** をダブルクリックし、 **[これらのポリシー設定を定義]** する を選択します。  

    2.  **[ユーザーまたはグループの追加]** をクリックし、 **[参照]** をクリックします。  

    3.  「 **Administrators**」と入力し、 **[名前の確認]** をクリックして、 **[OK]** をクリックします。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_85.gif)  

    4.  **[Ok]** をクリックし、もう一度 [ **ok]** をクリックします。  

10. **グループポリシー管理エディター**を終了するには、 **[ファイル]** をクリックし、 **[終了]** をクリックします。  

11. **グループポリシー管理**で、次の手順に従って、GPO をメンバーサーバーとワークステーションの ou にリンクします。  

    1.  &lt;フォレスト&gt;> \ Domains\\&lt;ドメイン&gt; に移動します (&lt;Forest&gt; はフォレストの名前、&lt;ドメイン&gt; は、グループポリシーを設定するドメインの名前です)。  

    2.  GPO が適用される OU を右クリックし、[既存の**gpo のリンク**] をクリックします。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_86.gif)  

    3.  作成した GPO を選択し、[ **OK]** をクリックします。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_87.gif)  

    4.  ワークステーションが含まれている他のすべての Ou へのリンクを作成します。  

    5.  メンバーサーバーを含む他のすべての Ou へのリンクを作成します。  

        > [!IMPORTANT]  
        > ジャンプサーバーを使用してドメインコントローラーと Active Directory を管理する場合は、この Gpo がリンクされていない OU にジャンプサーバーが配置されていることを確認します。  

        > [!NOTE]  
        > Gpo の Administrators グループに制限を実装すると、Windows は、ドメインの Administrators グループに加えて、コンピューターのローカル管理者グループのメンバーにも設定を適用します。 したがって、Administrators グループに制限を実装する場合は注意が必要です。 管理者グループのメンバーに対するネットワーク、バッチ、およびサービスのログオンを禁止することは、実装が可能な場所であれば、リモートデスクトップサービスによってローカルログオンやログオンを制限しないことをお勧めします。 これらのログオンの種類をブロックすると、ローカルの Administrators グループのメンバーがコンピューターの正当な管理をブロックする可能性があります。  
        >   
        > 次のスクリーンショットは、組み込みのローカルまたはドメインの管理者アカウントの誤用をブロックする構成設定を示しています。 この設定に含めると、ローカルコンピューターの Administrators グループのメンバーであるアカウントのログオンもブロックされるので、 **[リモートデスクトップサービス経由でログオンを拒否**する] ユーザー権利には Administrators グループが含まれていないことに注意してください。 コンピューター上のサービスが、このセクションで説明されている特権グループのいずれかのコンテキストで実行されるように構成されている場合、これらの設定を実装すると、サービスとアプリケーションが失敗する可能性があります。 そのため、このセクションのすべての推奨事項と同様に、環境内の適用性の設定を十分にテストする必要があります。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_88.gif)  

#### <a name="step-by-step-instructions-to-grant-user-rights-to-the-administrators-group"></a>管理者グループにユーザー権限を付与するための詳細な手順  

1.  **サーバーマネージャー**で、 **[ツール]** をクリックし、 **[グループポリシーの管理]** をクリックします。  

2.  コンソールツリーで、<Forest>、ドメイン\\<Domain>の順に展開し、**オブジェクトをグループポリシー**します (<Forest> はフォレストの名前、<Domain> はグループポリシーを設定するドメインの名前です)。  

3.  コンソールツリーで、 **[グループポリシーオブジェクト]** を右クリックし、 **[新規]** をクリックします。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_89.gif)  

4.  **[新しい gpo]** ダイアログボックスで、「<GPO Name>」と入力し、 **[OK]** をクリックします (<GPO Name> はこの gpo の名前です)。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_90.gif)  

5.  詳細ウィンドウで、 **<GPO Name>** を右クリックし、**編集** をクリックします。  

6.  **Computer Configuration\Policies\Windows** 権利 ポリシー に移動し、**ユーザー権利の割り当て** をクリックします。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_91.gif)  

7.  Administrators グループのメンバーがネットワーク経由でドメインコントローラーにアクセスできるようにするには、次の手順を実行します。  

    1.  **[ネットワークからこのコンピューターへのアクセス]** をダブルクリックし、 **[これらのポリシー設定を定義]** する を選択します。  

    2.  **[ユーザーまたはグループの追加]** をクリックし、 **[参照]** をクリックします。  

    3.  **[ユーザーまたはグループの追加]** をクリックし、 **[参照]** をクリックします。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_92.gif)  

    4.  **[Ok]** をクリックし、もう一度 [ **ok]** をクリックします。  

8.  Administrators グループのメンバーがローカルでログオンできるようにするには、次の手順を実行します。  

    1.  **[ローカルログオンを許可する]** をダブルクリックし、 **[これらのポリシー設定を定義]** する を選択します。  

    2.  **[ユーザーまたはグループの追加]** をクリックし、 **[参照]** をクリックします。  

    3.  「 **Administrators**」と入力し、 **[名前]** の確認 をクリックして、 **[OK]** をクリックします。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_93.gif)  

    4.  **[Ok]** をクリックし、もう一度 [ **ok]** をクリックします。  

9. 次の手順を実行して、Administrators グループのメンバーがリモートデスクトップサービスを使用してログオンできるようにするユーザー権限を構成します。  

    1.  [リモートデスクトップサービスの**ログオンを許可する**] をダブルクリックし、[**これらのポリシーの設定を定義**する] を選択します。  

    2.  **[ユーザーまたはグループの追加]** をクリックし、 **[参照]** をクリックします。  

    3.  「 **Administrators**」と入力し、 **[名前の確認]** をクリックして、 **[OK]** をクリックします。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_94.gif)  

    4.  **[Ok]** をクリックし、もう一度 [ **ok]** をクリックします。  

10. **グループポリシー管理エディター**を終了するには、 **[ファイル]** をクリックし、 **[終了]** をクリックします。  

11. **グループポリシー管理**で、次の手順を実行して GPO を DOMAIN controllers OU にリンクします。  

    1.  <Forest>\ Domains\\<Domain> に移動します (<Forest> はフォレストの名前、<Domain> はグループポリシーを設定するドメインの名前です)。  

    2.  ドメインコントローラー OU を右クリックし、**既存の GPO のリンク** をクリックします。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_95.gif)  

    3.  作成した GPO を選択し、[ **OK]** をクリックします。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_96.gif)  

#### <a name="verification-steps"></a>検証手順  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>[ネットワークからこのコンピューターへのアクセスを拒否する] GPO 設定を確認する  
GPO の変更 ("ジャンプサーバー" など) の影響を受けていないメンバーサーバーまたはワークステーションから、GPO の変更の影響を受けるネットワーク経由でメンバーサーバーまたはワークステーションにアクセスしようとします。 GPO 設定を確認するには、 **NET use**コマンドを使用してシステムドライブをマップします。  

1.  Administrators グループのメンバーであるアカウントを使用してローカルにログオンします。  

2.  マウスを使用して、画面の右上隅または右下隅にポインターを移動します。 **Charms**バーが表示されたら、 **[検索]** をクリックします。  

3.  **検索**ボックスに「**コマンドプロンプト**」と入力し、 **[コマンドプロンプト]** を右クリックします。次に、 **[管理者として実行]** をクリックして、管理者特権でのコマンドプロンプトを開きます。  

4.  昇格の承認を求めるメッセージが表示されたら、[**はい]** をクリックします。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_97.gif)  

5.  **コマンドプロンプト**ウィンドウで、「 **net use \\\\\<サーバー名\>\c $** 」と入力します。ここで、\<server Name\> は、ネットワーク経由でアクセスしようとしているメンバーサーバーまたはワークステーションの名前です。  

6.  次のスクリーンショットは、表示する必要があるエラーメッセージを示しています。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_98.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"バッチジョブとしてログオンを拒否する" GPO 設定を確認する  
GPO の変更の影響を受けたメンバーサーバーまたはワークステーションから、ローカルにログオンします。  

###### <a name="create-a-batch-file"></a>バッチファイルを作成する  

1.  マウスを使用して、画面の右上隅または右下隅にポインターを移動します。 **Charms**バーが表示されたら、 **[検索]** をクリックします。  

2.  **検索**ボックスに「 **notepad**」と入力し、 **[notepad]** をクリックします。  

3.  **メモ帳**で、「 **dir c:** 」と入力します。  

4.  **[ファイル]** をクリックし、 **[名前を付けて保存]** をクリックします。  

5.  **[ファイル名]** フィールドに、「<Filename>」と入力し**ます**(<Filename> は新しいバッチファイルの名前です)。  

###### <a name="schedule-a-task"></a>タスクのスケジュール設定  

1.  マウスを使用して、画面の右上隅または右下隅にポインターを移動します。 **Charms**バーが表示されたら、 **[検索]** をクリックします。  

2.  **検索**ボックスに「 **task scheduler**」と入力し、 **[タスクスケジューラ]** をクリックします。  

    > [!NOTE]  
    > Windows 8 を実行しているコンピューターの場合は、[検索] ボックスに「スケジュールタスク」と入力し、[タスクのスケジュール] をクリックします。  

3.  **[アクション]** をクリックし、 **[タスクの作成]** をクリックします。  

4.  **[タスクの作成]** ダイアログボックスで、「 **<Task Name>** 」と入力します (<Task Name> は新しいタスクの名前です)。  

5.  **[操作]** タブをクリックし、 **[新規作成]** をクリックします。  

6.  **[アクション]** フィールドで、 **[プログラムの開始]** を選択します。  

7.  **[プログラム/スクリプト]** フィールドの **[参照]** をクリックし、 **[バッチファイルの作成]** セクションで作成したバッチファイルを探して選択し、 **[開く]** をクリックします。  

8.  **[OK]** をクリックします。  

9. **[全般]** タブをクリックします。  

10. **[セキュリティオプション]** フィールドで、 **[ユーザーまたはグループの変更]** をクリックします。  

11. Administrators グループのメンバーであるアカウントの名前を入力し、名前の **[確認]** をクリックして、 **[OK]** をクリックします。  

12. [**ユーザーがログオンしているかどうかにかかわら**ず、**パスワードを保存**しない] を選択します。 タスクは、ローカルコンピューターのリソースにのみアクセスできます。  

13. **[OK]** をクリックします。  

14. タスクを実行するためのユーザーアカウントの資格情報を要求するダイアログボックスが表示されます。  

15. パスワードを入力したら、[ **OK]** をクリックします。  

16. 次のようなダイアログボックスが表示されます。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_99.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>"サービスとしてログオンを拒否する" GPO 設定を確認する  

1.  GPO の変更の影響を受けたメンバーサーバーまたはワークステーションから、ローカルにログオンします。  

2.  マウスを使用して、画面の右上隅または右下隅にポインターを移動します。 **Charms**バーが表示されたら、 **[検索]** をクリックします。  

3.  **検索**ボックスに「**サービス**」と入力し、 **[サービス]** をクリックします。  

4.  **[印刷スプーラ]** を見つけてダブルクリックします。  

5.  **[ログオン]** タブをクリックします。  

6.  **[ログオン]** の方法 フィールドで、 **[このアカウント]** を選択します。  

7.  **[参照]** をクリックして、Administrators グループのメンバーであるアカウントの名前を入力し、 **[名前の確認]** をクリックして、 **[OK]** をクリックします。  

8.  **[パスワード]** フィールドと **[パスワードの確認]** 入力 フィールドに、選択したアカウントのパスワードを入力し、[ **OK]** をクリックします。  

9. [ **OK]** を3回クリックします。  

10. **[印刷スプーラ]** を右クリックし、 **[再起動]** をクリックします。  

11. サービスを再起動すると、次のようなダイアログボックスが表示されます。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_100.png)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>プリンタスプーラサービスへの変更を元に戻す  

1.  GPO の変更の影響を受けたメンバーサーバーまたはワークステーションから、ローカルにログオンします。  

2.  マウスを使用して、画面の右上隅または右下隅にポインターを移動します。 **Charms**バーが表示されたら、 **[検索]** をクリックします。  

3.  **検索**ボックスに「**サービス**」と入力し、 **[サービス]** をクリックします。  

4.  **[印刷スプーラ]** を見つけてダブルクリックします。  

5.  **[ログオン]** タブをクリックします。  

6.  **[ログオン]** の方法 フィールドで、 **[ローカルシステム]** アカウント をクリックし、 **[OK]** をクリックします。  
