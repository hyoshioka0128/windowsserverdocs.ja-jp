---
ms.assetid: 13fe87d9-75cf-45bc-a954-ef75d4423839
title: 付録 I – 保護されたアカウントと Active Directory でグループの管理アカウントを作成します。
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e90c2c075ba2dc2b63e9a18c9eba192116265b90
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443525"
---
# <a name="appendix-i-creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>付録 i:Active Directory 内の保護されたアカウントとグループ アカウントの管理の作成

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

高い特権を持つグループの永続的なメンバーシップに依存せず、Active Directory のモデルを実装する課題の 1 つは、一時的なグループのメンバーシップが必要な場合は、これらのグループを設定するためのメカニズムが存在しなければなりません。 一部の privileged identity management ソリューションでは、DA など、フォレスト内の各ドメインの管理者グループのメンバーシップを永続的なソフトウェアのサービス アカウントが与えられている必要があります。 ただし、技術的には必要はありません Privileged Identity Management (PIM) の解決策を高い特権を持つこのようなコンテキストでそのサービスを実行します。  
  
この付録で説明する限られた特権と、厳密制御できますが、Active Directory で権限を持つグループを設定するために使用するアカウントを作成するネイティブ実装済みまたはサード パーティの PIM ソリューションを使用できる情報と一時的な昇格が必要です。 一時的なグループの作成を実行する管理スタッフによるこれらのアカウントの使用をネイティブのソリューションとして PIM を実装する場合と、サード パーティのソフトウェアを使用して PIM を実装する場合にこれらのアカウントをサービスとしての関数を適応できる可能性があります。アカウント。  
  
> [!NOTE]  
> この付録で説明する手順は、高い特権を持つ Active Directory グループの管理方法の 1 つを提供します。 ニーズに合わせて、追加の制限を追加する手順を調整したり、ここで説明されている制限の一部を省略できます。  
  
## <a name="creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>Active Directory 内の保護されたアカウントとグループ アカウントの管理の作成

詳細な手順で説明されている 4 つの一般的なアクティビティから成る過剰な権限とアクセス許可を付与する管理アカウントを必要とすることがなく、特権を持つグループのメンバーシップを管理するアカウントの作成を使用します。従います。  
  
1.  まず、限られた一連の信頼されたユーザーによってこれらのアカウントを管理する必要があるため、アカウントを管理するグループを作成する必要があります。 ドメイン内の一般的な母集団から隔離することと保護された特権のアカウントとシステムに対応する OU 構造がいない場合は、1 つを作成する必要があります。 具体的な手順については、この付録では提供されていない、ですが、スクリーン ショットは、このような OU 階層の例を示します。  
  
2.  管理アカウントを作成します。 これらのアカウントを「通常」のユーザー アカウントとして作成および既定では、ユーザーに既に付与されているもの以外のユーザー権限を与えないようにする必要があります。  
  
3.  管理アカウントを作成されただけでなくユーザーを制御するを有効にするアカウント (最初の手順で作成したグループ) を使用して、特殊な目的でのみ使用できるようにするには、制限事項を実装します。  
  
4.  ドメイン内の特権グループのメンバーシップを変更する管理アカウントを許可するには、各ドメイン内の AdminSDHolder オブジェクトのアクセス許可を構成します。  
  
綿密なすべての手順をテストして、実稼働環境に実装する前に、環境の必要に応じてそれらを変更する必要があります。 すべての設定が期待どおりに動作するも確認する必要があります (一部のテスト手順は、この付録で提供されますが、) し、管理アカウントのないを使用して保護グループの回復の設定を使用可能なディザスター リカバリー シナリオをテストする必要があります目的。 バックアップと復元の Active Directory の詳細については、次を参照してください。、 [AD DS のバックアップと復元のステップ バイ ステップ ガイド](https://technet.microsoft.com/library/cc771290(v=ws.10).aspx)します。  
  
> [!NOTE]  
> この付録で説明する手順を実装すると、各ドメイン内のすべての保護グループ、EAs、DAs および BAs のような最も高い特権 Active Directory のグループだけでなくのメンバーシップを管理できるアカウントを作成します。 Active Directory の保護されたグループの詳細については、次を参照してください[付録 c:。Active Directory のアカウントとグループの保護](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)します。  
  
### <a name="step-by-step-instructions-for-creating-management-accounts-for-protected-groups"></a>保護グループの管理アカウントを作成する手順  
  
#### <a name="creating-a-group-to-enable-and-disable-management-accounts"></a>管理アカウントを無効にするグループを作成します。

管理アカウントは、自分のパスワードを使用するたびにリセットする必要がありますがあるし、それらを必要とするアクティビティが完了するときに、無効にする必要があります。 これらのアカウントのスマート カード ログオン要件を実装することも検討、オプションの構成は、これらの手順は、管理アカウントをユーザー名と最小値として複雑なパスワードを構成することを想定していますコントロール。 この手順では、管理アカウントのパスワードをリセットし、、有効にして、アカウントを無効にするアクセス許可を持つグループを作成します。  
  
管理アカウントを無効にするグループを作成するには、次の手順を実行します。  
  
1.  管理アカウントを格納する OU 構造でグループを作成する OU を右クリックしをクリックして**新規** をクリック**グループ**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_115.png)  
  
2.  **新しいオブジェクト - グループ** ダイアログ ボックスに、グループの名前を入力します。 このグループを使用して、フォレスト内のすべての管理アカウントを「アクティブ化」する場合は、ようにユニバーサル セキュリティ グループを指定します。 単一ドメイン フォレストがある場合、または各ドメインでグループを作成する場合は、グローバル セキュリティ グループを作成することができます。 **[OK]** をクリックしてグループを作成します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_116.png)  
  
3.  作成したばかりのグループを右クリックし、 **[プロパティ]** をクリックし、 **[オブジェクト]** タブをクリックします。グループの**オブジェクト プロパティ**ダイアログ ボックスで、**オブジェクトを誤って削除されないように保護**、これのみ防ぐことはできません、承認済みユーザー、グループから削除、移動することからも別の OU 属性が最初にない場合は選択解除。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_117.png)  
  
    > [!NOTE]  
    > グループの親の管理を限られたユーザーを制限する Ou で既にアクセス許可を構成した場合、次の手順を実行する必要はありません。 記載されて制限付きの管理制御するには、このグループを作成した OU 構造を実装していない場合でも、変更に対するグループをセキュリティで保護できますように承認されていないユーザーです。  
  
4.  をクリックして、**メンバー**タブをクリックし、必要に応じてグループが管理アカウントの有効化または作成を担当するチームのメンバーに保護されているアカウントを追加します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_118.png)  
  
5.  既に行われていない場合などに、 **Active Directory ユーザーとコンピューター**コンソールで、**ビュー**選択と**高度な機能**します。 作成したグループを右クリックし、をクリックして**プロパティ**、 をクリックし、**セキュリティ**タブ。**セキュリティ** タブで、 **詳細設定**をクリックします。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_119.png)  
  
6.  **Advanced Security Settings for [グループ]** ダイアログ ボックスで、をクリックして**継承を無効にする**します。 メッセージが表示されたら、クリックして**継承されたアクセス許可には、このオブジェクトの明示的なアクセス許可を変換**、 をクリック**ok**を返すには、グループの**セキュリティ** ダイアログ ボックス。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_120.png)  
  
7.  **セキュリティ** タブで、このグループのアクセスを許可する必要がありますはないグループを削除します。 たとえば、Authenticated Users グループの名前と全般的なプロパティを読み取ることができるしたくない場合は、その ACE を削除できます。 アカウントへの演算子と pre-Windows 2000 Server 互換性のあるアクセスなど Ace を削除することもできます。 インプレース オブジェクトのアクセス許可の最小セットしておく必要があります、ただし。 次の Ace をそのままにします。  
  
    -   SELF  
  
    -   システム  
  
    -   Domain Admins  
  
    -   Enterprise Admins  
  
    -   管理者  
  
    -   Windows Authorization Access Group (該当する場合)  
  
    -   ENTERPRISE のドメイン コント ローラー  
  
    このグループを管理する Active Directory で最高の特権を持つグループを可能にする直感に反する感じるかもしれませんが、これらの設定を実装する目標はそれらのグループのメンバーが承認された変更を加えることを防ぐ。 代わりに、目標は、非常に高いレベルの特権を必要とする場合がある場合は、承認された変更が成功することを確認します。 このための特権グループの入れ子、権限の既定を変更することと、このドキュメント全体のアクセス許可は推奨されません。 既定の構造をそのまま残して、ディレクトリ内の最上位の特権グループのメンバーシップを空にして、想定どおりに機能をより安全な環境を作成できます。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_121.png)  
  
    > [!NOTE]  
    > このグループを作成した OU 構造のオブジェクトの監査ポリシーをまだ構成していない場合は、する必要があります監査を構成する変更をログにこのグループ。  
  
8.  「チェック アウト」に使用されるグループの構成を完了する管理アカウントが必要ですし、「チェックイン」アカウントは、そのアクティビティが完了するとします。  
  
#### <a name="creating-the-management-accounts"></a>管理アカウントを作成します。

少なくとも 1 つのアカウント、Active Directory インストールでの特権グループのメンバーシップを管理するために使用して、可能であれば、バックアップとして使用する 2 つ目のアカウントを作成する必要があります。 1 つのドメイン、フォレスト内で管理アカウントを作成し、すべてのドメインの管理機能を付与を選択するかどうかの保護グループ、または、プロシージャは、各ドメイン、フォレスト内の管理アカウントを実装するために選択するかどうか実質的に同じです。  
  
> [!NOTE]  
> このドキュメントの手順では、したがまだ実装されていないこと、ロールベースのアクセス制御と Active Directory privileged identity management を前提としています。 そのため、問題のドメインの Domain Admins グループのメンバーであるアカウントを持つユーザーがいくつかの手順を実行する必要があります。  
>   
> DA 特権を持つアカウントを使用する場合、構成操作を実行するドメイン コント ローラーにログオンできます。 DA 特権を必要としない手順は、管理ワークステーションにログオンしている低特権アカウントで実行できます。 明るい青色の枠線 ダイアログ ボックスを表示するスクリーン ショットでは、ドメイン コント ローラーで実行できるアクティビティを表します。 濃い青の色 ダイアログ ボックスを表示するスクリーン ショットでは、管理ワークステーションが限られた特権アカウントで実行できるアクティビティを表します。  
  
管理アカウントを作成するには、次の手順を実行します。  
  
1. ドメインの DA グループのメンバーであるアカウントを使用してドメイン コント ローラーにログオンします。  

2. 起動**Active Directory ユーザーとコンピューター**管理アカウントを作成する OU に移動します。  

3. OU を右クリックし、をクリックして**新規**クリック**ユーザー**します。  

4. **新しいオブジェクト - ユーザー**  ダイアログ ボックスで、アカウントの場合は、必要な名前付け情報を入力してをクリックして**次**します。  

   ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_122.png)  
  
5. ユーザー アカウントのチェック ボックスをオフ、初期パスワードを提供**ユーザーは次回ログオン時にパスワードを変更する必要があります**を選択します**ユーザーがパスワードを変更できない**と**アカウントが無効になっている**とクリックして**次**します。  

   ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_123.png)  

6. アカウントの詳細が正しいことを確認 をクリックして**完了**します。  

7. 作成したユーザーのオブジェクトを右クリックし、をクリックして**プロパティ**します。  

8. をクリックして、**アカウント**タブ。  

9. **アカウント オプション**フィールドで、選択、**アカウントは重要なので委任できない**フラグは、選択、**このアカウントは、Kerberos AES 128 ビット暗号化をサポートしている**や**このアカウントは、Kerberos AES 256 暗号化をサポートする**フラグが設定し、をクリックして**OK**します。  

   ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_124.png)  

   > [!NOTE]  
   > その他のアカウントと同様、このアカウントが限られており、かつ強力な関数であるため、アカウントはセキュリティで保護された管理ホストでのみ使用する必要があります。 すべてのセキュリティで保護された管理ホスト環境内で、グループ ポリシー設定の実装を検討する必要があります**ネットワーク セキュリティ。Kerberos で許可する暗号化の種類を構成する**最も安全な暗号化の種類のみを許可するセキュリティで保護されたホストを実行できます。  
   >
   > ホストのより安全な暗号化の種類の実装も資格情報盗難攻撃が軽減されませんが、適切な使用とセキュリティで保護されたホストの構成では。 コンピューターの全体的な攻撃対象領域を減らすだけ権限を持つアカウントでのみ使用されるホストのより強力な暗号化の種類を設定します。  
   >
   > システムとのアカウントでの暗号化の種類を構成する方法の詳細については、次を参照してください。 [Kerberos サポートされている暗号化の種類の Windows 構成](http://blogs.msdn.com/b/openspecification/archive/2011/05/31/windows-configurations-for-kerberos-supported-encryption-type.aspx)します。  
   >
   > これらの設定は、Windows Server 2012、Windows Server 2008 R2、Windows 8、または Windows 7 を実行しているコンピューターでのみサポートされます。  
  
10. **オブジェクト**] タブで [**オブジェクトを誤って削除されないように保護**します。 これはのみができないオブジェクト (承認されたユーザーの場合) によっても削除されないというされますが、AD DS 階層内の別の OU に移動してからない場合は、属性を変更する権限を持つユーザーでは、チェック ボックスはオフ最初。  

    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_125.png)  

11. をクリックして、**リモート_コントロール**タブ。  

12. クリア、**リモート_コントロールを有効にする**フラグ。 サポート スタッフに修正を実装するためにこのアカウントのセッションへの接続に必要になることはありません必要があります。  

    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_126.png)  

    > [!NOTE]  
    > 」の説明に従って、Active Directory のすべてのオブジェクトを指定された IT 所有者と、指定のビジネス所有者が必要[侵害対策を計画](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)します。 (外部データベース) ではなく Active Directory の AD DS オブジェクトの所有権を追跡している場合は、このオブジェクトのプロパティで適切な所有権情報を入力する必要があります。  
    >
    > この場合は、ビジネス オーナーは、IT 部門ではほとんどの場合、返しにも IT 所有者されているビジネス オーナーの禁止はありません。 オブジェクトの所有権を確立するポイントでは、変更する必要があります、オブジェクトにおそらく年最初の作成から連絡先を特定することを許可します。  

13. をクリックして、**組織**タブ。  

14. AD DS オブジェクトの基準で必要なすべての情報を入力します。  

    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_127.png)  

15. をクリックして、**ダイヤルイン**タブ。  

16. **ネットワーク アクセス許可**フィールドで、**アクセスを拒否する**します。このアカウントは必要がありますしないリモート接続で接続する必要があります。  

    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_128.png)  

    > [!NOTE]  
    > このアカウントが環境内で読み取り専用ドメイン コント ローラー (Rodc) にログオンに使用されること可能性が高いことはできません。 ただし、必要がありますの状況がログオンするアカウント、RODC にログオンする必要がありますアカウントを追加するこの Denied RODC Password Replication Group にそのパスワードが RODC にキャッシュされないようにします。  
    >
    > 使用後に、アカウントのパスワードをリセットするか、アカウントを無効にする、この設定を実装しても、アカウントに有害な影響はありませんし、アカウントのリセットを管理者が忘れた場合の状況でわかりやすくなりますパスワードは無効にします。  

17. **[所属するグループ]** タブをクリックします。  

18. **[追加]** をクリックします。  

19. 型**Denied RODC Password Replication の Group**で、 **[ユーザー、連絡先、コンピューター** ] ダイアログ ボックスをクリックします**名前の確認**します。 オブジェクト ピッカーでグループの名前に下線を引く、 をクリックして**OK**し、アカウントが次のスクリーン ショットに表示される 2 つのグループのメンバーでようになりましたことを確認します。 保護グループにアカウントを追加しないでください。  

20. **[OK]** をクリックします。  

    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_129.png)  

21. をクリックして、**セキュリティ** タブでをクリックし、**詳細**します。  

22. **セキュリティの詳細設定**ダイアログ ボックスで、をクリックして**継承を無効にする**として明示的なアクセス許可、継承されたアクセス許可をコピーしをクリックし、**追加**。  

    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_130.png)  

23. **[アカウント] のアクセス許可エントリ**ダイアログ ボックスで、をクリックして**プリンシパルの選択**し、前の手順で作成したグループに追加します。 ダイアログ ボックスの一番下までスクロールし、をクリックして**すべてクリア**すべて既定のアクセス許可を削除します。  

    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_131.png)  

24. ページのトップへのスクロール、**アクセス許可エントリ** ダイアログ ボックス。 いることを確認、**型**にドロップダウン リストが設定されている**許可**、し、**に適用されます**ドロップダウン リストで、**このオブジェクトのみ**します。  

25. **権限**フィールドで、**すべてのプロパティを読み取る**、**読み取りアクセス許可**と**パスワードのリセット**します。  

    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_132.png)  

26. **プロパティ**フィールドで、 **userAccountControl を読み取る**と**userAccountControl を書き込む**します。  

27. をクリックして**ok**、 **OK**で再度、**セキュリティの詳細設定** ダイアログ ボックス。  

    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_133.png)  

    > [!NOTE]  
    > **UserAccountControl**属性は複数のアカウントの構成オプションを制御します。 属性に対する書き込み権限を付与する場合は、構成オプションの一部のみを変更するアクセス許可を付与することはできません。  

28. **グループまたはユーザー名**のフィールド、**セキュリティ** タブで、アクセスしたり、アカウントの管理を許可する必要がありますすべてのグループを削除します。 Everyone グループと SELF 計算アカウントなど、Deny Ace で構成されているすべてのグループを削除しないでください (その ACE が設定されたときに、**ユーザーがパスワードを変更できない**フラグが、アカウントの作成時に有効になっています。 また、グループを追加した、システム アカウント、または EA、DA、BA、または、Windows Authorization Access Group などのグループは削除しないでください。  

    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_134.png)  

29. クリックして**詳細**し、セキュリティの詳細設定 ダイアログ ボックスは次のスクリーン ショットのようなことを確認します。  

30. をクリックして**OK**、および**OK**アカウントのプロパティ ダイアログ ボックスを閉じます。  

    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_135.png)  

31. 最初の管理アカウントのセットアップが完了しました。 後の手順では、アカウントをテストします。  

##### <a name="creating-additional-management-accounts"></a>追加の管理アカウントを作成します。

前の手順を繰り返すことによって、作成したアカウントをコピーすることによって、または、必要な構成設定でアカウントを作成するスクリプトを作成するには、追加の管理アカウントを作成できます。 ただし、先ほど作成したアカウントをコピーする場合、Acl、カスタマイズした設定の多くは、新しいアカウントにコピーされませんし、ほとんどの構成手順を繰り返す必要がありますに注意してください。  
  
代わりと保護対象のグループを unpopulate を挿入する権限を委任するグループを作成することができますが、グループとそこに配置するアカウントをセキュリティで保護する必要があります。 保護グループのメンバーシップを管理する権限が付与されますが、ディレクトリ内のごく少数のアカウントを設定する必要があります、個々 のアカウントを作成すると最も簡単な方法可能性があります。  
  
管理アカウントの配置先のグループを作成するを選択する方法にかかわらず、前述のように各アカウントがセキュリティで保護されるようにしてください。 説明したような GPO の制限事項の実装を検討する必要がありますも[付録 d:Active Directory でビルトイン Administrator アカウントを保護する](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)します。  
  
##### <a name="auditing-management-accounts"></a>管理アカウントの監査

アカウントにすべての書き込みを少なくとも、ログイン アカウントの監査を構成する必要があります。 これにより、成功したアカウントの有効化と、アカウントを操作する権限のないユーザーによる試行を特定することもが、承認済みの使用時にそのパスワードのリセットを特定するだけでなくが許可されます。 アカウントの書き込みが失敗したが、セキュリティ情報およびイベントの監視 (SIEM) システムの (該当する) 場合、キャプチャする必要があり、潜在的な侵害を調査担当スタッフに通知を提供するアラートをトリガーする必要があります。  
  
SIEM ソリューション (たとえば、イベント ログ、アプリケーション データ、ネットワーク ストリーム、マルウェア対策製品、および侵入の検出ソース) に関連するセキュリティ ソースからイベント情報を取得、データの照合、インテリジェントなビューと事前対応型のアクションを作成しようとしています. 市販の多くの SIEM ソリューションは、多くの企業がプライベートな実装を作成する. 適切に設計された、適切に実装されている SIEM は、セキュリティの監視とインシデント対応機能に大幅に向上させることができます。 ただし、機能と精度異なります大幅ソリューション。 Siem が、このホワイト ペーパーの範囲を超えていますが、任意の SIEM 実装者に含まれている特定のイベントの推奨事項を考慮する必要があります。  
  
ドメイン コント ローラーの推奨される監査の構成設定の詳細については、次を参照してください。[侵害の兆候の監視の Active Directory](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)します。 ドメイン コント ローラーに固有の構成設定が記載[侵害の兆候の監視の Active Directory](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)します。  
  
#### <a name="enabling-management-accounts-to-modify-the-membership-of-protected-groups"></a>保護グループのメンバーシップを変更する管理アカウントを有効にします。

この手順では、新しく作成された管理アカウント ドメイン内の保護グループのメンバーシップを変更するように、ドメインの AdminSDHolder オブジェクトに対するアクセス許可を構成します。 グラフィカル ユーザー インターフェイス (GUI) を使用して、この手順を実行することはできません。  
  
説明したよう[付録 c:Active Directory のアカウントとグループの保護](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)、SDProp タスクが実行されるオブジェクトは、実質的に「コピー」ドメインの AdminSDHolder で ACL がオブジェクトを保護します。 保護グループとアカウントを継承しないそのアクセス許可の AdminSDHolder オブジェクトそのアクセス許可は、AdminSDHolder オブジェクトと一致するように明示的に設定されます。 そのため、AdminSDHolder オブジェクトに対するアクセス許可を変更するときに対象としている保護されたオブジェクトの型に適切な属性を変更する必要があります。  
  
この場合、それらを読み取るとグループ オブジェクトで、メンバーの属性の書き込みを許可する、新しく作成された管理アカウント許可しているされます。 ただし、AdminSDHolder オブジェクトは、グループ オブジェクトではないと、グループの属性は、グラフィカル ACL エディターでは公開されません。 このため、Dsacls コマンド ライン ユーティリティを使用してアクセス許可の変更を実装することがあります。 (無効) の管理の保護グループのメンバーシップを変更するアカウントのアクセス許可を付与するには、次の手順を実行します。  
  
1. 可能であれば、ドメイン コント ローラー、PDC エミュレーター (PDCE) の役割をドメイン内のデータ グループのメンバーが作成されているユーザー アカウントの資格情報を保持しているドメイン コント ローラーにログオンします。  
  
   ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_136.png)  
  
2. 右クリックし、管理者特権でコマンド プロンプトを開く**コマンド プロンプト**クリック**管理者として実行**します。  
  
   ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_137.gif)  
  
3. 昇格を承認するメッセージが表示されたら、クリックして**はい**します。  
  
   ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_138.gif)  
  
   > [!NOTE]  
   > Windows で使用した昇格とユーザー アカウント制御 (UAC) の詳細については、次を参照してください。 [UAC プロセスとの対話](https://technet.microsoft.com/library/dd835561(v=WS.10).aspx)TechNet web サイト。  
  
4. コマンド プロンプト (、ドメイン固有の情報を置き換える) の種類で**Dsacls [自分のドメイン内の AdminSDHolder オブジェクトの識別名]/G [管理アカウント UPN]: RPWP; メンバー**します。  
  
   ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_139.gif)  
  
   (これは大文字小文字を区別しない) 前のコマンドはように動作します。  
  
   - Dsacls を設定またはディレクトリ オブジェクトの Ace を表示します。  
  
   - CN AdminSDHolder、CN = System, DC = = 含ま, DC = msft が変更されるオブジェクトを識別します  
  
   - /G の許可 ACE が構成されていることを示します  
  
   - PIM001@tailspintoys.msft Ace を許可するセキュリティ プリンシパルのユーザー プリンシパル名 (UPN) は、します。  
  
   - プロパティを読み取りし、書き込みのアクセス許可を RPWP 許可  
  
   - メンバーは、アクセス許可を設定するプロパティ (属性) の名前が、します。  
  
   使用の詳細については**Dsacls**、コマンド プロンプト パラメーターを指定せず、Dsacls を入力します。  
  
   ドメインの複数の管理アカウントを作成した場合は、アカウントごとに Dsacls コマンドを実行する必要があります。 AdminSDHolder オブジェクトの ACL 構成が完了したら、SDProp 実行、またはスケジュールされた実行が完了するまでの待機を強制する必要があります。 実行する SDProp の強制の詳細についてを参照してください「を実行している SDProp 手動で」[付録 c:Active Directory のアカウントとグループの保護](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)します。  
  
   SDProp が実行すると、保護対象のグループ、ドメイン内の AdminSDHolder オブジェクトに加えた変更が適用されたことを確認できます。 これは前に説明した理由の AdminSDHolder オブジェクトの ACL を表示して確認することはできませんが、保護グループの Acl を表示することによって、アクセス許可が適用されていることを確認できます。  
  
5. **Active Directory ユーザーとコンピューター**、有効にしたことを確認**高度な機能**します。 これを行うには、次のようにクリックします。**ビュー**、検索、 **Domain Admins**グループ化、グループを右クリックおよびクリック**プロパティ**します。  
  
6. をクリックして、**セキュリティ** タブでをクリックし、 **詳細設定**を開く、 **Advanced Security Settings for Domain Admins**  ダイアログ ボックス。  
  
   ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_140.gif)  
  
7. 選択**管理アカウントを許可する ACE**  をクリック**編集**します。 アカウントがのみ与えられていることを確認**メンバーを読み取る**と**メンバーの書き込み** をクリックし、DA グループに対するアクセス許可**OK**します。  
  
8. をクリックして**ok**で、**セキュリティの詳細設定** ダイアログ ボックスをクリックします**OK** DA グループのプロパティ ダイアログ ボックスを閉じます。  
  
   ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_141.gif)  
  
9. ドメインの他の保護グループの前の手順を繰り返すことができます。アクセス許可は、すべての保護グループに対して同じになります。 このドメイン内の保護グループの管理アカウントの作成と構成が完了しました。  
  
    > [!NOTE]  
    > グループ自体を Active Directory でグループのメンバーシップの書き込みアクセス許可を持つ任意のアカウントに追加もできます。 この動作は仕様であり、無効にすることはできません。 このため、管理アカウントを使用しない場合は無効にならないし、使用されているときに、無効になっているときと密接に、アカウントを監視する必要があります。  
  
#### <a name="verifying-group-and-account-configuration-settings"></a>グループとアカウントの構成設定を確認します。

作成し、構成されているドメイン (を最も高い特権を持つ EA、DA、BA グループを含む) で保護されたグループのメンバーシップを変更できる管理アカウントが、アカウントとその管理グループをされていることを確認する必要があります。正常に作成されます。 検証は、これらの一般的なタスクで構成されます。  
  
1.  グループを有効にし、グループは、のメンバーを有効にするアカウントを無効にして、パスワードのリセットが管理アカウントの他の管理の操作を実行することはできませんを確認する管理アカウントを無効にすることができますをテストします。  
  
2.  追加できることとするメンバーの削除は、ドメイン内のグループを保護できるだけでなく、保護されたアカウントとグループの他のプロパティを変更することはできませんを確認する管理アカウントをテストします。  
  
##### <a name="test-the-group-that-will-enable-and-disable-management-accounts"></a>テスト グループを有効にすると、管理アカウントを無効にします。
  
1.  管理アカウントを有効にして、そのパスワードのリセットをテストするには、セキュリティで保護された管理ワークステーションには、グループのメンバーであるアカウントを使用してで作成したログオン[付録 i:アカウントおよび Active Directory でグループ管理アカウントを作成する保護される](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_142.gif)  
  
2.  開いている**Active Directory ユーザーとコンピューター**管理アカウントを右クリックし、クリックして、**アカウントの有効化**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_143.gif)  
  
3.  アカウントが有効になっていることを確認 ダイアログ ボックスが表示されます。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_144.gif)  
  
4.  次に、管理アカウントのパスワードをリセットします。 これを行うには、アカウントをもう一度右クリックし、をクリックして**パスワードのリセット**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_145.gif)  
  
5.  アカウントの新しいパスワードを入力、**新しいパスワード**と**パスワードの確認入力**フィールド、およびクリック**OK**。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_146.gif)  
  
6.  アカウントのパスワードがリセットされたことを確認するダイアログ ボックスが表示されます。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_147.gif)  
  
7.  管理アカウントの追加のプロパティの変更を試みます。 アカウントを右クリックし、をクリックして**プロパティ**、 をクリックし、**リモート_コントロール**タブ。  
  
8.  選択**リモート_コントロールを有効にする**クリック**適用**。 操作が失敗して、**アクセスが拒否されました**エラー メッセージを表示する必要があります。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_148.gif)  
  
9. をクリックして、**アカウント**タブに移動して、アカウントとアカウントの名前、ログオン時間、またはログオンできるワークステーションを変更しようとしています。 すべてが失敗し、によって制御されないオプションを考慮する必要があります、 **userAccountControl**淡色され、変更のために使用できません、属性を表示する必要があります。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_149.gif)  
  
10. DA グループなどの保護グループに管理グループを追加しようとしてください。 クリックすると**OK**グループを変更するアクセス許可がないことを通知する、メッセージが表示する必要があります。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_150.gif)  
  
11. 構成できないことものを除く、管理アカウントのことを確認するために、追加のテストを実行**userAccountControl**設定とパスワードをリセットします。  
  
    > [!NOTE]  
    > **UserAccountControl**属性は複数のアカウントの構成オプションを制御します。 属性に対する書き込み権限を付与する場合は、構成オプションの一部のみを変更するアクセス許可を付与することはできません。  
  
##### <a name="test-the-management-accounts"></a>テスト管理アカウント

保護グループのメンバーシップを変更できる 1 つまたは複数のアカウントを有効になったため、保護グループのメンバーシップを変更できますが、保護されたアカウントとグループの他の変更を実行することはできませんが、アカウントをテストできます。  
  
1.  最初の管理アカウントとしてセキュリティで保護された管理ホストにログオンします。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_151.gif)  
  
2.  起動**Active Directory ユーザーとコンピューター**探し、 **Domain Admins グループ**します。  
  
3.  右クリックし、 **Domain Admins**をグループ化し、をクリックして**プロパティ**します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_152.gif)  
  
4.  **Domain Admins のプロパティ**、 をクリックして、**メンバー**  タブと**クリックして**追加します。 一時の Domain Admins 特権が与えられますし、アカウントの名前を入力**名前の確認**します。 アカウントの名前に下線を引く、 をクリックして**OK**に戻る、**メンバー**タブ。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_153.gif)  
  
5.  **メンバー**タブに移動して、 **Domain Admins のプロパティ**ダイアログ ボックスで、をクリックして**適用**。 クリックすると**適用**アカウント DA グループのメンバーを維持する必要があります、およびエラー メッセージは発生しません。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_154.gif)  
  
6.  をクリックして、**によって管理されている** タブで、 **Domain Admins のプロパティ** ダイアログ ボックスを任意のフィールドでテキストを入力することはできませんし、すべてのボタンは淡色表示になることを確認します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_155.gif)  
  
7.  をクリックして、**全般** タブで、 **Domain Admins のプロパティ** ダイアログ ボックスし、そのタブに関する情報のいずれかの変更できないことを確認します。  
  
    ![管理アカウントを作成します。](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_156.gif)  
  
8.  必要に応じて、追加の保護グループの次の手順を繰り返します。 完了したら、ログを有効にして、管理アカウントを無効にするために作成したグループのメンバーであるアカウントを使用してセキュリティで保護された管理ホストにログオンします。 そのだけテストして、アカウントを無効にする管理アカウントのパスワードをリセットします。 管理アカウントと有効にして、アカウントを無効化を担当するグループのセットアップが完了しました。  
