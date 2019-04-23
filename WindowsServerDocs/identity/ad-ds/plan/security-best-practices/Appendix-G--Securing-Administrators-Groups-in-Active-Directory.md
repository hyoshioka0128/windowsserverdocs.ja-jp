---
ms.assetid: 4baefbd3-038f-44c0-85ba-f24e9722b757
title: '付録 G: Active Directory の管理者グループのセキュリティ保護'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2912dfc534d751d4aa121d238dffc36c07562d76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882713"
---
# <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>付録 G :Active Directory の管理者グループのセキュリティ保護

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012


## <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>付録 G :Active Directory の管理者グループのセキュリティ保護  
Enterprise Admins (EA) とドメイン管理者 (DA) グループと同様に、組み込みの管理者 (BA) グループのメンバーシップはビルドまたはディザスター リカバリー シナリオでのみ必要な必要があります。 ありません日常的なユーザー アカウント、ドメインのビルトイン Administrator アカウントを除く、Administrators グループが」の説明に従って設定された場合[付録 d:Active Directory でビルトイン Administrator アカウントを保護する](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)します。  

管理者は、既定では、ほとんどのそれぞれのドメイン内の AD DS オブジェクトの所有者です。 このグループのメンバーシップは、所有権や、オブジェクトの所有権を取得する権限が必要なビルドまたはディザスター リカバリーのシナリオにおいて必要があります。 さらに、DAs と EAs は、お客様の権利と、Administrators グループの既定のメンバーシップに基づいてアクセス許可の数を継承します。 Active Directory で権限を持つグループの入れ子の既定のグループを変更しないでください、およびステップ バイ ステップの手順が記載されたは、各ドメインの管理者グループをセキュリティで保護する必要があります。  

フォレスト内の各ドメインで管理者グループ。  

1.  」の説明に従ってように保護されている、ドメインのビルトイン Administrator アカウントのような例外、Administrators グループからすべてのメンバーを削除[付録 d:Active Directory でビルトイン Administrator アカウントを保護する](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)します。  

2.  次のユーザー権限がメンバー サーバーと各ドメインにワークステーションを含む Ou にリンクされた、Gpo で DA グループを追加する必要があります**コンピューター \policies\windows 設定 \ セキュリティ \ Policies\ ユーザー権限割り当て**:  

    -   ネットワークからのこのコンピューターへのアクセスを拒否する  

    -   バッチ ジョブとしてのログオンを拒否  

    -   サービスとしてのログオンを拒否  

3.  ドメイン コント ローラーで、フォレスト内の各ドメインの OU で、Administrators グループが権限を付与する次ユーザー。  

    -   ネットワークからこのコンピューターにアクセスする  

    -   ローカル ログオンを許可  

    -   リモート デスクトップ サービスを使ったログオンを許可する  

4.  プロパティまたは Administrators グループのメンバーシップに変更を行った場合にアラートを送信するは、監査を構成する必要があります。  

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-administrators-group"></a>Administrators グループからすべてのメンバーを削除するための手順  

1.  **サーバー マネージャー**、 をクリックして**ツール**、 をクリック**Active Directory ユーザーとコンピューター**します。  

2.  Administrators グループからすべてのメンバーを削除するには、次の手順を実行します。  

    1.  ダブルクリックして、**管理者**をグループ化し、をクリックして、**メンバー**タブ。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_79.gif)  

    2.  グループのメンバーを選択して、**削除**、 をクリックして**はい**、 をクリック**ok**します。  

3.  Administrators グループのすべてのメンバーが削除されるまで、手順 2. を繰り返します。  

#### <a name="step-by-step-instructions-to-secure-administrators-groups-in-active-directory"></a>Active Directory の管理者グループをセキュリティで保護するための手順  

1.  **サーバー マネージャー**、 をクリックして**ツール**、 をクリック**Group Policy Management**します。  

2.  コンソール ツリーで、展開&lt;フォレスト&gt;\Domains\\&lt;ドメイン&gt;、し**グループ ポリシー オブジェクト**(場所&lt;フォレスト&gt;が、フォレストの名前と&lt;ドメイン&gt;はグループ ポリシーを設定するドメインの名前です)。  

3.  コンソール ツリーで、右クリック**グループ ポリシー オブジェクト**、 をクリック**新規**します。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_80.gif)  

4.  **新しい GPO**ダイアログ ボックスに「 <GPO Name>、 をクリック**OK** (場所*GPO 名*この GPO 名前を指定)。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_81.gif)  

5.  詳細ペインで右クリックして**<GPO Name>**、 をクリック**編集**します。  

6.  移動します**コンピューター \policies\windows \security settings \local Policies**、 をクリック**ユーザー権利の割り当て**します。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_82.gif)  

7.  Administrators グループのメンバーが次の手順に従って、ネットワーク経由でメンバー サーバーとワークステーションにアクセスすることを防ぐためにユーザー権限を構成します。  

    1.  ダブルクリック**ネットワークからこのコンピューターへのアクセスを拒否**選択と**これらのポリシー設定を定義**。  

    2.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

    3.  型**管理者**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_83.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

8.  Administrators グループのメンバーが、次の手順を実行してバッチ ジョブとしてログオンするを防ぐためにユーザー権限を構成します。  

    1.  ダブルクリック**バッチ ジョブとしてログオンを拒否**選択と**これらのポリシー設定を定義**。  

    2.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

    3.  型**管理者**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_84.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

9. Administrators グループのメンバーが次の手順に従って、サービスとしてログオンするを防ぐためにユーザー権限を構成します。  

    1.  ダブルクリック**サービスとしてログオンを拒否**選択と**これらのポリシー設定を定義**します。  

    2.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

    3.  型**管理者**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_85.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

10. 終了する**グループ ポリシー管理エディター**、 をクリックして**ファイル**、 をクリック**終了**します。  

11. **Group Policy Management**次の手順に従って、メンバー サーバーとワークステーションの Ou に GPO をリンクします。  

    1.  移動します、&lt;フォレスト&gt;> \Domains\\&lt;ドメイン&gt;(場所&lt;フォレスト&gt;フォレストの名前を指定し、&lt;ドメイン&gt;名前を指定しますドメインのグループ ポリシーを設定する)。  

    2.  GPO に適用され、をクリックする OU を右クリックして**既存の GPO をリンク**します。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_86.gif)  

    3.  先ほど作成した GPO を選択し、クリックして**OK**します。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_87.gif)  

    4.  ワークステーションが含まれているその他のすべての Ou へのリンクを作成します。  

    5.  メンバー サーバーを含むその他のすべての Ou へのリンクを作成します。  

        > [!IMPORTANT]  
        > ジャンプ サーバーをドメイン コント ローラーと Active Directory の管理に使用する場合は、ジャンプ サーバーが Gpo がリンクされていないこの OU 内にあることを確認します。  

        > [!NOTE]  
        > Gpo 内の管理者グループに制限を実装すると、Windows は、ドメインの管理者グループだけでなく、コンピューターのローカルの Administrators グループのメンバーに、設定を適用します。 したがって、Administrators グループの制限を実装するときに注意を使用する必要があります。 ローカル ログオンまたはリモート デスクトップ サービス経由のログオンが、Administrators グループのメンバーは、ネットワーク、バッチ、およびサービスのログオンを禁止するには、任意の場所が実装可能なことをお勧めは制限されません。 これらのログオンの種類をブロックしているローカルの Administrators グループのメンバーごとのコンピュータの正当な管理をブロックできます。  
        >   
        > 次のスクリーン ショットがローカルの組み込みの不正使用をブロックする構成設定を表示し、ドメイン管理者アカウントのローカルまたはドメインのビルトイン管理者グループの不正使用だけでなくします。 なお、**リモート デスクトップ サービスを使ったログオンを拒否する**ローカル コンピューターのメンバーであるアカウントのこれらのログオンもブロックはこの設定に含めるために、ユーザー権限で、Administrators グループが含まれません管理者グループ。 このセクションで説明されている権限を持つグループのいずれかのコンテキストで実行するコンピューター上のサービスが構成される場合は、サービスとアプリケーションの失敗を生成してこれらの設定を実装できます。 そのため、すべてがのこのセクションでは、推奨事項には、必ず十分なテスト設定の適用性の環境内でします。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_88.gif)  

#### <a name="step-by-step-instructions-to-grant-user-rights-to-the-administrators-group"></a>Grant ユーザー権限を管理者グループにする手順  

1.  **サーバー マネージャー**、 をクリックして**ツール**、 をクリック**Group Policy Management**します。  

2.  コンソール ツリーで、展開<Forest>\Domains\\<Domain>、し**グループ ポリシー オブジェクト**(場所<Forest>フォレストの名前を指定および<Domain>先ドメインの名前を指定しますグループ ポリシーの設定)。  

3.  コンソール ツリーで、右クリック**グループ ポリシー オブジェクト**、 をクリック**新規**します。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_89.gif)  

4.  **新しい GPO**ダイアログ ボックスに「 <GPO Name>、 をクリック**OK** (場所<GPO Name>この GPO の名前を指定します)。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_90.gif)  

5.  詳細ペインで右クリックして**<GPO Name>**、 をクリック**編集**します。  

6.  移動します**コンピューター \policies\windows \security settings \local Policies**、 をクリック**ユーザー権利の割り当て**します。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_91.gif)  

7.  次の手順に従って、ネットワーク経由でアクセスのドメイン コント ローラーに Administrators グループのメンバーを許可するユーザーの権限を構成します。  

    1.  ダブルクリック**ネットワークからこのコンピューターへのアクセス**選択と**これらのポリシー設定を定義**。  

    2.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

    3.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_92.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

8.  Administrators グループのメンバーは、次の手順に従って、ローカルでログオンを許可するユーザーの権限を構成します。  

    1.  ダブルクリック**ローカル ログオンを許可する**選択と**これらのポリシー設定を定義**。  

    2.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

    3.  型**管理者**、確認 をクリックして**名**、 をクリック**OK**します。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_93.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

9. Administrators グループのメンバーは、次の手順に従って、リモート デスクトップ サービス経由でログオンを許可するユーザーの権限を構成します。  

    1.  ダブルクリック**リモート デスクトップ サービスを使ったログオンを許可する**選択**これらのポリシー設定を定義**します。  

    2.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

    3.  型**管理者**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_94.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

10. 終了する**グループ ポリシー管理エディター**、 をクリックして**ファイル**、 をクリック**終了**します。  

11. **Group Policy Management**次の手順に従って、ドメイン コント ローラー OU に GPO をリンクします。  

    1.  移動します、 <Forest>\Domains\\ <Domain> (場所<Forest>フォレストの名前を指定し、<Domain>グループ ポリシーを設定するドメインの名前を指定)。  

    2.  ドメイン コント ローラー をクリックし、OU を右クリックして**既存の GPO をリンク**します。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_95.gif)  

    3.  先ほど作成した GPO を選択し、クリックして**OK**します。  

        ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_96.gif)  

#### <a name="verification-steps"></a>検証手順  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>アクセスを拒否をこのコンピューターにネットワークから"GPO の設定を確認します。  
メンバー サーバーまたはワークステーション (「ジャンプ サーバー」) など、GPO の変更の影響を受けませんからには、メンバー サーバーまたはワークステーションを GPO の変更によって影響を受けるネットワーク経由でアクセスしてみます。 GPO の設定を確認するにマップしようとする、システム ドライブを使用して、 **NET USE**コマンド。  

1.  使用してローカルの Administrators グループのメンバーであるアカウントでログインします。  

2.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

3.  **検索**ボックスに「**コマンド プロンプト**、右クリックして**コマンド プロンプト**順にクリックします**管理者として実行**を管理者特権でを開くコマンド プロンプト。  

4.  昇格を承認するメッセージが表示されたら、クリックして**はい**します。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_97.gif)  

5.  **コマンド プロンプト**ウィンドウで、「 **net \\ \\\<サーバー名\>\c$** ここで、\<サーバー名\>が、メンバー サーバーまたはネットワーク経由でアクセスしようとしているワークステーションの名前。  

6.  次のスクリーン ショットには、表示されるエラー メッセージが表示されます。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_98.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>「バッチ ジョブとしてのログオンを拒否」GPO の設定を確認します。  
任意のメンバー サーバーまたは GPO の変更によって影響を受けるワークステーションからローカルでログオンします。  

###### <a name="create-a-batch-file"></a>バッチ ファイルを作成します。  

1.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

2.  **検索**ボックスに「**メモ帳** をクリック**メモ帳**します。  

3.  **メモ帳**、型**dir c:** します。  

4.  クリックして**ファイル**、 をクリック**名前を付けて保存**します。  

5.  **ファイル名**フィールドに「  **<Filename>.bat** (場所<Filename>新しいバッチ ファイルの名前です).  

###### <a name="schedule-a-task"></a>タスクをスケジュールします。  

1.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

2.  **検索**ボックスに「**タスク スケジューラ** をクリック**タスク スケジューラ**します。  

    > [!NOTE]  
    > 検索ボックスに、Windows 8 を実行するコンピューターでタスクのスケジュール設定を入力し、[タスクのスケジュール設定] をクリックします。  

3.  クリックして**アクション**、 をクリック**タスクの作成**です。  

4.  **タスクの作成**ダイアログ ボックスに「 **<Task Name>** (場所<Task Name>新しいタスク名前を指定します).  

5.  をクリックして、**アクション**タブをクリックし、をクリックして**新規**します。  

6.  **アクション**フィールドで、**プログラムを起動する**します。  

7.  **プログラム/スクリプト**フィールドに、をクリックして**参照**を検索して選択で作成したバッチ ファイル、**バッチ ファイルを作成**セクションをクリックします**を開く**.  

8.  **[OK]** をクリックします。  

9. **[全般]** タブをクリックします。  

10. **セキュリティ オプション**フィールドに、をクリックして**変更ユーザーまたはグループ**します。  

11. Administrators グループのメンバーであるアカウントの名前を入力**名前の確認**、 をクリック**OK**します。  

12. 選択**ユーザーがログに記録された青いでないかどうかを実行**と**パスワードを保存しない**します。 タスクは、ローカル コンピューターのリソースへのアクセスを必要のみがあります。  

13. **[OK]** をクリックします。  

14. タスクを実行する資格情報要求のユーザー アカウント ダイアログ ボックスが表示されます。  

15. パスワードを入力すると、次のようにクリックします。 **OK**します。  

16. 次のようなダイアログ ボックスが表示されます。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_99.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>「サービスとしてのログオンを拒否」GPO の設定を確認します。  

1.  任意のメンバー サーバーまたは GPO の変更によって影響を受けるワークステーションからローカルでログオンします。  

2.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

3.  **検索**ボックスに「**サービス**、 をクリック**サービス**します。  

4.  見つけてダブルクリック**印刷スプーラー**します。  

5.  **[ログオン]** タブをクリックします。  

6.  **としてログオン**フィールドで、**このアカウント**します。  

7.  をクリックして**参照**、Administrators グループのメンバーであるアカウントの名前を入力、 をクリックして**名前の確認**、 をクリック**OK**。  

8.  **パスワード**と**パスワードの確認入力**フィールドは、選択したアカウントのパスワードを入力し、をクリックして**OK**します。  

9. クリックして**OK** 3 回です。  

10. 右クリック**印刷スプーラー**クリック**再起動**。  

11. サービスが再起動されると、次のようなダイアログ ボックスが表示されます。  

    ![セキュリティで保護された管理グループ](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_100.png)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>プリンタ スプーラ サービスへの変更を元に戻す  

1.  任意のメンバー サーバーまたは GPO の変更によって影響を受けるワークステーションからローカルでログオンします。  

2.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

3.  **検索**ボックスに「**サービス**、 をクリック**サービス**します。  

4.  見つけてダブルクリック**印刷スプーラー**します。  

5.  **[ログオン]** タブをクリックします。  

6.  **としてログオン**フィールドに、をクリックして**ローカル システム**アカウント、およびクリックして **[ok]** します。  
