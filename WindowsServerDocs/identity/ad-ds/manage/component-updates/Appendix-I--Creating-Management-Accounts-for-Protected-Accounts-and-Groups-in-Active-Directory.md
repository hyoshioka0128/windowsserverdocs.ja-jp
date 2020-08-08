---
ms.assetid: 13fe87d9-75cf-45bc-a954-ef75d4423839
title: 付録 I-Active Directory で保護されたアカウントとグループの管理アカウントを作成する
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 7f8624b23a746eed5df9ab55c7c01d0dfbd9cb0f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87943861"
---
# <a name="appendix-i-creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>付録 I: Active Directory の保護されたアカウントとグループの管理アカウントを作成する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

高い特権を持つグループの永続的なメンバーシップに依存しない Active Directory モデルを実装する際の課題の1つは、グループの一時的なメンバーシップが必要になったときに、これらのグループを設定するためのメカニズムが必要であることです。 特権 id 管理ソリューションの中には、ソフトウェアのサービスアカウントに、フォレスト内の各ドメインの DA や管理者などのグループに永続的なメンバーシップが付与されていることが必要です。 ただし、Privileged Identity Management (PIM) ソリューションでは、このような高い権限を持つコンテキストでサービスを実行する必要はありません。

この付録では、ネイティブに実装された、またはサードパーティの PIM ソリューションを使用して、権限の制限があり、厳密に制御できるアカウントを作成するために使用できる情報を提供しますが、一時的な昇格が必要な場合に Active Directory に特権グループを設定するために使用できます。 PIM をネイティブソリューションとして実装している場合は、これらのアカウントを使用して一時的なグループの作成を実行できます。また、サードパーティのソフトウェアを使用して PIM を実装している場合は、これらのアカウントをサービスアカウントとして機能するように調整することもできます。

> [!NOTE]
> この付録で説明する手順では、Active Directory で高い特権を持つグループを管理する方法の1つを紹介します。 これらの手順は、ニーズに合わせて調整したり、制限を追加したり、ここで説明する制限を省略したりすることができます。

## <a name="creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>Active Directory の保護されたアカウントとグループの管理アカウントを作成する

管理アカウントに過度の権限とアクセス許可を付与しなくても、特権グループのメンバーシップを管理するために使用できるアカウントを作成するには、次の手順で説明されている4つの一般的なアクティビティが必要です。

1.  まず、アカウントを管理するグループを作成する必要があります。これらのアカウントは、限られた一連の信頼されたユーザーによって管理される必要があるためです。 特権と保護されたアカウントおよびシステムをドメインの一般作成から分離できる OU 構造がまだない場合は、作成する必要があります。 この付録では具体的な手順については説明していませんが、このような OU 階層の例をスクリーンショットに示しています。

2.  管理アカウントを作成します。 これらのアカウントは、"通常の" ユーザーアカウントとして作成され、既定でユーザーに付与されているユーザー権限以外に付与される必要があります。

3.  管理アカウントに制限を実装して、作成された専用の目的だけでなく、アカウントを有効化および使用できるユーザー (最初の手順で作成したグループ) を制御することもできます。

4.  各ドメインの AdminSDHolder オブジェクトに対するアクセス許可を構成して、管理アカウントがドメイン内の特権グループのメンバーシップを変更できるようにします。

運用環境で実装する前に、これらのすべての手順を十分にテストし、必要に応じて環境に合わせて変更する必要があります。 また、すべての設定が想定どおりに動作することを確認する必要があります (この付録ではいくつかのテスト手順が示されています)。また、管理アカウントを使用して保護されたグループに回復するために使用できないディザスターリカバリーシナリオをテストする必要があります。 Active Directory のバックアップと復元の詳細については、 [AD DS のバックアップと回復のステップバイステップガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771290(v=ws.10))を参照してください。

> [!NOTE]
> この付録で説明されている手順を実行して、EAs、DAs、BAs などの最高レベルの特権 Active Directory グループだけでなく、各ドメインのすべての保護されたグループのメンバーシップを管理できるアカウントを作成します。 Active Directory での保護グループの詳細については、「[付録 C: Active Directory の保護されたアカウントとグループ](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)」を参照してください。

### <a name="step-by-step-instructions-for-creating-management-accounts-for-protected-groups"></a>保護されたグループの管理アカウントを作成するための詳細な手順

#### <a name="creating-a-group-to-enable-and-disable-management-accounts"></a>管理アカウントを有効または無効にするグループの作成

管理アカウントのパスワードは、使用するたびにリセットされる必要があり、必要な活動が完了したら無効にする必要があります。 これらのアカウントにはスマートカードログオン要件を実装することも検討できますが、これはオプションの構成であり、これらの手順では、管理アカウントがユーザー名と長い複雑なパスワードで最小制御として構成されることを前提としています。 この手順では、管理アカウントのパスワードをリセットし、アカウントを有効または無効にするアクセス許可を持つグループを作成します。

管理アカウントを有効または無効にするグループを作成するには、次の手順を実行します。

1.  管理アカウントを格納する OU 構造で、グループを作成する OU を右クリックし、[**新規**] をクリックして、[**グループ**] をクリックします。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_115.png)

2.  [**新しいオブジェクト-グループ**] ダイアログボックスで、グループの名前を入力します。 このグループを使用して、フォレスト内のすべての管理アカウントを "アクティブ化" する予定の場合は、ユニバーサルセキュリティグループにしてください。 単一ドメインフォレストの場合、または各ドメインにグループを作成する予定がある場合は、グローバルセキュリティグループを作成できます。 **[OK]** をクリックしてグループを作成します。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_116.png)

3.  作成したグループを右クリックし、[**プロパティ**] をクリックして、[**オブジェクト**] タブをクリックします。グループの [**オブジェクトのプロパティ**] ダイアログボックスで、[誤って削除されないように**保護**する] を選択します。これにより、他の権限のあるユーザーがグループを削除できなくなるだけでなく、属性を最初にオフにしない限り、別の OU に移動することもできません。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_117.png)

    > [!NOTE]
    > 限られた数のユーザーのみに管理を制限するために、グループの親 Ou に対するアクセス許可を既に構成している場合は、次の手順を実行する必要はありません。 ここで提供されているのは、このグループを作成した OU 構造に限定された管理制御を実装していない場合でも、承認されていないユーザーによるグループの変更を防ぐことができるようにするためです。

4.  [**メンバー** ] タブをクリックし、管理アカウントを有効にしたり、必要に応じて保護されたグループを設定したりするチームメンバーのアカウントを追加します。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_118.png)

5.  まだ行っていない場合は、 **Active Directory ユーザーとコンピューター** ] コンソールで、[**表示**] をクリックし、[**高度な機能**] を選択します。 作成したグループを右クリックし、[**プロパティ**] をクリックして、[**セキュリティ**] タブをクリックします。[**セキュリティ**] タブで、[**詳細設定**] をクリックします。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_119.png)

6.  **[グループ] の [セキュリティの詳細設定**] ダイアログボックスで、[**継承を無効にする**] をクリックします。 メッセージが表示されたら、[継承された**アクセス許可をこのオブジェクトの明示的なアクセス許可に変換**] をクリックし、[ **OK** ] をクリックして、グループの [**セキュリティ**] ダイアログボックスに戻ります。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_120.png)

7.  [**セキュリティ**] タブで、このグループへのアクセスを許可しないグループを削除します。 たとえば、認証されたユーザーがグループの名前と全般プロパティを読み取ることができないようにするには、その ACE を削除します。 また、アカウントオペレーターや Windows 2000 サーバー互換アクセスなどの Ace を削除することもできます。 ただし、オブジェクト権限の最小セットをそのままにしておく必要があります。 次の Ace はそのままにしておきます。

    -   SELF

    -   SYSTEM

    -   Domain Admins

    -   Enterprise Admins

    -   管理者

    -   Windows 認証アクセスグループ (該当する場合)

    -   エンタープライズドメインコントローラ

    Active Directory の最上位の特権グループがこのグループを管理できるようになっているように思えるかもしれませんが、これらの設定を実装する目的は、それらのグループのメンバーが承認された変更を行うことができないようにすることではありません。 その目的は、非常に高いレベルの特権が必要な場合に、承認された変更が成功することを保証することです。 このため、このドキュメントでは、既定の特権グループの入れ子、権限、アクセス許可を変更しないことをお勧めします。 既定の構造をそのままにして、ディレクトリ内の最上位の特権グループのメンバーシップを空にすることで、引き続き予想どおりに機能する、より安全な環境を作成できます。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_121.png)

    > [!NOTE]
    > このグループを作成した OU 構造内のオブジェクトに対して監査ポリシーをまだ構成していない場合は、このグループの変更をログに記録するように監査を構成する必要があります。

8.  管理アカウントが必要になったときに "チェックアウト" するために使用されるグループの構成が完了し、その活動が完了したことを示すアカウントが "チェックイン" されます。

#### <a name="creating-the-management-accounts"></a>管理アカウントの作成

Active Directory のインストールで特権グループのメンバーシップを管理するために使用されるアカウントを少なくとも1つ作成する必要があります。また、バックアップとして機能する2番目のアカウントを使用することもできます。 フォレスト内の単一ドメインに管理アカウントを作成し、すべてのドメインの保護されたグループに管理機能を付与するかどうかにかかわらず、また、フォレスト内の各ドメインに管理アカウントを実装することを選択した場合でも、手順は実質的に同じです。

> [!NOTE]
> このドキュメントに記載されている手順では、ロールベースのアクセス制御を実装しておらず、Active Directory 用に privileged identity management を実装していないことを前提としています。 そのため、一部の手順は、対象のドメインの Domain Admins グループのメンバーであるアカウントを持つユーザーが実行する必要があります。
>
> DA 特権を持つアカウントを使用している場合は、ドメインコントローラーにログオンして構成アクティビティを実行できます。 DA 特権を必要としない手順は、管理ワークステーションにログオンしている低い特権のアカウントで実行できます。 薄い青の色で囲まれたダイアログボックスを表示するスクリーンショットは、ドメインコントローラーで実行できるアクティビティを表します。 濃い青の色のダイアログボックスを表示するスクリーンショットは、特権が制限されているアカウントを使用して管理ワークステーションで実行できる活動を表します。

管理アカウントを作成するには、次の手順を実行します。

1. ドメインの DA グループのメンバーであるアカウントを使用して、ドメインコントローラーにログオンします。

2. **Active Directory ユーザーとコンピューター** ] を起動し、管理アカウントを作成する OU に移動します。

3. OU を右クリックし、[**新規**] をクリックして、[**ユーザー**] をクリックします。

4. [**新しいオブジェクト-ユーザー** ] ダイアログボックスで、アカウントの名前を入力し、[**次へ**] をクリックします。

   ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_122.png)

5. ユーザーアカウントの初期パスワードを指定し、[**ユーザーは次回ログオン時にパスワードの変更が必要**]、[**ユーザーはパスワードを変更できない**]、[**アカウントは無効**] の順に選択し、[**次へ**] をクリックします。

   ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_123.png)

6. アカウントの詳細が正しいことを確認し、[**完了**] をクリックします。

7. 作成したユーザーオブジェクトを右クリックし、[**プロパティ**] をクリックします。

8. **[アカウント]** タブをクリックします。

9. [**アカウントのオプション**] フィールドで、[**アカウントは重要なので委任できない**] フラグを選択し、[**このアカウントで kerberos aes 128 ビット暗号化をサポート**する] または [**このアカウントで kerberos aes 256 暗号化をサポート**する] を選択し、[ **OK]** をクリックします。

   ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_124.png)

   > [!NOTE]
   > このアカウントは、他のアカウントと同様に、制限がありますが、強力な機能を持ちます。このアカウントは、セキュリティで保護された管理ホストでのみ使用してください。 環境内のすべてのセキュリティで保護された管理ホストについては、ネットワークセキュリティを実装することを検討する必要があります。セキュリティで保護されたホストに実装できる最も安全な暗号化の種類のみを許可するように、 **Kerberos で許可される暗号化の種類を構成**するグループポリシーします。
   >
   > ホストに対してより安全な暗号化の種類を実装しても、資格情報の盗難攻撃を軽減することはできませんが、セキュリティで保護されたホストの適切な使用と構成が行われます。 特権アカウントによってのみ使用されるホストに対して、より強力な暗号化の種類を設定すると、コンピューターの攻撃対象領域が軽減されます。
   >
   > システムおよびアカウントでの暗号化の種類の構成の詳細については、「 [Kerberos でサポートされる暗号化の種類の Windows 構成](https://blogs.msdn.com/b/openspecification/archive/2011/05/31/windows-configurations-for-kerberos-supported-encryption-type.aspx)」を参照してください。
   >
   > これらの設定は、Windows Server 2012、Windows Server 2008 R2、Windows 8、または Windows 7 を実行しているコンピューターでのみサポートされます。

10. [**オブジェクト**] タブで、[誤って削除されないように**オブジェクトを保護**する] を選択します。 これにより、オブジェクトが (承認されたユーザーによっても) 削除されるのを防ぐだけでなく、属性を変更する権限を持つユーザーが最初にチェックボックスをオフにしない限り、AD DS 階層内の別の OU に移動できなくなります。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_125.png)

11. [**リモートコントロール**] タブをクリックします。

12. [**リモートコントロールを有効にする**] フラグをオフにします。 サポートスタッフがこのアカウントのセッションに接続して修正プログラムを実装する必要はありません。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_126.png)

    > [!NOTE]
    > Active Directory 内のすべてのオブジェクトには、「[セキュリティ侵害の計画](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)」で説明されているように、指定された IT 所有者と指定されたビジネス所有者が必要です。 外部データベースではなく Active Directory 内の AD DS オブジェクトの所有権を追跡する場合は、このオブジェクトのプロパティに適切な所有権情報を入力する必要があります。
    >
    > このケースでは、ビジネスの所有者はほとんどが IT 部門であり、ビジネスの所有者が IT 担当者でもありません禁止。 オブジェクトの所有権を確立するには、オブジェクトに対して変更を行う必要があるときに、たとえば最初の作成から何年もの間、連絡先を識別できるようにします。

13. [**組織**] タブをクリックします。

14. AD DS オブジェクトの標準で必要な情報を入力します。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_127.png)

15. [**ダイヤル**イン] タブをクリックします。

16. [**ネットワークアクセス許可**] フィールドで、[**アクセスの拒否**] を選択します。このアカウントは、リモート接続経由で接続する必要はありません。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_128.png)

    > [!NOTE]
    > お使いの環境で読み取り専用ドメインコントローラー (Rodc) にログオンするときに、このアカウントが使用されることはほとんどありません。 ただし、アカウントが RODC にログオンする必要がある場合は、このアカウントを拒否 RODC パスワードレプリケーショングループに追加して、パスワードが RODC にキャッシュされないようにする必要があります。
    >
    > アカウントのパスワードは、使用するたびにリセットする必要があり、アカウントを無効にする必要がありますが、この設定を実装してもアカウントに対する deleterious の影響はありません。また、管理者がアカウントのパスワードをリセットして無効にすることを忘れた場合に役立つ可能性があります。

17. **[所属するグループ]** タブをクリックします。

18. **[追加]** をクリックします。

19. [**ユーザー、連絡先、コンピューターの選択**] ダイアログボックスで「**拒否済み RODC パスワードレプリケーショングループ**」と入力し、[**名前の確認**] をクリックします。 オブジェクトピッカーでグループの名前に下線が表示されたら、[ **OK]** をクリックして、アカウントが次のスクリーンショットに表示される2つのグループのメンバになっていることを確認します。 保護されているグループにアカウントを追加しないでください。

20. **[OK]** をクリックします。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_129.png)

21. [**セキュリティ**] タブをクリックし、[**詳細設定**] をクリックします。

22. [**セキュリティの詳細設定**] ダイアログボックスで、[**継承の無効化**] をクリックし、継承されたアクセス許可を明示的なアクセス許可としてコピーして、[**追加**] をクリックします

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_130.png)

23. **[アカウント] ダイアログボックスの [アクセス許可エントリ**] で、[**プリンシパルの選択**] をクリックし、前の手順で作成したグループを追加します。 ダイアログボックスの一番下までスクロールし、[**すべてクリア**] をクリックして、すべての既定のアクセス許可を削除します。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_131.png)

24. [**アクセス許可エントリ**] ダイアログボックスの一番上までスクロールします。 [**種類**] ドロップダウンリストが [**許可**] に設定されていることを確認し、[**適用先**] ドロップダウンリストで [**このオブジェクトのみ**] を選択します。

25. [**権限**] フィールドで、 **[すべてのプロパティの読み取り**]、[**読み取りアクセス許可**]、[**パスワードのリセット**] を選択します。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_132.png)

26. [**プロパティ**] フィールドで、[ **useraccountcontrol を読み取り**、useraccountcontrol を**書き込む**] を選択します。

27. [**セキュリティの詳細設定**] ダイアログボックスで、**もう一度 [** **ok**] をクリックします。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_133.png)

    > [!NOTE]
    > **UserAccountControl**属性では、複数のアカウント構成オプションを制御します。 属性に書き込み権限を付与する場合、一部の構成オプションのみを変更する権限を付与することはできません。

28. [**セキュリティ**] タブの [**グループ名またはユーザー名**] フィールドで、アカウントへのアクセスまたは管理を許可しないグループをすべて削除します。 Everyone グループや自己計算されるアカウントなど、拒否 Ace を使用して構成されているグループは削除しないでください (この ACE は、アカウントの作成時に [**ユーザーがパスワードを変更できない**] フラグが有効になっていた場合に設定されていました)。 また、追加したばかりのグループ、システムアカウント、または EA、DA、BA、Windows 認証アクセスグループなどのグループを削除しないようにしてください。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_134.png)

29. [**詳細**設定] をクリックし、[セキュリティの詳細設定] ダイアログボックスが次のスクリーンショットのように表示されることを確認します。

30. [ **Ok**] を**もう一度**クリックして、アカウントの [プロパティ] ダイアログボックスを閉じます。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_135.png)

31. これで、最初の管理アカウントのセットアップが完了しました。 アカウントのテストは、後の手順で行います。

##### <a name="creating-additional-management-accounts"></a>追加の管理アカウントの作成

前の手順を繰り返すか、先ほど作成したアカウントをコピーするか、必要な構成設定を使用してアカウントを作成するスクリプトを作成することにより、追加の管理アカウントを作成できます。 ただし、作成したアカウントをコピーする場合、カスタマイズした設定や Acl の多くは新しいアカウントにコピーされないため、ほとんどの構成手順を繰り返す必要があります。

代わりに、保護されたグループを設定および設定解除する権限を委任するグループを作成できますが、グループとそのグループに配置するアカウントをセキュリティで保護する必要があります。 保護されたグループのメンバーシップを管理する権限が付与されているディレクトリ内のアカウントはほとんどないため、個別のアカウントを作成するのが最も簡単な方法である可能性があります。

管理アカウントを配置するグループをどのように作成するかにかかわらず、前に説明したように、各アカウントがセキュリティで保護されていることを確認する必要があります。 また、 [「付録 D: Active Directory での組み込み管理者アカウントのセキュリティ保護](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)」で説明されているような GPO 制限の実装も検討してください。

##### <a name="auditing-management-accounts"></a>管理アカウントの監査

アカウントの監査を構成して、少なくともアカウントへのすべての書き込みをログに記録する必要があります。 これにより、承認された使用中にアカウントの有効な有効化とパスワードのリセットだけでなく、承認されていないユーザーによるアカウントの操作の試行を識別することができます。 アカウントの書き込みに失敗した場合は、セキュリティ情報とイベント監視 (SIEM) システム (該当する場合) にキャプチャし、潜在的な侵害の調査を担当するスタッフに通知するアラートをトリガーする必要があります。

SIEM ソリューションでは、関連するセキュリティソース (イベントログ、アプリケーションデータ、ネットワークストリーム、マルウェア対策製品、侵入検出ソースなど) からのイベント情報を取得し、データを照合して、インテリジェントなビューやプロアクティブなアクションを作成しようとします。 多くの商用 SIEM ソリューションがあり、多くの企業はプライベートな実装を作成しています。 適切に設計され、適切に実装された SIEM により、セキュリティの監視とインシデント対応の機能が大幅に向上します。 ただし、機能と精度はソリューションによって大きく異なります。 SIEMs はこの記事の範囲を超えていますが、含まれている特定のイベント推奨事項は、SIEM の実装者が検討する必要があります。

ドメインコントローラーの推奨される監査構成設定の詳細については、「[セキュリティ侵害の兆候に対する Active Directory の監視](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)」を参照してください。 ドメインコントローラー固有の構成設定は、[セキュリティ侵害の兆候を監視 Active Directory](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)に提供されています。

#### <a name="enabling-management-accounts-to-modify-the-membership-of-protected-groups"></a>管理アカウントを有効にして保護されたグループのメンバーシップを変更する

この手順では、ドメインの AdminSDHolder オブジェクトに対するアクセス許可を構成して、新しく作成された管理アカウントがドメイン内の保護されたグループのメンバーシップを変更できるようにします。 この手順は、グラフィカルユーザーインターフェイス (GUI) を使用して実行することはできません。

[「付録 C: Active Directory の保護されたアカウントとグループ](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)」で説明したように、ドメインの AdminSDHolder オブジェクトの ACL は、SDProp タスクの実行時に保護されたオブジェクトに実質的に "コピー" されます。 保護されたグループとアカウントは、AdminSDHolder オブジェクトからアクセス許可を継承しません。これらのアクセス許可は、AdminSDHolder オブジェクトのアクセス許可と一致するように明示的に設定されます。 そのため、AdminSDHolder オブジェクトのアクセス許可を変更する場合は、対象とする保護対象オブジェクトの種類に適した属性に変更する必要があります。

この場合、新しく作成された管理アカウントに、グループオブジェクトの members 属性の読み取りと書き込みを許可するように与えます。 ただし、AdminSDHolder オブジェクトはグループオブジェクトではなく、グループ属性はグラフィカル ACL エディターでは公開されません。 この理由から、Dsacls コマンドラインユーティリティを使用してアクセス許可の変更を実装することになります。 保護されたグループのメンバーシップを変更するアクセス許可を (無効) 管理アカウントに付与するには、次の手順を実行します。

1. ドメインコントローラー (可能であれば、PDC エミュレーター (PDCE) の役割を持つドメインコントローラー) にログオンし、ドメイン内の DA グループのメンバーになっているユーザーアカウントの資格情報を使用します。

   ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_136.png)

2. [**コマンドプロンプト**] を右クリックし、[**管理者として実行**] をクリックして、管理者特権でのコマンドプロンプトを開きます。

   ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_137.gif)

3. 昇格の承認を求めるメッセージが表示されたら、[**はい]** をクリックします。

   ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_138.gif)

   > [!NOTE]
   > Windows での昇格とユーザーアカウント制御 (UAC) の詳細については、TechNet web サイトの「 [uac のプロセスと対話](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd835561(v=ws.10))」を参照してください。

4. コマンドプロンプトで、「」と入力します (ドメイン固有の情報に置き換えてください) **Dsacls [ドメイン内の AdminSDHolder オブジェクトの識別名]/g [management ACCOUNT UPN]: RPQ wp; メンバー**。

   ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_139.gif)

   前のコマンド (大文字と小文字は区別されません) は、次のように動作します。

   - Dsacls がディレクトリオブジェクトの Ace を設定または表示する

   - CN = AdminSDHolder、CN = System、DC = TailSpinToys、DC = msft 変更するオブジェクトを識別します。

   - /G は、許可 ACE が構成されていることを示します。

   - PIM001@tailspintoys.msftAce が付与されるセキュリティプリンシパルのユーザープリンシパル名 (UPN) を指定します。

   - "プロパティの読み取り" 権限と "プロパティの書き込み" アクセス許可を "RPQ WP" に付与

   - メンバーは、権限を設定するプロパティ (属性) の名前です。

   **Dsacls**の使用方法の詳細については、コマンドプロンプトで「dsacls」と入力してください。

   ドメインに対して複数の管理アカウントを作成した場合は、アカウントごとに Dsacls コマンドを実行する必要があります。 AdminSDHolder オブジェクトの ACL 構成が完了したら、SDProp を強制的に実行するか、スケジュールされた実行が完了するまで待機する必要があります。 SDProp を強制的に実行する方法の詳細については、「[付録 C: Active Directory の保護されたアカウントとグループ](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)」の「SDProp の手動実行」を参照してください。

   SDProp を実行すると、AdminSDHolder オブジェクトに対して行った変更がドメイン内の保護されたグループに適用されていることを確認できます。 これを確認するには、前述の理由により AdminSDHolder オブジェクトの ACL を表示しますが、保護されたグループの Acl を表示して、アクセス許可が適用されていることを確認できます。

5. [ **Active Directory ユーザーとコンピューター**] で、 **[高度な機能**] が有効になっていることを確認します。 これを行うには、[**表示**] をクリックし、 **domain Admins**グループを見つけて、グループを右クリックし、[**プロパティ**] をクリックします。

6. [**セキュリティ**] タブをクリックし、[**詳細**設定] をクリックして、[**ドメイン管理者のセキュリティの詳細設定**] ダイアログボックスを開きます。

   ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_140.gif)

7. [**管理アカウントの ACE を許可する**] を選択し、[**編集**] をクリックします。 このアカウントに、DA グループに対する **"メンバーの読み取り**" アクセス許可と "**メンバーの書き込み**" アクセス許可が付与されていることを確認し、[ **OK]** をクリックします。

8. [**セキュリティの詳細設定**] ダイアログボックスで [ **ok** ] をクリックし、もう一度 [ **ok** ] をクリックして、[DA] グループの [プロパティ] ダイアログボックスを閉じます。

   ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_141.gif)

9. ドメイン内の他の保護グループに対して、前の手順を繰り返すことができます。アクセス許可は、すべての保護グループで同じである必要があります。 これで、このドメイン内の保護されたグループの管理アカウントの作成と構成が完了しました。

    > [!NOTE]
    > Active Directory 内のグループのメンバーシップを書き込む権限を持つアカウントも、そのグループに追加できます。 この動作は仕様によるものであり、無効にすることはできません。 このため、使用されていないときは常に管理アカウントを無効にし、無効になっている場合や使用されている場合はアカウントを厳密に監視する必要があります。

#### <a name="verifying-group-and-account-configuration-settings"></a>グループとアカウントの構成設定を確認しています

ドメイン内の保護されたグループのメンバーシップを変更できる管理アカウントを作成し、構成しました (これには、最も特権の高い EA、DA、および BA グループが含まれます)。アカウントとその管理グループが正しく作成されていることを確認する必要があります。 検証は、次の一般的なタスクで構成されます。

1.  管理アカウントを有効または無効にして、グループのメンバーがアカウントを有効または無効にし、パスワードをリセットできることを確認するグループをテストします。ただし、管理アカウントで他の管理アクティビティを実行することはできません。

2.  管理アカウントをテストして、ドメイン内の保護されたグループにメンバーを追加したり、削除したりできることを確認します。ただし、保護されたアカウントとグループのその他のプロパティは変更できません。

##### <a name="test-the-group-that-will-enable-and-disable-management-accounts"></a>管理アカウントを有効または無効にするグループをテストする

1.  管理アカウントの有効化とパスワードのリセットをテストするには、 [「付録 I: Active Directory で保護されたアカウントとグループの管理アカウントを作成](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)する」で作成したグループのメンバーであるアカウントを使用して、セキュリティで保護された管理ワークステーションにログオンします。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_142.gif)

2.  **Active Directory ユーザーとコンピューター**] を開き、管理アカウントを右クリックして、[**アカウントの有効化**] をクリックします。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_143.gif)

3.  アカウントが有効になっていることを確認するダイアログボックスが表示されます。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_144.gif)

4.  次に、管理アカウントのパスワードをリセットします。 これを行うには、アカウントをもう一度右クリックし、[**パスワードのリセット**] をクリックします。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_145.gif)

5.  [**新しいパスワード**] フィールドと [**パスワードの確認**入力] フィールドにアカウントの新しいパスワードを入力し、[ **OK]** をクリックします。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_146.gif)

6.  アカウントのパスワードがリセットされたことを確認するダイアログボックスが表示されます。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_147.gif)

7.  次に、管理アカウントの追加のプロパティを変更します。 アカウントを右クリックし、[**プロパティ**] をクリックして、[**リモートコントロール**] タブをクリックします。

8.  [**リモートコントロールを有効にする**] を選択し、[**適用**] をクリックします。 操作は失敗し、**アクセス拒否**エラーメッセージが表示されます。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_148.gif)

9. アカウントの [**アカウント**] タブをクリックし、アカウントの名前、ログオン時間、またはログオンワークステーションを変更します。 すべて失敗し、 **userAccountControl**属性によって制御されないアカウントオプションが淡色表示になり、変更できなくなります。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_149.gif)

10. 保護されたグループ (DA グループなど) に管理グループを追加します。 [ **OK**] をクリックすると、グループを変更するアクセス許可がないことを知らせるメッセージが表示されます。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_150.gif)

11. 必要に応じて追加のテストを実行し、 **userAccountControl**設定とパスワードのリセットを除く管理アカウントで何も構成できないことを確認します。

    > [!NOTE]
    > **UserAccountControl**属性では、複数のアカウント構成オプションを制御します。 属性に書き込み権限を付与する場合、一部の構成オプションのみを変更する権限を付与することはできません。

##### <a name="test-the-management-accounts"></a>管理アカウントをテストする

保護されたグループのメンバーシップを変更できる1つ以上のアカウントを有効にしたので、アカウントをテストして、保護されたグループのメンバーシップを変更できることを確認します。ただし、保護されたアカウントとグループに対して他の変更を行うことはできません。

1.  最初の管理アカウントとして、セキュリティで保護された管理ホストにログオンします。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_151.gif)

2.  **Active Directory ユーザーとコンピューター** ] を起動し、 **domain Admins グループ**を見つけます。

3.  **Domain Admins**グループを右クリックし、[**プロパティ**] をクリックします。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_152.gif)

4.  **Domain Admins のプロパティ**で、[**メンバー** ] タブをクリックし、[追加] を**クリック**します。 一時的なドメイン管理者の特権が付与されるアカウントの名前を入力し、[**名前の確認**] をクリックします。 アカウントの名前に下線が引かれたら、[ **OK** ] をクリックして [**メンバー** ] タブに戻ります。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_153.gif)

5.  [ **Domain Admins のプロパティ**] ダイアログボックスの [**メンバー** ] タブで、[**適用**] をクリックします。 [**適用**] をクリックすると、アカウントが DA グループのメンバーになり、エラーメッセージが表示されなくなります。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_154.gif)

6.  [ **Domain Admins のプロパティ**] ダイアログボックスの [**管理者**] タブをクリックし、フィールドにテキストを入力できず、すべてのボタンがグレー表示されていることを確認します。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_155.gif)

7.  [ **Domain Admins のプロパティ**] ダイアログボックスの [**全般**] タブをクリックし、そのタブに関する情報を変更できないことを確認します。

    ![管理アカウントの作成](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_156.gif)

8.  必要に応じて、追加の保護グループに対してこれらの手順を繰り返します。 完了したら、管理アカウントを有効または無効にするために作成したグループのメンバーであるアカウントを使用して、セキュリティで保護された管理ホストにログオンします。 次に、テストした管理アカウントのパスワードをリセットし、アカウントを無効にします。 管理アカウントと、アカウントを有効または無効にするグループのセットアップが完了しました。
