---
ms.assetid: 017b88a6-f29b-4787-99b6-b5c8eaf8c3df
title: '付録 F: Active Directory の Domain Admins グループのセキュリティ保護'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1f35503d1f02d616255c067fbc1750a0cab974cc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880143"
---
# <a name="appendix-f-securing-domain-admins-groups-in-active-directory"></a>付録 F:Active Directory の Domain Admins グループのセキュリティ保護

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012


## <a name="appendix-f-securing-domain-admins-groups-in-active-directory"></a>付録 F:Active Directory の Domain Admins グループのセキュリティ保護  
Enterprise Admins (EA) グループと同様に、ドメイン管理者 (DA) グループのメンバーシップはビルドまたはディザスター リカバリー シナリオでのみ必要な必要があります。 ありません日常的なユーザー アカウント、ドメインのビルトイン Administrator アカウントを除く DA グループが」の説明に従って設定された場合[付録 d:Active Directory でビルトイン Administrator アカウントを保護する](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)します。  

ドメイン管理者は、既定では、すべてのメンバー サーバーと、それぞれのドメイン内のワークステーションにローカルの Administrators グループのメンバーです。 この既定の入れ子はサポート性とディザスター リカバリーのための変更しないでください。 Domain Admins がメンバー サーバー上のローカルの Administrators グループから削除された場合は、各メンバー サーバーとドメインのワークステーションの管理者グループにグループを追加する必要があります。 各ドメインの Domain Admins グループは、次のステップ バイ ステップの手順」の説明に従って、セキュリティで保護する必要があります。  

フォレスト内の各ドメインの Domain Admins グループ。  

1.  」の説明に従ってように保護されている、ドメインのビルトイン Administrator アカウントのような例外グループからすべてのメンバーを削除[付録 d:Active Directory でビルトイン Administrator アカウントを保護する](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)します。  

2.  次のユーザー権限がメンバー サーバーと各ドメインにワークステーションを含む Ou にリンクされた、Gpo で DA グループを追加する必要があります**コンピューター \policies\windows 設定 \ セキュリティ settings \local policies \user Rights割り当て**:  

    -   ネットワークからのこのコンピューターへのアクセスを拒否する  

    -   バッチ ジョブとしてのログオンを拒否  

    -   サービスとしてのログオンを拒否  

    -   ローカル ログオンを拒否  

    -   リモート デスクトップ サービス ユーザーの権利を使ったログオンを拒否します。  

3.  プロパティまたは Domain Admins グループのメンバーシップに変更を行った場合にアラートを送信するは、監査を構成する必要があります。  

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-domain-admins-group"></a>Domain Admins グループからすべてのメンバーを削除するための手順  

1.  **サーバー マネージャー**、 をクリックして**ツール**、 をクリック**Active Directory ユーザーとコンピューター**します。  

2.  DA グループからすべてのメンバーを削除するには、次の手順を実行します。  

    1.  ダブルクリックして、 **Domain Admins**をグループ化し、をクリックして、**メンバー**タブ。  

        ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_62.gif)  

    2.  グループのメンバーを選択して、**削除**、 をクリックして**はい**、 をクリック**ok**します。  

3.  DA グループのすべてのメンバーが削除されるまで、手順 2. を繰り返します。  

#### <a name="step-by-step-instructions-to-secure-domain-admins-in-active-directory"></a>Active Directory の Domain Admins をセキュリティで保護するための手順  

1.  **サーバー マネージャー**、 をクリックして**ツール**、 をクリック**Group Policy Management**します。  

2.  コンソール ツリーで、展開\<フォレスト\>\\ドメイン\\\<ドメイン\>、し**グループ ポリシー オブジェクト**(場所\<フォレスト\>フォレストの名前を指定し、\<ドメイン\>グループ ポリシーを設定するドメインの名前を指定します)。  

3.  コンソール ツリーで、右クリック**グループ ポリシー オブジェクト**、 をクリック**新規**します。  

    ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_63.gif)  

4.  **新しい GPO**ダイアログ ボックスに「 \<GPO 名\> をクリック**OK** (場所\<GPO 名\>この GPO の名前を指定します).  

    ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_64.gif)  

5.  詳細ペインで右クリックして\<GPO 名\>、 をクリック**編集**します。  

6.  移動します**コンピューター \policies\windows \security settings \local Policies**、 をクリック**ユーザー権利の割り当て**します。  

    ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_65.gif)  

7.  Domain Admins グループのメンバーが次の手順に従って、ネットワーク経由でメンバー サーバーとワークステーションにアクセスすることを防ぐためにユーザー権限を構成します。  

    1.  ダブルクリック**ネットワークからこのコンピューターへのアクセスを拒否**選択と**これらのポリシー設定を定義**。  

    2.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

    3.  型**Domain Admins**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_66.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

8.  DA グループのメンバーが、次の手順を実行してバッチ ジョブとしてログオンするを防ぐためにユーザー権限を構成します。  

    1.  ダブルクリック**バッチ ジョブとしてログオンを拒否**選択と**これらのポリシー設定を定義**。  

    2.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

    3.  型**Domain Admins**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_67.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

9. DA グループのメンバーが次の手順に従って、サービスとしてログオンするを防ぐためにユーザー権限を構成します。  

    1.  ダブルクリック**サービスとしてログオンを拒否**選択と**これらのポリシー設定を定義**します。  

    2.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

    3.  型**Domain Admins**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_68.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

10. ローカルでログオン メンバー サーバーとワークステーションに、次の手順を実行してから、Domain Admins グループのメンバーを防ぐためにユーザー権限を構成します。  

    1.  ダブルクリック**ローカル ログオンを拒否する**選択**これらのポリシー設定を定義**。  

    2.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

    3.  型**Domain Admins**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_69.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

11. Domain Admins グループのメンバーが、次の手順でメンバー サーバーとリモート デスクトップ サービスを使用してワークステーションにアクセスすることを防ぐためにユーザー権限を構成します。  

    1.  ダブルクリック**リモート デスクトップ サービスを使ったログオンを拒否する**選択**これらのポリシー設定を定義**。  

    2.  クリックして**追加のユーザーまたはグループ** をクリック**参照**します。  

    3.  型**Domain Admins**、 をクリックして**名前の確認**、 をクリック**OK**します。  

        ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_70.gif)  

    4.  をクリックして **[ok]** と**OK**もう一度です。  

12. 終了する**グループ ポリシー管理エディター**、 をクリックして**ファイル**、 をクリック**終了**します。  

13. グループ ポリシーの管理には、次の手順に従って、メンバー サーバーとワークステーションの Ou に GPO をリンクします。  

    1.  移動します、\<フォレスト\>\Domains\\\<ドメイン\>(場所\<フォレスト\>フォレストの名前を指定し、\<ドメイン\>の名前を指定しますドメイン グループ ポリシーを設定する)。  

    2.  GPO に適用され、をクリックする OU を右クリックして**既存の GPO をリンク**します。  

        ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_71.gif)  

    3.  先ほど作成した GPO を選択し、クリックして**OK**します。  

        ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_72.gif)  

    4.  ワークステーションが含まれているその他のすべての Ou へのリンクを作成します。  

    5.  メンバー サーバーを含むその他のすべての Ou へのリンクを作成します。  

        > [!IMPORTANT]  
        > ジャンプ サーバーをドメイン コント ローラーと Active Directory の管理に使用する場合は、ジャンプ サーバーが Gpo がリンクされていないこの OU 内にあることを確認します。  

#### <a name="verification-steps"></a>検証手順  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>アクセスを拒否をこのコンピューターにネットワークから"GPO の設定を確認します。  
メンバー サーバーまたはワークステーション (「ジャンプ サーバー」) など、GPO の変更の影響を受けませんからには、メンバー サーバーまたはワークステーションを GPO の変更によって影響を受けるネットワーク経由でアクセスしてみます。 GPO の設定を確認するにマップしようとする、システム ドライブを使用して、 **NET USE**コマンド。  

1.  Domain Admins グループのメンバーであるアカウントをローカルでログオンします。  

2.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

3.  **検索**ボックスに「**コマンド プロンプト**、右クリックして**コマンド プロンプト**順にクリックします**管理者として実行**を管理者特権でを開くコマンド プロンプト。  

4.  昇格を承認するメッセージが表示されたら、クリックして**はい**します。  

    ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_73.gif)  

5.  **コマンド プロンプト**ウィンドウで、「 **net \\ \\\<サーバー名\>\c$** ここで、\<サーバー名\>が、メンバー サーバーまたはネットワーク経由でアクセスしようとしているワークステーションの名前。  

6.  次のスクリーン ショットには、表示されるエラー メッセージが表示されます。  

    ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_74.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>「バッチ ジョブとしてのログオンを拒否」GPO の設定を確認します。  

任意のメンバー サーバーまたは GPO の変更によって影響を受けるワークステーションからローカルでログオンします。  

###### <a name="create-a-batch-file"></a>バッチ ファイルを作成します。  

1.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

2.  **検索**ボックスに「**メモ帳** をクリック**メモ帳**します。  

3.  **メモ帳**、型**dir c:** します。  

4.  クリックして**ファイル**、 をクリック**名前を付けて保存**します。  

5.  **ファイル**名前フィールドに「  **\<Filename\>.bat** (場所\<ファイル名\>新しいバッチ ファイルの名前を指定します)。  

###### <a name="schedule-a-task"></a>タスクをスケジュールします。  

1.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

2.  **検索**ボックスに「**タスク スケジューラ** をクリック**タスク スケジューラ**します。  

    > [!NOTE]  
    > 実行しているコンピューター、Windows 8 で、**検索**ボックスに「**タスクのスケジュール**、 をクリック**タスクのスケジュール**します。  

3.  **タスク スケジューラ**メニュー バーでクリックして**アクション**、 をクリック**タスクの作成**です。  

4.  **タスクの作成**ダイアログ ボックスに「 **\<タスク名\>** (場所\<タスク名\>新しいタスク名前を指定します).  

5.  をクリックして、**アクション**タブをクリックし、をクリックして**新規**します。  

6.  **アクション**フィールドで、**プログラムを起動する**します。  

7.  [**プログラム/スクリプト**、] をクリックして**参照**を検索して選択で作成したバッチ ファイル、**バッチ ファイルを作成**セクションをクリックします**を開く**.  

8.  **[OK]** をクリックします。  

9. **[全般]** タブをクリックします。  

10. [**セキュリティ**オプション] をクリックして**変更ユーザーまたはグループ**します。  

11. Domain Admins グループのメンバーであるアカウントの名前を入力**名前の確認**、 をクリック**OK**します。  

12. 選択 **、ユーザーがログオンしているかどうかにかかわらず実行**選択と**パスワードを保存しない**。 タスクは、ローカル コンピューターのリソースへのアクセスを必要のみがあります。  

13. **[OK]** をクリックします。  

14. タスクを実行する資格情報要求のユーザー アカウント ダイアログ ボックスが表示されます。  

15. 資格情報を入力すると、次のようにクリックします。 **OK**します。  

16. 次のようなダイアログ ボックスが表示されます。  

    ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_75.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>「サービスとしてのログオンを拒否」GPO の設定を確認します。  

1.  任意のメンバー サーバーまたは GPO の変更によって影響を受けるワークステーションからローカルでログオンします。  

2.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

3.  **検索**ボックスに「**サービス**、 をクリック**サービス**します。  

4.  見つけてダブルクリック**印刷スプーラー**します。  

5.  **[ログオン]** タブをクリックします。  

6.  **としてログオン**を選択、**このアカウント**オプション。  

7.  をクリックして**参照**、Domain Admins グループのメンバーであるアカウントの名前を入力、 をクリックして**名前の確認**、 をクリック**OK**。  

8.  **パスワード**と**パスワードの確認入力**、選択したアカウントのパスワードを入力し、をクリックして**OK**します。  

9. クリックして**OK** 3 回です。  

10. 右クリック**印刷スプーラー**クリック**再起動**。  

11. サービスが再起動されると、次のようなダイアログ ボックスが表示されます。  

    ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_76.gif)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>プリンタ スプーラ サービスへの変更を元に戻す  

1.  任意のメンバー サーバーまたは GPO の変更によって影響を受けるワークステーションからローカルでログオンします。  

2.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

3.  **検索**ボックスに「**サービス**、 をクリック**サービス**します。  

4.  見つけてダブルクリック**印刷スプーラー**します。  

5.  **[ログオン]** タブをクリックします。  

6.  **としてログオン**を選択、**ローカル システム**アカウント、およびクリックして**ok**。  

##### <a name="verify-deny-log-on-locally-gpo-settings"></a>「ローカル ログオンを拒否」GPO の設定を確認します。  

1.  すべてのメンバー サーバーまたはワークステーション、GPO の変更によって影響を受けるには、Domain Admins グループのメンバーであるアカウントを使用してローカルでログオンを試みます。 次のようなダイアログ ボックスが表示されます。  

    ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_77.gif)  

##### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>「リモート デスクトップ サービス経由でログオンを拒否」GPO の設定を確認します。    
1.  マウスで画面の右または右上隅にポインターを移動します。 ときに、**チャーム**バーが表示されたら、をクリックして**検索**します。  

2.  **検索**ボックスに「**リモート デスクトップ接続**、 をクリック**リモート デスクトップ接続**します。  

3.  **コンピューター**フィールドに接続し、をクリックしたいコンピューターの名前を「 **Connect**します。 (入力することできますもコンピューター名の代わりに IP アドレスです。)  

4.  入力を求められたら、Domain Admins グループのメンバーであるアカウントの資格情報を提供します。  

5.  次のようなダイアログ ボックスが表示されます。  

    ![セキュリティで保護されたドメインの管理者グループ](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_78.gif)  
