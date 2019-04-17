---
ms.assetid: 5b2876ac-fe7d-4054-bfba-b692e57bc0d2
title: "付録 C: Active Directory のアカウントとグループの保護"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c1d29b61844428115f8b2d1f5d935f225a249659
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>付録 c: 保護されたアカウントと Active Directory のグループ

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012


## <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>付録 c: 保護されたアカウントと Active Directory のグループ  
Active Directory 内で、保護されたアカウントとグループに、高い権限を持つアカウントとグループの既定のセットと見なされます。 Active Directory のほとんどのオブジェクト、代理管理者 (Active Directory オブジェクトを管理するアクセス許可を委任されているユーザー) はなどのグループのメンバーシップを変更する自体を許可するアクセス許可を変更するなど、オブジェクトに対するアクセス許可を変更できます。  

ただし、保護されたアカウントとグループ、オブジェクトのアクセス許可設定され適用される場合でも、オブジェクトは、一貫性のあるオブジェクトはへのアクセス許可、ディレクトリを移動することを確認する自動処理します。 保護されたオブジェクトのアクセス許可を手動で変更された誰か場合でもこの処理によって、アクセス許可がその既定値を迅速に返されることです。  

### <a name="protected-groups"></a>保護されたグループ  
次の表には、ドメイン コント ローラーのオペレーティング システムで表示されている Active Directory 内の保護グループが含まれています。  

**オペレーティング システムで Active Directory の保護されたアカウントとグループ**  

|||||  
|-|-|-|-|  
|**Windows 2000 < SP4**|**Windows 2000 SP4、Windows Server 2003 RTM**|**Windows Server 2003 SP1 +**|**Windows Server 2012、Windows Server 2008 R2、Windows Server 2008**|  
|管理者|アカウント オペレーター|アカウント オペレーター|アカウント オペレーター|  
||管理者|管理者|管理者|  
||管理者|管理者|管理者|  
||バックアップ オペレーター|バックアップ オペレーター|バックアップ オペレーター|  
||Cert Publishers|||  
|Domain Admins|Domain Admins|Domain Admins|Domain Admins|  
||ドメイン コント ローラー|ドメイン コント ローラー|ドメイン コント ローラー|  
|Enterprise Admins|Enterprise Admins|Enterprise Admins|Enterprise Admins|  
||Krbtgt|Krbtgt|Krbtgt|  
||演算子を印刷します|演算子を印刷します|演算子を印刷します|  
||||読み取り専用ドメイン コント ローラー|  
||レプリケーター|レプリケーター|レプリケーター|  
|Schema Admins|Schema Admins|Schema Admins|Schema Admins|  
||サーバー オペレーター|サーバー オペレーター|サーバー オペレーター|  

#### <a name="adminsdholder"></a>AdminSDHolder  
AdminSDHolder オブジェクトの目的は、ドメイン内の保護されたアカウントとグループ「テンプレート」のアクセス許可を提供することです。 AdminSDHolder は、すべての Active Directory ドメインのシステム コンテナー内のオブジェクトとして自動的に作成されます。 パスには: **CN AdminSDHolder、CN = System, DC = < domain_component > = DC = < domain_component > ですか。**  

Administrators グループが所有している、Active Directory ドメイン内のほとんどのオブジェクトとは異なり、Domain Admins グループ AdminSDHolder が所有します。 既定では、EAs を変更できる、任意のドメインの AdminSDHolder オブジェクトと、ドメインの Domain Admins と Administrators グループのことができます。 さらに、AdminSDHolder の既定の所有者は、ドメインの Domain Admins グループが、管理者または Enterprise Admins のメンバーの所有権オブジェクト。  

#### <a name="sdprop"></a>SDProp  
SDProp は、ドメインの PDC エミュレーター (PDCE) を持つドメイン コント ローラー上 (既定) では 60 分間隔で実行されるプロセスです。 SDProp は、保護されたアカウントと、ドメイン内のグループのアクセス許可を持つ、ドメインの AdminSDHolder オブジェクトに対するアクセス許可を比較します。 保護されたアカウントとグループのいずれかのアクセス許可で AdminSDHolder オブジェクトに対するアクセス許可が一致しない場合、ドメインの AdminSDHolder オブジェクトのものと一致する保護されたアカウントとグループのアクセス許可がリセットされます。  

さらに、アクセス許可の継承が無効で、保護グループとアカウント、意味する場合でも、アカウントとグループをディレクトリ内の別の場所に移動、権限を継承しない、新しい親オブジェクトからです。 親オブジェクトへのアクセス許可の変更は AdminSDHolder のアクセス許可を変更しないように AdminSDHolder オブジェクトの継承が無効です。  

##### <a name="changing-sdprop-interval"></a>SDProp 間隔を変更します。  
通常、SDProp 実行に使用する、テスト目的でを除く時間の間隔を変更する必要はありません。 ドメインの PDCE で、SDProp 間隔を変更する必要がある場合は、regedit を使用して追加または \system\currentcontrolset\services\ntds\parameters の AdminSDProtectFrequency DWORD 値を変更します。  

値の範囲は 7200 (2 時間に 1 分) を 60 秒です。 変更を反転するには、これにより、60 分間隔に戻す SDProp AdminSDProtectFrequency キーを削除します。 一般に必要がありますしないこの間隔の軽減運用ドメインと LSASS のドメイン コント ローラーの処理のオーバーヘッドを増やすことができます。 この増加の影響は、ドメイン内の保護されたオブジェクトの数に依存します。  

##### <a name="running-sdprop-manually"></a>SDProp を手動で実行しています。  
AdminSDHolder 変更をテストする方が、SDProp を手動で実行をすぐに実行するタスクがスケジュールされた実行には影響しません。 Windows Server 2008 を実行するドメイン コント ローラーに少し異なる方法で実行し、Windows Server 2012 または Windows Server 2008 R2 を実行するドメイン コント ローラー上にあるより前は、SDProp を手動で実行されています。  

以前のオペレーティング システムで SDProp を手動で実行するための手順が用意されて[Microsoft サポートの記事 251343](https://support.microsoft.com/kb/251343)、し、古いおよびそれ以降のオペレーティング システムの詳細な手順を次に示します。 どちらの場合に、Active Directory の rootDSE オブジェクトに接続し、操作の名前を変更する属性として指定、rootDSE オブジェクトの null DN の変更操作を実行する必要があります。 RootDSE オブジェクトに対する変更可能な操作の詳細については、次を参照してください。 [rootDSE 変更操作](https://msdn.microsoft.com/library/cc223297.aspx)、MSDN web サイト。  

###### <a name="running-sdprop-manually-in-windows-server-2008-or-earlier"></a>Windows Server 2008 またはそれ以前に手動で実行中の SDProp  
Ldp.exe を使用して、または LDAP 修正スクリプトを実行して、実行する SDProp を強制することができます。 SDProp Ldp.exe を使用してを実行するには、ドメイン内の AdminSDHolder オブジェクトに変更を行った後、次の手順を実行します。  

1.  起動**Ldp.exe**します。  

2.  をクリックして**接続**Ldp] ダイアログ ボックスで**接続**します。  

    ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_9.gif)  

3.  **接続**] ダイアログ ボックスで、PDC エミュレーター (PDCE) の役割を持つドメインのドメイン コント ローラーの名前を入力し、をクリックして**OK**します。  

    ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_10.png)  

4.  によって示されている、正常に接続していることを確認する**Dn: (RootDSE)**次のスクリーン ショット] をクリックして**接続**] をクリック**バインド**します。  

    ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_11.png)  

5.  **バインド**] ダイアログ ボックスに、rootDSE オブジェクトを変更するアクセス許可を持つユーザー アカウントの資格情報を入力します。 (そのユーザーとしてログオンしている場合は選択**としてバインド**現在ログオンしているユーザー)。をクリックして**OK**します。  

    ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_12.png)  

6.  バインド操作を完了したら、クリックして**参照**、] をクリック**変更**します。  

    ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_13.png)  

7.  **変更**ダイアログ ボックスで、退出、 **DN**フィールドを空白です。 **エントリ属性の編集**フィールドを入力**FixUpInheritance**、し、[、**値**フィールドを入力**はい**します。 をクリックして**Enter**を設定する、**エントリ一覧**次のスクリーン ショットに示すようにします。  

    ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_14.gif)  

8.  設定の変更] ダイアログ ボックスで実行] をクリックし、そのオブジェクトの AdminSDHolder オブジェクトに加えられた変更が表示されていることを確認します。  

> [!NOTE]  
> 保護グループのメンバーシップを変更する権限を持たないアカウントの指定を許可するように AdminSDHolder の変更については、次を参照してください。[付録 i: 管理アカウントを作成する Active Directory 内の保護されるアカウントとグループ](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)します。  

LDIFDE またはスクリプトを使用して SDProp を手動で実行する場合は、次のように変更エントリを作成できます。  

![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_15.gif)  

###### <a name="running-sdprop-manually-in-windows-server-2012-or-windows-server-2008-r2"></a>Windows Server 2012 または Windows Server 2008 R2 で SDProp を手動で実行しています。  
Ldp.exe を使用して、または LDAP 修正スクリプトを実行して、実行する SDProp を強制することもできます。 SDProp Ldp.exe を使用してを実行するには、ドメイン内の AdminSDHolder オブジェクトに変更を行った後、次の手順を実行します。  

1.  起動**Ldp.exe**します。  

2.  **Ldp**ダイアログ ボックスで、をクリックして**接続**、] をクリック**接続**します。  

    ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_16.gif)  

3.  **接続**] ダイアログ ボックスで、PDC エミュレーター (PDCE) の役割を持つドメインのドメイン コント ローラーの名前を入力し、をクリックして**OK**します。  

    ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_17.gif)  

4.  によって示されている、正常に接続していることを確認する**Dn: (RootDSE)**次のスクリーン ショット] をクリックして**接続**] をクリック**バインド**します。  

    ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_18.gif)  

5.  **バインド**] ダイアログ ボックスに、rootDSE オブジェクトを変更するアクセス許可を持つユーザー アカウントの資格情報を入力します。 (そのユーザーとしてログオンしている場合は選択**現在ログオンしているユーザーのバインド**.)をクリックして**OK**します。  

    ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_19.gif)  

6.  バインド操作を完了したら、クリックして**参照**、] をクリック**変更**します。  

    ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_20.gif)  

7.  **変更**ダイアログ ボックスで、退出、 **DN**フィールドを空白です。 **エントリ属性の編集**フィールドを入力**RunProtectAdminGroupsTask**、し、[、**値**フィールドを入力**1**します。 をクリックして**Enter**に次のようにエントリの一覧を入力します。  

    ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_21.gif)  

8.  データが設定された**変更**ダイアログ ボックスで、] をクリックして**実行**、そのオブジェクトの AdminSDHolder オブジェクトに加えられた変更が表示されていることを確認します。  

LDIFDE またはスクリプトを使用して SDProp を手動で実行する場合は、次のように変更エントリを作成できます。  

![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_22.gif)  
