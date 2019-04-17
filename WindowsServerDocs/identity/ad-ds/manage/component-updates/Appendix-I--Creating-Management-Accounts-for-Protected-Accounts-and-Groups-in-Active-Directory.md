---
ms.assetid: 13fe87d9-75cf-45bc-a954-ef75d4423839
title: "付録 I - Active Directory の保護されたアカウントとグループの管理アカウントを作成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 666180adca691d6c9783a43063df76877115fc40
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="appendix-i-creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>付録 i: Active Directory 内の保護されたアカウントとグループ アカウントの管理を作成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

  
## <a name="appendix-i-creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>付録 i: Active Directory 内の保護されたアカウントとグループ アカウントの管理を作成します。  

永続的な高い権限を持つグループのメンバーシップに依存しないの Active Directory のモデルを実装する際の課題の 1 つは、グループに一時的なメンバーシップが必要な場合は、これらのグループを設定するためのメカニズムが存在する必要があります。 一部の特権の id 管理ソリューションでは、ソフトウェアのサービス アカウントに永続的な DA や管理者は、フォレスト内の各ドメインでなどのグループ メンバーシップが付与されている必要があります。 ただし、技術的には必要はありません Privileged Identity Management (PIM) の解決策をこのような高い権限を持つコンテキストで、サービスを実行します。  
  
この付録では、特権が制限されていると、厳重制御することができますが一時的な昇格が必要な場合は、Active Directory の権限を持つグループを設定するために使用するアカウントを作成するネイティブ実装されたまたはサード パーティの PIM ソリューションを使用できる情報を提供します。 ネイティブのソリューションとして PIM を実装する場合は、これらのアカウントで使用できる管理スタッフ一時グループの作成を実行してサード パーティ製ソフトウェアを介した PIM を実装する場合のサービス アカウントとして機能するこれらのアカウントの調整が行わできる可能性があります。  
  
> [!NOTE]  
> この付録で説明する手順は、Active Directory で高い権限を持つグループの管理に 1 つの方法を提供します。 適応次の手順に、必要に応じて、追加の制限を追加したり、ここで説明されている制限の一部を省略できます。  
  
### <a name="creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>Active Directory 内の保護されたアカウントとグループ アカウントの管理を作成します。  
過剰な権利を付与する管理アカウントを必要とせずに権限を持つグループのメンバーシップを管理するアカウントを作成するを使用して、アクセス許可は、次の手順で説明されている 4 つの全般的なアクティビティで構成されています。  
  
1.  最初に、信頼されたユーザーの制限されたセットによってこれらのアカウントを管理する必要があるため、アカウントを管理するグループを作成する必要があります。 分離の特権と保護されたアカウントとドメインの全般的な人口からシステムに対応した OU 構造があるない場合は、作成する必要があります。 この付録では、具体的な手順は提供されていない、スクリーン ショット表示 OU 階層の例です。  
  
2.  管理アカウントを作成します。 これらのアカウントを「通常」のユーザー アカウントとして作成し、以外に、既定では、ユーザーに与えられた既にユーザー権利が付与されていない必要があります。  
  
3.  管理アカウントが作成された、有効にし、アカウント (最初の手順で作成したグループ) を使用してユーザーを制御するだけでなく、特別な目的にのみ使用できるようにするには、制限を実装します。  
  
4.  ドメイン内の特権グループのメンバーシップを変更する管理アカウントを許可するように各ドメイン内の AdminSDHolder オブジェクトのアクセス許可を構成します。  
  
十分にこれらの手順のすべてをテストして、実稼働環境に実装する前に、環境に必要に応じて変更する必要があります。 すべての設定が期待どおりに動作を確認する必要がありますも (いくつかのテストの手順は、この付録で提供されますが、) とを管理アカウントは保護グループを回復するための設定に使用する利用できない障害回復シナリオをテストする必要があります。 For more information about backing up and restoring Active Directory, see the [AD DS Backup and Recovery Step-by-Step Guide](https://technet.microsoft.com/library/cc771290(v=ws.10).aspx).  
  
> [!NOTE]  
> この付録で説明する手順を実装すると、各ドメイン内のすべての保護グループ、だけでなく、高い特権 Active Directory グループ EAs、DAs BAs などのメンバーシップを管理できるアカウントを作成します。 Active Directory の保護グループの詳細については、次を参照してください。[付録 c: 保護されたアカウントと Active Directory のグループ](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)します。  
  
#### <a name="step-by-step-instructions-for-creating-management-accounts-for-protected-groups"></a>保護グループの管理アカウントを作成する方法を手順に沿って  
  
##### <a name="creating-a-group-to-enable-and-disable-management-accounts"></a>有効にして、管理アカウントを無効にするグループを作成します。  
管理アカウントは、パスワードを使用するたびにリセットする必要があり、それらを必要とするアクティビティが完了すると無効にする必要があります。 これらのアカウントのスマート カード ログオン要件を実装することも検討は、オプションの構成は、次に挙げる手順では、最小限のコントロールとして、ユーザー名と、長くて複雑なパスワードで管理アカウントを構成するを前提としています。 この手順では、アクセス許可を持つ管理アカウントのパスワードをリセットして有効にして、アカウントを無効にするグループを作成します。  
  
有効にして、管理アカウントを無効にするグループを作成するには、次の手順を実行します。  
  
1.  管理アカウントを収容する OU 構造で、グループを作成する OU を右クリックして] をクリックして**新規**] をクリック**グループ**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_115.png)  
  
2.  **新しいオブジェクト - グループ**] ダイアログ ボックスで、グループの名前を入力します。 このグループを使用して、フォレスト内のすべての管理アカウントを「アクティブ」にする場合は、ようにユニバーサル セキュリティ グループを指定します。 単一ドメイン フォレストがある場合、または各ドメインでグループを作成する予定の場合は、グローバル セキュリティ グループを作成することができます。 をクリックして**OK**グループを作成します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_116.png)  
  
3.  Right-click the group you just created, click **Properties**, and click the **Object** tab. In the group's **Object property** dialog box, select **Protect object from accidental deletion**, which will not only prevent otherwise-authorized users from deleting the group, but also from moving it to another OU unless the attribute is first deselected.  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_117.png)  
  
    > [!NOTE]  

    > グループの親の管理ユーザーの制限されたセットを制限する Ou に、アクセス許可が既に構成されている場合、次の手順を実行する必要はありません。 次のとおりできるように、このグループを作成した OU 構造の限られた管理制御を実装していない場合でも、グループの変更に対してセキュリティで保護できます承認されていないユーザーです。  
  
4.  をクリックして、**メンバー**タブをクリックし、保護される必要な場合に、グループの管理アカウントを有効にするか、設定を担当するチームのメンバーのアカウントを追加します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_118.png)  
  
5.  既に完了していない場合、そのために、 **Active Directory ユーザーとコンピューター**コンソールで、をクリックして**ビュー**選択**高度な機能**します。 Right-click the group you just created, click **Properties**, and click the **Security** tab. On the **Security** tab, click **Advanced**.  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_119.png)  
  
6.  **[グループ] のセキュリティの詳細設定**ダイアログ ボックスで、をクリックして**継承の無効にする**します。 メッセージが表示されたら、] をクリックして**変換は、このオブジェクトに対するアクセス許可を明示的にアクセス許可を継承**、] をクリック**OK** 、グループに戻るに**セキュリティ**] ダイアログ ボックス。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_120.png)  
  
7.  **セキュリティ**] タブで、このグループのアクセスを許可しないでグループを削除します。 たとえば、Authenticated Users グループの名前と全般的なプロパティを読み取ることができるしたくない場合は、その ACE を削除できます。 アカウント オペレーターおよび pre-Windows 2000 Server 互換性のあるアクセスのような Ace を削除することもできます。 必要があります、ただし、このまま最小セットのオブジェクトのアクセス許可。 次の Ace をそのままにします。  
  
    -   自己  
  
    -   システム  
  
    -   Domain Admins  
  
    -   Enterprise Admins  
  
    -   管理者  
  
    -   Windows Authorization Access Group (該当する場合)  
  
    -   エンタープライズ ドメイン コント ローラー  
  
    反するかもしれませんがこのグループを管理する Active Directory で最も高い権限を持つグループを許可するように、これらの設定を実装する際の目標はそのグループのメンバーが承認された変更を加えることを防ぐにしません。 代わりに、目標は、非常に高いレベルの特権を必要とする場合がある場合は、承認された変更が成功することを確認します。 このためのグループの入れ子、権限、特権を持つ既定を変更して、このドキュメント全体を通じてアクセス許可がお勧めできないこと勧めします。 既定の構造を維持したまま、ディレクトリ内の最上位の特権グループのメンバーシップを空にする、期待どおりに機能するより安全な環境を作成できます。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_121.png)  
  
    > [!NOTE]  
    > このグループを作成した OU 構造のオブジェクトの監査ポリシーをまだ構成していない場合は必要があります監査を構成する変更をログにこのグループです。  
  
8.  「チェック アウト」に使用されるグループの構成を完了して「チェックイン」アカウントのアクティビティが完了すると、必要なときにアカウントを管理します。  
  
##### <a name="creating-the-management-accounts"></a>管理アカウントを作成します。  
インストールでは、Active Directory、権限を持つグループのメンバーシップを管理するために使用するには、少なくとも 1 つのアカウント、可能であれば、バックアップとして機能するように 2 つ目のアカウントを作成する必要があります。 グループ、保護されている 1 つのドメイン、フォレスト内の管理アカウントを作成し、すべてのドメインの管理機能を付与を選択するかどうか、またはフォレスト内の各ドメインにアカウントの管理を実装することを選択するかどうかの手順は、実質的に同じです。  
  
> [!NOTE]  
> このドキュメントの手順は、まだを実装していない役割に基づいたアクセス制御と Active Directory の privileged identity management 前提としています。 そのため、問題のドメインの Domain Admins グループのメンバーであるアカウントを持つユーザーがいくつかの手順を実行する必要があります。  
>   
> DA 特権を持つアカウントを使用するときに構成のアクティビティを実行するドメイン コント ローラーにログオンできます。 DA 特権を必要としない手順は、管理ワークステーションにログオンしている権限の少ないアカウントで実行することができます。 明るい青色で囲まれたダイアログ ボックスを示すスクリーン ショットは、ドメイン コント ローラーで実行できるアクティビティを表します。 青の暗い色のダイアログ ボックスを示すスクリーン ショットは、特権が制限されているアカウントを持つ管理ワークステーションに実行できるアクティビティを表します。  
  
管理アカウントを作成するには、次の手順を実行します。  
  
1.  ドメインの DA グループのメンバーであるアカウントでドメイン コント ローラーにログオンします。  
  
2.  起動**Active Directory ユーザーとコンピューター**管理アカウントを作成する OU に移動します。  
  
3.  OU を右クリックし、をクリックして**新規**] をクリック**ユーザー**します。  
  
4.  **新しいオブジェクト - ユーザー** ] ダイアログ ボックスで、アカウントの場合は、必要な名前付け情報を入力し、をクリックして**次**します。  
  
5.  ドメインの DA グループのメンバーであるアカウントでドメイン コント ローラーにログオンします。  
  
6.  起動**Active Directory ユーザーとコンピューター**管理アカウントを作成する OU に移動します。  
  
7.  OU を右クリックし、をクリックして**新規**] をクリック**ユーザー**します。  
  
8.  **新しいオブジェクト - ユーザー** ] ダイアログ ボックスで、アカウントの場合は、必要な名前付け情報を入力し、をクリックして**次**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_122.png)  
  
9. オフ、ユーザー アカウントの初期のパスワードを提供する**ユーザーは次回ログオン時にパスワードを変更する必要があります**を選択**ユーザーがパスワードを変更できない**と**アカウントが無効になっている**、] をクリック**[次へ]**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_123.png)  
  
10. アカウントの詳細が正しいことを確認] をクリックして**完了**します。  
  
11. 作成したユーザー オブジェクトを右クリックし、をクリックして**プロパティ**します。  
  
12. をクリックして、**アカウント**] タブ。  
  
13. **アカウント オプション**フィールドで、選択、**アカウントは重要なので委任できない**フラグで、**このアカウントは、Kerberos AES 128 ビット暗号化をサポートしている**や、**このアカウントは、Kerberos AES 256 の暗号化をサポートする**、フラグを設定し] をクリックして**[ok]**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_124.png)  
  
    > [!NOTE]  
    > その他のアカウントと同様に、このアカウントが、限られたが、強力な機能であるため、アカウントはセキュリティで保護された管理ホストでのみ使用してください。 すべてのセキュリティで保護された管理ホスト環境内で、グループ ポリシー設定の実装を検討する必要があります**ネットワーク セキュリティ: Kerberos で許可する暗号化の構成の種類**最も安全な暗号化の種類のみを許可するようにセキュリティで保護されたホストを実装することができます。  
    >   
    > 安全な暗号化の種類をそのホストの実装も資格情報盗難攻撃が緩和されませんが、適切な使用方法と、セキュリティで保護されたホストの構成は、します。 特権アカウントでのみ使用されるホストのより強力な暗号化の種類を設定すると、コンピューターの全体的な攻撃単に低下します。  
    >   
    > システムおよびアカウントの暗号化の種類の構成に関する詳細については、次を参照してください。 [Kerberos サポートされている暗号化の種類についての Windows の構成](http://blogs.msdn.com/b/openspecification/archive/2011/05/31/windows-configurations-for-kerberos-supported-encryption-type.aspx)します。  
    >   
    > **注:**これらの設定は、Windows Server 2012、Windows Server 2008 R2、Windows 8、または Windows 7 を実行しているコンピューターでのみサポートされます。  
  
14. **オブジェクト**] タブで [**オブジェクトを誤って削除されないように保護する**します。 これはのみができないオブジェクト (でも承認されたユーザーの場合) によって削除されないというできなくなりますが、AD DS 階層内の別の OU に移動してから属性を変更するためのアクセス許可を持つユーザーが、チェック ボックスをオフ最初にしない限り、します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_125.png)  
  
15. をクリックして、**リモート_コントロール**] タブ。  
  
16. クリア、**リモート_コントロールを有効にする**フラグ。 これには、サポート スタッフの修正プログラムを実装するこのアカウントのセッションに接続するために必要なことはありませんする必要があります。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_126.png)  
  
    > [!NOTE]  
    > 」の説明に従って、Active Directory 内の各オブジェクトを指定された IT 所有者と、指定されたビジネス所有者必要があります[セキュリティ侵害を計画する](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)します。 (外部データベース) ではなく Active Directory 内の AD DS オブジェクトの所有権を追跡している場合は、このオブジェクトのプロパティで適切な所有権情報を入力する必要があります。  
    >   
    > この場合は、ビジネス オーナーは、IT 部門ではほとんどの場合、返しにも IT 所有者されているビジネス オーナーで禁止していることはありません。 オブジェクトの所有権を確立する点は、変更するオブジェクトに加え、おそらく年最初の作成からが必要なときに、連絡先を識別するためです。  
  
17. クリックして、**組織**] タブ。  
  
18. AD DS オブジェクトの標準のために必要な情報を入力します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_127.png)  
  
19. クリックして、**ダイヤルイン**] タブ。  
  
20. **ネットワーク アクセス許可**フィールドで、[**アクセス権の拒否**します。リモート接続経由で接続はこのアカウントが必要はありません。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_128.png)  
  
    > [!NOTE]  
    > 可能性の高い環境内で読み取り専用ドメイン コント ローラー (Rodc) にログオンするためにこのアカウントが使用されることはありません。 ただし、状況これまで必要ログオンするアカウントに RODC にログオンする必要がありますこのアカウントを追加する Denied RODC Password Replication Group そのパスワードが RODC にキャッシュされていないようにします。  
    >   
    > 使用後、アカウントのパスワードをリセットする必要がありますされ、アカウントを無効にする必要がありますが、この設定を実装しても、アカウントに deleterious 影響はありませんし、アカウントのパスワードをリセットし、それを無効にする管理者を忘れた場合の状況でことをお勧めします。  
  
21. をクリックして、**所属するグループ**] タブ。  
  
22. をクリックして**追加**します。  
  
23. 種類**Denied RODC Password Replication の Group**で、 **[ユーザー、連絡先、コンピューター** ] ダイアログ ボックスとクリック**名前の確認**します。 グループの名前は、オブジェクト ピッカーで下線が引かれますをクリックして**OK**アカウントは、次のスクリーン ショットに表示される 2 つのグループのメンバーでができるようになりましたことを確認します。 保護グループにアカウントを追加できません。  
  
24. をクリックして**OK**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_129.png)  
  
25. をクリックして、**セキュリティ**タブし、をクリックして**詳細**します。  
  
26. **高度なセキュリティ設定**ダイアログ ボックスで、] をクリックして**継承を無効にする**として明示的なアクセス許可は、継承されたアクセス許可をコピーし] をクリックし、**追加**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_130.png)  
  
27. **[アカウント] のアクセス許可エントリ**ダイアログ ボックスで、をクリックして**プリンシパルの選択**し、前の手順で作成したグループに追加します。 ダイアログ ボックスの下部までスクロールし、をクリックして**すべてクリア**をすべての既定のアクセス許可を削除します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_131.png)  
  
28. スクロールの先頭に、**アクセス許可エントリ**] ダイアログ ボックス。 いることを確認、**種類**にドロップダウン リストが設定されている**許可**、し、[、**に適用されます**ドロップダウン リストで、**このオブジェクトのみ**します。  
  
29. **アクセス許可**フィールドで、[**すべてのプロパティの読み取り**、**読み取りアクセス許可を**、および**パスワード リセット**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_132.png)  
  
30. **プロパティ**フィールドで、[ **userAccountControl を読み取る**と**書き込み userAccountControl**します。  
  
31. をクリックして**OK**、 **[ok]**でもう一度、**高度なセキュリティ設定**] ダイアログ ボックス。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_133.png)  
  
    > [!NOTE]  
    > **UserAccountControl**属性は複数のアカウントの構成オプションを制御します。 属性に書き込みアクセス許可を付与した場合は、構成オプションの一部のみを変更するアクセス許可を付与することはできません。  
  
32. **グループ名またはユーザー名**フィールド、**セキュリティ**] タブで、アクセスしたり、アカウントの管理を許可しないで任意のグループを削除します。 Everyone グループと SELF 計算アカウントなど、拒否 Ace が構成されている任意のグループを削除しないでください (その ACE が設定されたときに、**ユーザーがパスワードを変更できない**アカウントの作成中にフラグが有効にします。 また、グループを追加した、SYSTEM アカウント、または EA、DA、BA、または Windows Authorization Access Group などのグループは削除しないでください。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_134.png)  
  
33. をクリックして**詳細**し、セキュリティの詳細設定] ダイアログ ボックスが次のスクリーン ショットのような表示されることを確認します。  
  
34. をクリックして**OK**、および**[ok]** 、アカウントのプロパティ] ダイアログ ボックスを閉じます。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_135.png)  
  
35. 最初の管理アカウントのセットアップが完了しました。 後の手順では、アカウントをテストします。  
  
###### <a name="creating-additional-management-accounts"></a>追加の管理アカウントを作成します。  
前の手順を繰り返すことで、作成したアカウントをコピーしたりして、必要な構成設定とアカウントを作成するスクリプトを作成するには、追加の管理アカウントを作成することができます。 ただし、作成したアカウントをコピーする場合、カスタマイズした設定および Acl の多くは新しいアカウントにコピーされませんし、ほとんどの構成手順を繰り返すことができます。  
  
代わりに設定し、保護グループを unpopulate 権限を委任するグループを作成することができますが、グループとそれに配置するアカウントをセキュリティで保護する必要があります。 保護グループのメンバーシップを管理する機能を付与されているディレクトリにごく少数のアカウントが存在する必要があります、ため個々 のアカウントを作成すると最も簡単な方法可能性があります。  
  
管理アカウントの配置先グループを作成するを選択する方法に関係なく、前述のように、各アカウントが保護されていることを確認する必要があります。 GPO の制限に記載されているのと同様の実装を検討する必要がありますも[付録 d: セキュリティで保護する組み込み管理者アカウントでは、Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)します。  
  
###### <a name="auditing-management-accounts"></a>管理アカウントの監査  
ログオンする、少なくとも、アカウントにすべての書き込みアカウント上での監査を構成する必要があります。 成功したアカウントの有効化とも承認されていないユーザーによってしようとすると、アカウントの操作を識別するが、承認済みの使用中に、パスワードのリセットを識別するだけでなく、これにより、します。 アカウントに失敗した書き込みでは、システムでは、セキュリティ情報およびイベント監視 (SIEM) (該当する場合)、キャプチャするかされ、潜在的なセキュリティ侵害を調査するためのスタッフに通知を提供するアラートをトリガーする必要があります。  
  
SIEM ソリューション (たとえば、イベント ログ、アプリケーション データ、ネットワークのストリーム、マルウェア対策製品、および侵入検出ソース) の関連するセキュリティ ソースからのイベント情報の取得、照合データをやり直してくださいインテリジェントなビューや積極的に処理します。 多くの商用 SIEM ソリューションはし、多くの企業は、プライベートの実装を作成します。 適切に設計し、適切に実装されている SIEM は、セキュリティの監視とインシデント対応の機能に大幅に向上させることができます。 ただし、機能と精度ごとに異なる大幅ソリューションです。 Siem が、このホワイト ペーパーの範囲を超えていますが、任意の SIEM 作成者によって含まれている特定のイベントに関する推奨事項を考慮してください。  
  
ドメイン コント ローラーの推奨される監査の構成設定の詳細については、次を参照してください。[監視の Active Directory のセキュリティ侵害の兆候](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)します。 ドメイン コント ローラーに固有の構成設定で提供[監視の Active Directory のセキュリティ侵害の兆候](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)します。  
  
##### <a name="enabling-management-accounts-to-modify-the-membership-of-protected-groups"></a>保護グループのメンバーシップを変更する管理アカウントを有効にします。  
この手順では、新しく作成された管理アカウント ドメイン内の保護グループのメンバーシップの変更を許可するように、ドメインの AdminSDHolder オブジェクトに対するアクセス許可を構成します。 グラフィカル ユーザー インターフェイス (GUI) 経由では、この手順を実行することはできません。  
  
説明したよう[付録 c: 保護されたアカウントと Active Directory のグループ](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)、SDProp タスクの実行時にドメインの AdminSDHolder オブジェクトが効果的に「コピー」への ACL がオブジェクトを保護します。 保護グループとアカウントから継承されないそのアクセス許可の AdminSDHolder オブジェクトそのアクセス許可は AdminSDHolder オブジェクトのものと一致する明示的に設定します。 そのため、AdminSDHolder オブジェクトに対するアクセス許可を変更するときに対象としている保護されたオブジェクトの種類に適した属性を変更する必要があります。  
  
ここを許可するグループ オブジェクトの属性のメンバーの書き込みと読み取りを許可するように新しく作成された管理アカウント。 ただし、AdminSDHolder オブジェクトは、グループ オブジェクトではありません、グループの属性が、グラフィック ACL エディターで公開されていません。 このため、Dsacls コマンド ライン ユーティリティを使用してアクセス許可の変更を実装することができます。 (無効) の管理を保護グループのメンバーシップを変更するアカウントのアクセスを許可するには、次の手順を実行します。  
  
1.  可能であれば、ドメイン コント ローラーを行った DA グループのメンバーで、ドメイン ユーザー アカウントの資格情報を使って、PDC エミュレーター (PDCE) 役割を持つドメイン コント ローラーにログオンします。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_136.png)  
  
2.  右クリックして、管理者特権のコマンド プロンプトを開く**コマンド プロンプト**] をクリック**管理者として実行**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_137.gif)  
  
3.  権限の昇格を承認するのにメッセージが表示されたら、] をクリックして**はい**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_138.gif)  
  
    > [!NOTE]  
    > For more information about elevation and user account control (UAC) in Windows, see [UAC Processes and Interactions](https://technet.microsoft.com/library/dd835561(v=WS.10).aspx) on the TechNet website.  
  
4.  コマンド プロンプトで、種類 (、ドメイン固有の情報に置き換えて) **Dsacls [自分のドメイン内の AdminSDHolder オブジェクトの識別名]/G [UPN をアカウントの管理]: RPWP; メンバー**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_139.gif)  
  
    (これは大文字小文字を区別しない) 前のコマンドは次のとおり動作します。  
  
    -   Dsacls を設定またはディレクトリ オブジェクトの Ace を表示  
  
    -   CN AdminSDHolder、CN = System, DC = = 含ま, DC = msft 変更されるオブジェクトの識別  
  
    -   /G を与える ACE が構成されていることを示します  
  
    -   PIM001@tailspintoys.msftAce の付与するセキュリティ プリンシパルのユーザー プリンシパル名 (UPN) は、します。  
  
    -   RPWP 付与プロパティの読み取りし、書き込みのアクセス許可  
  
    -   メンバーは、プロパティ (属性) の名前が、アクセス許可を設定します。  
  
    使用の詳細については**Dsacls**、Dsacls コマンド プロンプトでパラメーターを指定せずに入力します。  
  
    ドメインの複数の管理アカウントを作成した場合は、アカウントごとに Dsacls コマンドを実行する必要があります。 AdminSDHolder オブジェクトの ACL の構成を完了するを実行、またはそのスケジュールされた実行が完了するまで待ってから SDProp を強制する必要があります。 実行する SDProp の強制の詳細についてを参照してください「を実行している SDProp 手動で」[付録 c: 保護されたアカウントと Active Directory のグループ](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)します。  
  
    SDProp が実行されると、AdminSDHolder オブジェクトに加えられた変更が、ドメインの保護グループに適用されているを確認することができます。 これは以前のように、上の理由から AdminSDHolder オブジェクトの ACL を表示して確認することはできませんが、保護グループの Acl を表示して、アクセス許可が適用されていることを確認できます。  
  
5.  **Active Directory ユーザーとコンピューター**、有効にすることを確認する**高度な機能**します。 これを行うには、次のようにクリックします。**ビュー**、検索、 **Domain Admins**をグループ化し、グループを右クリックし、クリック**プロパティ**します。  
  
6.  をクリックして、**セキュリティ**タブし、をクリックして**詳細**を開くには、 **Domain Admins のセキュリティの詳細設定**] ダイアログ ボックス。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_140.gif)  
  
7.  選択**管理アカウントに許可する ACE** ] をクリック**編集**します。 アカウントがのみ付与されていることを確認**メンバーの読み取り**と**メンバーの書き込み**DA グループ、およびクリックでアクセス許可**OK**します。  
  
8.  をクリックして**[ok]**で、**高度なセキュリティ設定**] ダイアログ ボックスで、クリック**[ok]** DA グループのプロパティ] ダイアログ ボックスを閉じます。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_141.gif)  
  
9. ドメイン内の他の保護グループの前の手順を繰り返すことができます。アクセス許可は、すべての保護グループと同じである必要があります。 このドメイン内の保護グループの管理アカウントの作成と構成を完了したようになりました。  
  
    > [!NOTE]  
    > Active Directory でグループのメンバーシップを作成するアクセス許可を持つ任意のアカウントによっては、グループに追加自体ことができます。 この動作は仕様であり、無効にすることはできません。 このため、管理アカウントを使用しない場合は無効にする必要があります常に保持して、使用に属している場合と、無効になっている場合に、アカウントを厳密に監視する必要があります。  
  
##### <a name="verifying-group-and-account-configuration-settings"></a>グループとアカウントの構成設定を確認します。  
作成し、構成済みの管理アカウント (を EA、DA、および BA の最も高い権限を持つグループを含む)、ドメイン内の保護グループのメンバーシップを変更できるようになったアカウントとその管理グループが正常に作成されたことを確認する必要があります。 検証は、これらの一般的なタスクで構成されます。  
  
1.  有効にし、グループのメンバーを有効にするアカウントを無効にして、パスワードのリセットが管理アカウントの他の管理アクティビティを実行することはできませんを確認する管理アカウントを無効にするグループをテストします。  
  
2.  テスト、管理アカウントことを確認を追加することをメンバーの削除は、ドメイン内のグループを保護できるだけでなく、その他の保護されたアカウントとグループのプロパティを変更することはできません。  
  
###### <a name="test-the-group-that-will-enable-and-disable-management-accounts"></a>テスト グループを有効にし、管理アカウントを無効にします。  
  
1.  管理アカウントを有効にして、そのパスワードをリセットするをテストするには、セキュリティで保護された管理ワークステーションには、グループのメンバーであるアカウントを使用してで作成したログオン[付録 i: 管理アカウントを作成する Active Directory 内の保護されるアカウントとグループ](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_142.gif)  
  
2.  開いている**Active Directory ユーザーとコンピューター**管理アカウントを右クリックし、クリックして、**アカウントの有効化**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_143.gif)  
  
3.  アカウントが有効になっていることを確認] ダイアログ ボックスが表示されます。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_144.gif)  
  
4.  次に、管理アカウントのパスワードをリセットします。 これを行うには、アカウントをもう一度右クリックし] をクリックして**パスワードのリセット**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_145.gif)  
  
5.  アカウントの新しいパスワードを入力、**新しいパスワード**と**パスワードの確認入力**フィールド、およびクリック**[ok]**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_146.gif)  
  
6.  アカウントのパスワードがリセットされていることを確認するためのダイアログ ボックスが表示されます。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_147.gif)  
  
7.  管理アカウントの追加のプロパティを変更する試行できるようになりました。 アカウントを右クリックし、をクリックして**プロパティ**、] をクリックし、**リモート_コントロール**] タブ。  
  
8.  選択**リモート_コントロールを有効にする**] をクリック**適用**します。 操作が失敗する必要があります、**アクセスが拒否されました**エラー メッセージを表示する必要があります。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_148.gif)  
  
9. をクリックして、**アカウント**アカウント タブに移動して、アカウントの名、ログオン時間、またはワークステーションのログオンを変更しようとします。 すべてが失敗し、アカウントによって制御されていないオプション、 **userAccountControl**灰色変更するために使用できなくなり、属性を表示する必要があります。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_149.gif)  
  
10. DA グループなどの保護グループに管理グループを追加しようとしてください。 クリックすると**OK**、グループを変更するアクセス許可がないことを通知する、メッセージが表示する必要があります。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_150.gif)  
  
11. ように構成することできません何も管理アカウント以外のことを確認するために必要な追加のテストを実行**userAccountControl**設定とパスワードをリセットします。  
  
    > [!NOTE]  
    > **UserAccountControl**属性は複数のアカウントの構成オプションを制御します。 属性に書き込みアクセス許可を付与した場合は、構成オプションの一部のみを変更するアクセス許可を付与することはできません。  
  
###### <a name="test-the-management-accounts"></a>管理アカウントをテストします。  
保護グループのメンバーシップを変更できる 1 つまたは複数のアカウントを有効にしたようになったため、保護グループのメンバーシップを変更することができますが、保護されたアカウントとグループの他の変更を実行することはできませんが、アカウントをテストできます。  
  
1.  最初の管理アカウントとセキュリティで保護された管理ホストにログオンします。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_151.gif)  
  
2.  起動**Active Directory ユーザーとコンピューター**を検索し、 **Domain Admins グループ**します。  
  
3.  右クリックし、 **Domain Admins**グループ化し、をクリックして**プロパティ**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_152.gif)  
  
4.  **Domain Admins のプロパティ**、] をクリックして、**メンバー** ] タブと**クリックして**追加します。 一時的な Domain Admins の権限を与えられるし] をクリックするアカウントの名前を入力**名前の確認**します。 アカウントの名前に下線が引かれますをクリックして**OK**に戻るに、**メンバー** ] タブ。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_153.gif)  
  
5.  **メンバー**タブに移動して、 **Domain Admins のプロパティ**ダイアログ ボックスで、をクリックして**適用**します。 クリックすると**適用**が発生しないことのエラー メッセージ、アカウントが DA グループのメンバーを維持する必要があります。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_154.gif)  
  
6.  をクリックして、**によって管理されている**] タブで、 **Domain Admins のプロパティ**] ダイアログ ボックスことを確認してすべてのフィールドにテキストを入力できないすべてのボタンが淡色表示にします。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_155.gif)  
  
7.  をクリックして、**全般**] タブで、 **Domain Admins のプロパティ**] ダイアログ ボックスし、そのタブに関する情報のいずれかを変更できないことを確認します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_156.gif)  
  
8.  必要に応じて、追加の保護グループを次の手順を繰り返します。 完了したら、ログに記録を有効にし、管理アカウントを無効に作成したグループのメンバであるアカウントを使用してセキュリティで保護された管理ホストにログオンします。 だけでテストされ、アカウントを無効にするには、管理アカウントのパスワードをリセットし、します。 管理アカウントとグループを有効にして、アカウントを無効にするとの責任を負うがセットアップを完了しました。  
  


