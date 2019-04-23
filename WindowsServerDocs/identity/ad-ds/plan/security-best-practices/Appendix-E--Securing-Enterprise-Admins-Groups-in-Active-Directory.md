---
ms.assetid: f643099e-f9c6-476f-9378-5a9228c39b33
title: 付録 E - Active Directory の Enterprise Admins グループのセキュリティ保護
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 976eb8c7159c8349b72bee05a5248b5cc116d96b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856723"
---
# <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>付録 E:Active Directory の Enterprise Admins グループのセキュリティ保護

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012


## <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>付録 E:Active Directory の Enterprise Admins グループのセキュリティ保護  
Enterprise Admins (EA) グループは、フォレスト ルート ドメインに格納されているが、含める必要がありますいないルート ドメインの管理者アカウントのような例外を日常的にユーザー」の説明に従って、セキュリティで保護が提供される[付録 d:Active Directory でビルトイン Administrator アカウントを保護する](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)します。  

エンタープライズ管理者は、既定では、フォレスト内の各ドメインで Administrators グループのメンバーです。 フォレスト ディザスター リカバリーのシナリオが発生した場合 EA 権限が必要になるため、各ドメインの管理者グループから、EA のグループを削除する必要がありますできません。 フォレストの Enterprise Admins グループがセキュリティで保護する必要がある次のステップ バイ ステップの手順で説明されています。  

フォレストの Enterprise Admins グループ。  

1.  次のユーザー権利をメンバー サーバーと各ドメインにワークステーションを含む Ou にリンクされている Gpo、Enterprise Admins グループを追加する必要があります**コンピューター \policies\windows 設定 \ セキュリティ \ Policies\ユーザー権利の割り当て**:  

    -   ネットワークからのこのコンピューターへのアクセスを拒否する  

    -   バッチ ジョブとしてのログオンを拒否  

    -   サービスとしてのログオンを拒否  

    -   ローカル ログオンを拒否  

    -   リモート デスクトップ サービスを使ったログオンを拒否  

2.  プロパティまたは Enterprise Admins グループのメンバーシップに変更を行った場合にアラートを送信する監査を構成します。  

### <a name="step-by-step-instructions-for-removing-all-members-from-the-enterprise-admins-group"></a>Enterprise Admins グループからすべてのメンバーを削除するための手順  

1.  **サーバー マネージャー**、 をクリックして**ツール**、 をクリック**Active Directory ユーザーとコンピューター**します。  

2.  コンソール ツリーで、フォレスト ルート ドメインを管理していない場合は右クリック<Domain>、 をクリックし、**ドメインの変更**(場所<Domain>現在管理しているドメインの名前を指定します)。  

    ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_43.gif)  

3.  **ドメインの変更**ダイアログ ボックスで、をクリックして**参照**、フォレスト ルート ドメインを選択して、クリックして **[ok]** します。  

    ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_44.gif)  

4.  EA グループからすべてのメンバーを削除します。  

    1.  ダブルクリックして、 **Enterprise Admins**をグループ化し、をクリックし、**メンバー**  タブ。  

        ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_45.gif)  

    2.  グループのメンバーを選択して、**削除**、 をクリックして**はい**、 をクリック**ok**します。  

5.  EA のグループのすべてのメンバーが削除されるまで、手順 2. を繰り返します。  

### <a name="step-by-step-instructions-to-secure-enterprise-admins-in-active-directory"></a>Active Directory の Enterprise Admins をセキュリティで保護するための手順  

1.  **サーバー マネージャー**、 をクリックして**ツール**、 をクリック**Group Policy Management**します。  

2.  コンソール ツリーで、展開<Forest>\Domains\\<Domain>、し**グループ ポリシー オブジェクト**(場所<Forest>フォレストの名前を指定および<Domain>先ドメインの名前を指定しますグループ ポリシーの設定)。  

    > [!NOTE]  
    > 複数のドメインを含むフォレストでのような GPO は、Enterprise Admins グループのセキュリティで保護することが必要な各ドメインで作成されます。  

3.  コンソール ツリーで、右クリック**グループ ポリシー オブジェクト**、 をクリック**新規**します。  

    ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_46.gif)  

4.  **新しい GPO**ダイアログ ボックスに「 <GPO Name>、 をクリック**OK** (場所<GPO Name>この GPO の名前を指定します)。  

    ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_47.gif)  

5.  詳細ペインで右クリックして<GPO Name>、 をクリック**編集**します。  

6.  移動します**コンピューター \policies\windows \security settings \local Policies**、 をクリック**ユーザー権利の割り当て**します。  

    ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_48.gif)  

7.  Enterprise Admins グループのメンバーが次の手順に従って、ネットワーク経由でメンバー サーバーとワークステーションにアクセスすることを防ぐためにユーザー権限を構成します。  

    1.  ダブルクリック**ネットワークからこのコンピューターへのアクセスを拒否**選択と**これらのポリシー設定を定義**。  

    2.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

    3.  型**Enterprise Admins**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_49.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

8.  Enterprise Admins グループのメンバーが、次の手順を実行してバッチ ジョブとしてログオンするを防ぐためにユーザー権限を構成します。  

    1.  ダブルクリック**バッチ ジョブとしてログオンを拒否**選択と**これらのポリシー設定を定義**。  

    2.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

        > [!NOTE]  
        > 複数のドメインを含むフォレストで次のようにクリックします。**場所**フォレストのルート ドメインを選択します。  

    3.  型**Enterprise Admins**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_50.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

9. EA のグループのメンバーが次の手順に従って、サービスとしてログオンするを防ぐためにユーザー権限を構成します。  

    1.  ダブルクリック**サービスとしてのログオンを拒否**選択**これらのポリシー設定を定義**します。  

    2.  クリックして**追加のユーザーまたはグループ**順にクリックします**参照**します。  

        > [!NOTE]  
        > 複数のドメインを含むフォレストで次のようにクリックします。**場所**フォレストのルート ドメインを選択します。  

    3.  型**Enterprise Admins**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_51.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

10. ローカルでログオン メンバー サーバーとワークステーションに、次の手順を実行してから、Enterprise Admins グループのメンバーを防ぐためにユーザーの権限を構成します。  

    1.  ダブルクリック**ローカル ログオンを拒否する**選択**これらのポリシー設定を定義**。  

    2.  クリックして**追加のユーザーまたはグループ**順にクリックします**参照**します。  

        > [!NOTE]  
        > 複数のドメインを含むフォレストで次のようにクリックします。**場所**フォレストのルート ドメインを選択します。  

    3.  型**Enterprise Admins**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_52.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

11. Enterprise Admins グループのメンバーが、次の手順でメンバー サーバーとリモート デスクトップ サービスを使用してワークステーションにアクセスすることを防ぐためにユーザー権限を構成します。  

    1.  ダブルクリック**リモート デスクトップ サービスを使ったログオンを拒否する**選択**これらのポリシー設定を定義**。  

    2.  クリックして**追加のユーザーまたはグループ**順にクリックします**参照**します。  

        > [!NOTE]  
        > 複数のドメインを含むフォレストで次のようにクリックします。**場所**フォレストのルート ドメインを選択します。  

    3.  型**Enterprise Admins**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_53.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

12. 終了する**グループ ポリシー管理エディター**、 をクリックして**ファイル**、 をクリック**終了**します。  

13. **Group Policy Management**次の手順に従って、メンバー サーバーとワークステーションの Ou に GPO をリンクします。  

    1.  移動します、 <Forest>\Domains\\ <Domain> (場所<Forest>フォレストの名前を指定し、<Domain>グループ ポリシーを設定するドメインの名前を指定)。  

    2.  GPO に適用され、をクリックする OU を右クリックして**既存の GPO をリンク**します。  

        ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_54.gif)  

    3.  先ほど作成した GPO を選択し、クリックして**OK**します。  

        ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_55.gif)  

    4.  ワークステーションが含まれているその他のすべての Ou へのリンクを作成します。  

    5.  メンバー サーバーを含むその他のすべての Ou へのリンクを作成します。  

    6.  複数のドメインを含むフォレストでのような GPO は、Enterprise Admins グループのセキュリティで保護することが必要な各ドメインで作成されます。  

> [!IMPORTANT]  
> ジャンプ サーバーをドメイン コント ローラーと Active Directory の管理に使用する場合は、ジャンプ サーバーが Gpo がリンクされていないこの OU 内にあることを確認します。  

### <a name="verification-steps"></a>検証手順  

#### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>アクセスを拒否をこのコンピューターにネットワークから"GPO の設定を確認します。  
メンバー サーバーまたはワークステーション (「ジャンプ サーバー」) など、GPO の変更の影響を受けませんからには、メンバー サーバーまたはワークステーションを GPO の変更によって影響を受けるネットワーク経由でアクセスしてみます。 GPO の設定を確認するにマップしようとする、システム ドライブを使用して、 **NET USE**コマンドで、次の手順を実行します。  

1.  EA のグループのメンバーであるアカウントをローカルでログオンします。  

2.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

3.  **検索**ボックスに「**コマンド プロンプト**、右クリックして**コマンド プロンプト**順にクリックします**管理者として実行**を管理者特権でを開くコマンド プロンプト。  

4.  昇格を承認するメッセージが表示されたら、クリックして**はい**します。  

    ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_56.gif)  

5.  **コマンド プロンプト**ウィンドウで、「 **net \\ \\\<サーバー名\>\c$** ここで、\<サーバー名\>が、メンバー サーバーまたはネットワーク経由でアクセスしようとしているワークステーションの名前。  

6.  次のスクリーン ショットには、表示されるエラー メッセージが表示されます。  

    ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_57.gif)  

#### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>「バッチ ジョブとしてのログオンを拒否」GPO の設定を確認します。  

任意のメンバー サーバーまたは GPO の変更によって影響を受けるワークステーションからローカルでログオンします。  

##### <a name="create-a-batch-file"></a>バッチ ファイルを作成します。  

1.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

2.  **検索**ボックスに「**メモ帳** をクリック**メモ帳**します。  

3.  **メモ帳**、型**dir c:** します。  

4.  クリックして**ファイル**、 をクリック**名前を付けて保存**します。  

5.  **ファイル**名 ボックスに「  **<Filename>.bat** (場所<Filename>新しいバッチ ファイルの名前です).  

##### <a name="schedule-a-task"></a>タスクをスケジュールします。  

1.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

2.  **検索**ボックスに「**タスク スケジューラ** をクリック**タスク スケジューラ**します。  

    > [!NOTE]  
    > 実行しているコンピューター、Windows 8 で、**検索**ボックスに「**タスクのスケジュール**、 をクリック**タスクのスケジュール**します。  

3.  クリックして**アクション**、 をクリック**タスクの作成**です。  

4.  **タスクの作成**ダイアログ ボックスに「 **<Task Name>** (場所<Task Name>新しいタスク名前を指定します).  

5.  をクリックして、**アクション**タブをクリックし、をクリックして**新規**します。  

6.  **アクション**フィールドで、**プログラムを起動する**します。  

7.  [**プログラム/スクリプト**、] をクリックして**参照**を検索して選択で作成したバッチ ファイル、**バッチ ファイルを作成**セクションをクリックします**を開く**.  

8.  **[OK]** をクリックします。  

9. **[全般]** タブをクリックします。  

10. **セキュリティ オプション**フィールドに、をクリックして**変更ユーザーまたはグループ**します。  

11. EAs のグループのメンバーであるアカウントの名前を入力**名前の確認**、 をクリック**OK**します。  

12. 選択 **、ユーザーがログオンしているかどうかにかかわらず実行**選択と**パスワードを保存しない**。 タスクは、ローカル コンピューターのリソースへのアクセスを必要のみがあります。  

13. **[OK]** をクリックします。  

14. タスクを実行する資格情報要求のユーザー アカウント ダイアログ ボックスが表示されます。  

15. 資格情報を入力すると、次のようにクリックします。 **OK**します。  

16. 次のようなダイアログ ボックスが表示されます。  

    ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_58.gif)  

#### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>「サービスとしてのログオンを拒否」GPO の設定を確認します。  

1.  任意のメンバー サーバーまたは GPO の変更によって影響を受けるワークステーションからローカルでログオンします。  

2.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

3.  **検索**ボックスに「**サービス**、 をクリック**サービス**します。  

4.  見つけてダブルクリック**印刷スプーラー**します。  

5.  **[ログオン]** タブをクリックします。  

6.  **としてログオン**、**このアカウント**します。  

7.  をクリックして**参照**、EAs グループのメンバーであるアカウントの名前を入力、 をクリックして**名前の確認**、 をクリック**OK**。  

8.  **パスワード:** と**パスワードの確認入力**、選択したアカウントのパスワードを入力し、をクリックして**OK**します。  

9. クリックして**OK** 3 回です。  

10. 右クリックし、**印刷スプーラー**サービスし、選択**再起動**します。  

11. サービスが再起動されると、次のようなダイアログ ボックスが表示されます。  

    ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_59.gif)  

#### <a name="revert-changes-to-the-printer-spooler-service"></a>プリンタ スプーラ サービスへの変更を元に戻す  

1.  任意のメンバー サーバーまたは GPO の変更によって影響を受けるワークステーションからローカルでログオンします。  

2.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

3.  **検索**ボックスに「**サービス**、 をクリック**サービス**します。  

4.  見つけてダブルクリック**印刷スプーラー**します。  

5.  **[ログオン]** タブをクリックします。  

6.  **としてログオン**を選択、**ローカル システム**アカウント、およびクリックして**ok**。  

#### <a name="verify-deny-log-on-locally-gpo-settings"></a>「ローカル ログオンを拒否」GPO の設定を確認します。  

1.  すべてのメンバー サーバーまたはワークステーション、GPO の変更によって影響を受けるには、EA のグループのメンバーであるアカウントを使用してローカルでログオンを試みます。 次のようなダイアログ ボックスが表示されます。  

    ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_60.gif)  

#### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>「リモート デスクトップ サービス経由でログオンを拒否」GPO の設定を確認します。  

1.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

2.  **検索**ボックスに「**リモート デスクトップ接続**、 をクリックし、**リモート デスクトップ接続**します。  

3.  **コンピューター**フィールドへの接続をクリックしたいコンピューターの名前を入力**Connect**します。 (入力することできますもコンピューター名の代わりに IP アドレスです。)  

4.  入力を求められたら、EA グループのメンバーであるアカウントの資格情報を提供します。  

5.  次のようなダイアログ ボックスが表示されます。  

    ![セキュリティで保護されたエンタープライズ管理者グループ](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_61.gif)  
