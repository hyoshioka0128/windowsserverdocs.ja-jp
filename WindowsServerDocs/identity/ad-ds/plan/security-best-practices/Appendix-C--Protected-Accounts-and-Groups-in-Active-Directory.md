---
ms.assetid: 5b2876ac-fe7d-4054-bfba-b692e57bc0d2
title: 付録 C - Active Directory のアカウントとグループの保護
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 70e29ad42b57cf315c7179d6eea8220ad2bfab48
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834703"
---
# <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>付録 C保護されたアカウントと Active Directory のグループ

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

## <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>付録 C保護されたアカウントと Active Directory のグループ

Active Directory 内で保護されたアカウントとグループには、高い特権を持つアカウントとグループの既定のセットが考慮されます。 委任された管理者 (Active Directory オブジェクトを管理するアクセス許可を委任されているユーザー) と Active Directory でほとんどのオブジェクトのメンバーシップを変更する自体を許可するアクセス許可を変更するなど、オブジェクトに対する権限を変更できます。たとえば、グループ  

ただし、保護されたアカウントとグループの場合は、オブジェクトのアクセス許可が設定および適用により、一貫性のあるオブジェクトがある場合でも、オブジェクトは残りのアクセス許可は、ディレクトリを移動する自動プロセス経由でします。 場合でも、保護されたオブジェクトのアクセス許可を手動で変更だれかがこのプロセスでは、アクセス許可が既定値に迅速に返されることが保証します。  

### <a name="protected-groups"></a>保護されたグループ

次の表には、ドメイン コント ローラーのオペレーティング システムで表示されている Active Directory で保護されたグループが含まれています。  

#### <a name="protected-accounts-and-groups-in-active-directory-by-operating-system"></a>オペレーティング システムで Active Directory で保護されたアカウントおよびグループ

| Windows Server 2003 RTM | Windows Server 2003 SP1 以降 | Windows Server 2012、 <br> Windows Server 2008 R2、 <br> Windows Server 2008 | Windows Server 2016 |
| --- | --- | --- | --- |
|Account Operators|Account Operators|Account Operators|Account Operators|
|管理者|管理者|管理者|管理者|
|管理者|管理者|管理者|管理者|
|Backup Operators|Backup Operators|Backup Operators|Backup Operators|
|Cert Publishers|||
|Domain Admins|Domain Admins|Domain Admins|Domain Admins|
|ドメイン コントローラー|ドメイン コントローラー|ドメイン コントローラー|ドメイン コントローラー|
|Enterprise Admins|Enterprise Admins|Enterprise Admins|Enterprise Admins|
||||Enterprise Key Admins|
||||キーの管理者|
|Krbtgt|Krbtgt|Krbtgt|Krbtgt|
|Print Operators|Print Operators|Print Operators|Print Operators|
|||Read-Only Domain Controllers|Read-Only Domain Controllers|
|Replicator|Replicator|Replicator|Replicator|
|Schema Admins|Schema Admins|Schema Admins|Schema Admins|
|Server Operators|Server Operators|Server Operators|Server Operators|

#### <a name="adminsdholder"></a>AdminSDHolder

AdminSDHolder オブジェクトでは、保護されたアカウントとドメイン内のグループの「テンプレート」アクセス許可を提供します。 AdminSDHolder はすべての Active Directory ドメインのシステム コンテナー内のオブジェクトとして自動的に作成されます。 パスには。**CN=AdminSDHolder,CN=System,DC=<domain_component>,DC=<domain_component>?.**  

Administrators グループが所有している、Active Directory ドメイン内のほとんどのオブジェクトとは異なり、Domain Admins グループ AdminSDHolder が所有します。 既定では、EAs は、ドメインの Domain Admins と管理者グループと同様、任意のドメインの AdminSDHolder オブジェクトに変更を実行できます。 さらに、AdminSDHolder の既定の所有者は、ドメインの Domain Admins グループが、管理者または Enterprise Admins のメンバーのユーザーは、オブジェクトの所有権を取得できます。  

#### <a name="sdprop"></a>SDProp

SDProp は、60 分 (既定) をドメインの PDC エミュレーター (PDCE) を保持するドメイン コント ローラーで実行されるプロセスです。 SDProp は、保護されたアカウントとドメイン内のグループ、アクセス許可を持つ、ドメインの AdminSDHolder オブジェクトに対する権限を比較します。 保護されたアカウントとグループのいずれかのアクセス許可では、AdminSDHolder オブジェクトのアクセス許可は一致しない場合、ドメインの AdminSDHolder オブジェクトと一致するように、保護されたアカウントとグループのアクセス許可がリセットされます。  

さらに、アクセス許可の継承は無効で保護されたグループとアカウントをする場合でも、アカウントとグループは、ディレクトリ内の別の場所に移動、権限を継承しない新しい親オブジェクトからです。 親オブジェクトへのアクセス許可の変更が AdminSDHolder のアクセス許可を変更しないように AdminSDHolder オブジェクトの継承は無効です。  

##### <a name="changing-sdprop-interval"></a>SDProp 間隔を変更します。

通常、テスト目的でを除き、SDProp を実行する間隔を変更する必要はありません。 ドメインの場合、PDCE で、SDProp 間隔を変更する必要がある場合は、regedit を使用して追加または \system\currentcontrolset\services\ntds\parameters AdminSDProtectFrequency DWORD 値を変更します。  

値の範囲は、7200 (2 時間に 1 分) に 60 秒単位です。 変更を反転するには、これにより、60 分間隔に戻す SDProp AdminSDProtectFrequency キーを削除します。 一般にする必要がありますいないを軽減しこの間隔運用ドメインの LSASS のドメイン コント ローラーの処理オーバーヘッドを増やすことができます。 この増加の影響は、ドメインで保護されているオブジェクトの数に依存します。  

##### <a name="running-sdprop-manually"></a>SDProp を手動で実行されています。

AdminSDHolder 変更をテストする方法がよりは SDProp を手動で実行するがすぐに実行するタスクしますが、スケジュールされた実行には影響しません。 Windows Server 2008 を実行するドメイン コント ローラーに対して若干異なる方法で実行し、Windows Server 2012 または Windows Server 2008 R2 を実行するドメイン コント ローラーで実行されるより前は、SDProp を手動で実行します。  

以前のオペレーティング システムで SDProp を手動で実行するための手順が記載[Microsoft サポート記事 251343](https://support.microsoft.com/kb/251343)、および新旧のオペレーティング システムの詳細な手順を次に示します。 どちらの場合に、Active Directory では、rootDSE オブジェクトに接続し、操作の名前を変更する属性として指定する、rootDSE オブジェクトの null DN の変更操作を実行する必要があります。 RootDSE オブジェクトに対する変更可能な操作の詳細については、次を参照してください。 [rootDSE 変更操作](https://msdn.microsoft.com/library/cc223297.aspx)、MSDN web サイト。  

###### <a name="running-sdprop-manually-in-windows-server-2008-or-earlier"></a>Windows Server 2008 またはそれ以前に手動で実行中の SDProp

Ldp.exe を使用して、または LDAP の変更スクリプトを実行して実行する SDProp を強制することができます。 Ldp.exe を使用して SDProp を実行するには、ドメイン内の AdminSDHolder オブジェクトに変更を加えた後、次の手順を実行します。  

1. 起動**Ldp.exe**します。  
2. クリックして**接続**Ldp ダイアログ ボックスをクリックして**Connect**します。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_9.gif)  

3. **Connect**  ダイアログ ボックスで、PDC エミュレーター (PDCE) ロールを保持するドメインのドメイン コント ローラーの名前を入力し、をクリックして**OK**します。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_10.png)  

4. によって示される、正常に接続していることを確認します**Dn:。(RootDSE)** 次のスクリーン ショットでは、次のようにクリックします。**接続**クリック**バインド**。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_11.png)  

5. **バインド** ダイアログ ボックスに、rootDSE オブジェクトを変更するアクセス許可を持つユーザー アカウントの資格情報を入力します。 (そのユーザーとしてログオンしている場合は選択**としてバインド**現在ログオンしているユーザーです)。**[OK]** をクリックします。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_12.png)  

6. バインド操作を完了すると後でクリックして**参照**、 をクリック**変更**します。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_13.png)  

7. **変更**ままにしてください ダイアログ ボックス、 **DN**フィールドを空白。 **エントリ属性の編集**フィールドに「 **FixUpInheritance**、し、**値**フィールドに「**はい**します。 クリックして **」と入力**を設定する、**エントリ一覧**次のスクリーン ショットに示すようにします。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_14.gif)  

8. 設定の変更 ダイアログ ボックスでは、実行、 をクリックし、AdminSDHolder オブジェクトに加えた変更がそのオブジェクトに表示されていることを確認します。  

> [!NOTE]  
> 保護グループのメンバーシップを変更する特権のないアカウントの指定を許可する AdminSDHolder を変更する方法の詳細については、次を参照してください[付録 i:。アカウントおよび Active Directory でグループ管理アカウントを作成する保護される](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)します。  

LDIFDE またはスクリプトを使用して、SDProp を手動で実行する場合は、次に示すように変更エントリを作成できます。  

![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_15.gif)  

###### <a name="running-sdprop-manually-in-windows-server-2012-or-windows-server-2008-r2"></a>Windows Server 2012 または Windows Server 2008 R2 で SDProp を手動で実行します。

Ldp.exe を使用して、または LDAP の変更スクリプトを実行して実行する SDProp を強制することもできます。 Ldp.exe を使用して SDProp を実行するには、ドメイン内の AdminSDHolder オブジェクトに変更を加えた後、次の手順を実行します。  

1. 起動**Ldp.exe**します。  

2. **Ldp**ダイアログ ボックスで、をクリックして**接続**、 をクリック**Connect**します。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_16.gif)  

3. **Connect**  ダイアログ ボックスで、PDC エミュレーター (PDCE) ロールを保持するドメインのドメイン コント ローラーの名前を入力し、をクリックして**OK**します。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_17.gif)  

4. によって示される、正常に接続していることを確認します**Dn:。(RootDSE)** 次のスクリーン ショットでは、次のようにクリックします。**接続**クリック**バインド**。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_18.gif)  

5. **バインド** ダイアログ ボックスに、rootDSE オブジェクトを変更するアクセス許可を持つユーザー アカウントの資格情報を入力します。 (そのユーザーとしてログオンしている場合は選択**バインドは、現在ログオンしているユーザー**)。**[OK]** をクリックします。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_19.gif)  

6. バインド操作を完了すると後でクリックして**参照**、 をクリック**変更**します。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_20.gif)  

7. **変更**ままにしてください ダイアログ ボックス、 **DN**フィールドを空白。 **エントリ属性の編集**フィールドに「 **RunProtectAdminGroupsTask**、し、**値**フィールドに「 **1**します。 クリックして**Enter**次に示すように、エントリの一覧を設定します。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_21.gif)  

8. 設定された**変更**ダイアログ ボックスで、をクリックして**実行**、AdminSDHolder オブジェクトに加えた変更がそのオブジェクトに表示されていることを確認します。  

LDIFDE またはスクリプトを使用して、SDProp を手動で実行する場合は、次に示すように変更エントリを作成できます。  

![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_22.gif)  
