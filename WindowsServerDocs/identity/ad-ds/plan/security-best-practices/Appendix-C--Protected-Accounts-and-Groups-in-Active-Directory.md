---
ms.assetid: 5b2876ac-fe7d-4054-bfba-b692e57bc0d2
title: 付録 C-Active Directory の保護されたアカウントとグループ
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: cfee6eedd1582c3df960cca1c32fce27c74f82cb
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86963234"
---
# <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>付録 C: Active Directory の保護されたアカウントとグループ

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

## <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>付録 C: Active Directory の保護されたアカウントとグループ

Active Directory 内では、高い特権を持つアカウントとグループの既定のセットは、保護されたアカウントとグループと見なされます。 Active Directory のほとんどのオブジェクトでは、代理管理者 (Active Directory オブジェクトを管理するためのアクセス許可を委任されたユーザー) は、グループのメンバーシップを変更するためのアクセス許可を変更するなど、オブジェクトのアクセス許可を変更できます。  

ただし、保護されたアカウントとグループを使用すると、オブジェクトの権限は、オブジェクトがディレクトリに移動された場合でも、オブジェクトに対するアクセス許可が一貫していることを保証する自動プロセスによって設定および適用されます。 他のユーザーが保護されたオブジェクトのアクセス許可を手動で変更した場合でも、このプロセスによって、アクセス許可が既定値に迅速に返されます。  

### <a name="protected-groups"></a>保護されたグループ

次の表に、ドメインコントローラーのオペレーティングシステムによって一覧表示される Active Directory の保護されたグループを示します。  

#### <a name="protected-accounts-and-groups-in-active-directory-by-operating-system"></a>オペレーティングシステムによって Active Directory の保護されたアカウントとグループ

| Windows Server 2003 RTM | Windows Server 2003 SP1 + | Windows Server 2012、 <br> Windows Server 2008 R2、 <br> Windows Server 2008 | Windows Server 2016 |
| --- | --- | --- | --- |
|Account Operators|Account Operators|Account Operators|Account Operators|
|管理者|管理者|管理者|管理者|
|管理者|管理者|管理者|管理者|
|Backup Operators|Backup Operators|Backup Operators|Backup Operators|
|Cert Publishers|||
|Domain Admins|Domain Admins|Domain Admins|Domain Admins|
|ドメイン コントローラー|ドメイン コントローラー|ドメイン コントローラー|ドメイン コントローラー|
|Enterprise Admins|Enterprise Admins|Enterprise Admins|Enterprise Admins|
|Krbtgt|Krbtgt|Krbtgt|Krbtgt|
|演算子を印刷します。|演算子を印刷します。|演算子を印刷します。|演算子を印刷します。|
|||Read-Only Domain Controllers|Read-Only Domain Controllers|
|レプリケーター|レプリケーター|レプリケーター|レプリケーター|
|Schema Admins|Schema Admins|Schema Admins|Schema Admins|
|Server Operators|Server Operators|Server Operators|Server Operators|

#### <a name="adminsdholder"></a>AdminSDHolder

AdminSDHolder オブジェクトの目的は、ドメイン内の保護されたアカウントとグループに "テンプレート" アクセス許可を提供することです。 AdminSDHolder は、すべての Active Directory ドメインのシステムコンテナーにオブジェクトとして自動的に作成されます。 そのパスは次のとおりです: **cn = AdminSDHolder、cn = System、dc =<domain_component>、dc =<domain_component>?。**  

Administrators グループによって所有されている Active Directory ドメイン内のほとんどのオブジェクトとは異なり、AdminSDHolder は Domain Admins グループによって所有されています。 既定では、EAs はドメインのドメイン管理者および管理者グループと同様に、任意のドメインの AdminSDHolder オブジェクトに変更を加えることができます。 また、AdminSDHolder の既定の所有者はドメインの Domain Admins グループですが、Administrators または Enterprise Admins のメンバーは、オブジェクトの所有権を取得できます。  

#### <a name="sdprop"></a>SDProp

SDProp は、ドメインの PDC エミュレーター (PDCE) を保持しているドメインコントローラー上で60分ごと (既定では) 実行されるプロセスです。 SDProp は、ドメインの AdminSDHolder オブジェクトのアクセス許可と、ドメイン内の保護されたアカウントおよびグループのアクセス許可を比較します。 保護されているアカウントとグループのアクセス許可が、AdminSDHolder オブジェクトのアクセス許可と一致しない場合、保護されたアカウントとグループのアクセス許可は、ドメインの AdminSDHolder オブジェクトのアクセス許可と一致するようにリセットされます。  

また、保護されたグループとアカウントでは、権限の継承が無効になっています。つまり、アカウントとグループがディレクトリ内の別の場所に移動された場合でも、新しい親オブジェクトから権限を継承しません。 親オブジェクトに対するアクセス許可の変更によって、AdminSDHolder のアクセス許可が変更されないように、AdminSDHolder オブジェクトで継承が無効になっています。  

##### <a name="changing-sdprop-interval"></a>SDProp 間隔の変更

通常は、SDProp を実行する間隔を変更する必要はありません。ただし、テスト目的では使用しません。 SDProp 間隔を変更する必要がある場合は、ドメインの PDCE で regedit を使用して、Hklm\system\currentcontrolset\services\ntds\parameters の AdminSDProtectFrequency DWORD 値を追加または変更します。  

値の範囲は、60 ~ 7200 (1 分 ~ 2 時間) です。 変更を元に戻すには、AdminSDProtectFrequency キーを削除します。これにより、SDProp は60分の間隔に戻ります。 通常、運用環境のドメインでは、ドメインコントローラーの LSASS 処理のオーバーヘッドが増えるため、この間隔を短くすることは避けてください。 この増加による影響は、ドメイン内の保護されたオブジェクトの数によって異なります。  

##### <a name="running-sdprop-manually"></a>SDProp を手動で実行する

AdminSDHolder の変更をテストするには、手動で SDProp を実行します。これにより、タスクは直ちに実行されますが、スケジュールされた実行には影響しません。 Windows server 2008 以前を実行しているドメインコントローラーと windows server 2012 または Windows Server 2008 R2 を実行しているドメインコントローラーでは、SDProp を手動で実行する方法が少し異なります。  

以前のオペレーティングシステムで SDProp を手動で実行する手順については[Microsoft サポートの記事 251343](https://support.microsoft.com/kb/251343)で説明しています。また、古いオペレーティングシステムと新しいオペレーティングシステムの詳細な手順については、以下を参照してください。 どちらの場合も、Active Directory で rootDSE オブジェクトに接続し、rootDSE オブジェクトに対して null の DN を指定して変更操作を実行し、変更する属性として操作の名前を指定する必要があります。 RootDSE オブジェクトでの変更可能な操作の詳細については、MSDN web サイトの「 [rootdse の変更操作](/openspecs/windows_protocols/ms-adts/fc74972f-b267-4c1a-8716-0f5b48cf52b9)」を参照してください。  

###### <a name="running-sdprop-manually-in-windows-server-2008-or-earlier"></a>Windows Server 2008 以前での SDProp の手動実行

Ldp.exe を使用するか、LDAP 変更スクリプトを実行して、強制的に SDProp を実行することができます。 Ldp.exe を使用して SDProp を実行するには、ドメイン内の AdminSDHolder オブジェクトに変更を加えた後で、次の手順を実行します。  

1. **Ldp.exe**を起動します。  
2. [Ldp] ダイアログボックスの [**接続**] をクリックし、[**接続**] をクリックします。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_9.gif)  

3. [**接続**] ダイアログボックスで、PDC エミュレーター (pdce) の役割を持つドメインのドメインコントローラーの名前を入力し、[ **OK]** をクリックします。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_10.png)  

4. 次のスクリーンショットの**Dn: (RootDSE)** で示されているように、正常に接続したことを確認します。 [**接続**] をクリックし、[**バインド**] をクリックします。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_11.png)  

5. [**バインド**] ダイアログボックスで、rootDSE オブジェクトを変更するアクセス許可を持つユーザーアカウントの資格情報を入力します。 (そのユーザーとしてログオンしている場合は、[現在のログオンユーザー**としてバインド**する] を選択できます)。[ **OK]** をクリックします。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_12.png)  

6. バインド操作が完了したら、[**参照**] をクリックし、[**変更**] をクリックします。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_13.png)  

7. [**変更**] ダイアログボックスで、 **DN**フィールドを空白のままにします。 [**エントリ属性の編集**] フィールドに「 **fixupinheritance**」と入力し、[**値**] フィールドに「 **Yes」** と入力します。 **Enter キーを押し**て、次のスクリーンショットに示すように入力**リスト**を設定します。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_14.gif)  

8. [設定された変更] ダイアログボックスで、[実行] をクリックし、AdminSDHolder オブジェクトに対して行った変更がそのオブジェクトに表示されていることを確認します。  

> [!NOTE]  
> 指定した特権のないアカウントが保護されたグループのメンバーシップを変更することを許可するように AdminSDHolder を変更する方法については、「[付録 I: Active Directory で保護されたアカウントとグループの管理アカウントを作成](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)する」をご覧ください。  

LDIFDE またはスクリプトを使用して手動で SDProp を実行する場合は、次に示すように、変更エントリを作成できます。  

![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_15.gif)  

###### <a name="running-sdprop-manually-in-windows-server-2012-or-windows-server-2008-r2"></a>Windows Server 2012 または Windows Server 2008 R2 で手動で SDProp を実行する

Ldp.exe を使用するか、LDAP 変更スクリプトを実行して、強制的に SDProp を実行することもできます。 Ldp.exe を使用して SDProp を実行するには、ドメイン内の AdminSDHolder オブジェクトに変更を加えた後で、次の手順を実行します。  

1. **Ldp.exe**を起動します。  

2. [ **Ldp** ] ダイアログボックスで、[**接続**] をクリックし、[**接続**] をクリックします。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_16.gif)  

3. [**接続**] ダイアログボックスで、PDC エミュレーター (pdce) の役割を持つドメインのドメインコントローラーの名前を入力し、[ **OK]** をクリックします。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_17.gif)  

4. 次のスクリーンショットの**Dn: (RootDSE)** で示されているように、正常に接続したことを確認します。 [**接続**] をクリックし、[**バインド**] をクリックします。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_18.gif)  

5. [**バインド**] ダイアログボックスで、rootDSE オブジェクトを変更するアクセス許可を持つユーザーアカウントの資格情報を入力します。 (そのユーザーとしてログオンしている場合は、[**現在のログオンユーザーとしてバインド**する] を選択できます)。[ **OK]** をクリックします。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_19.gif)  

6. バインド操作が完了したら、[**参照**] をクリックし、[**変更**] をクリックします。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_20.gif)  

7. [**変更**] ダイアログボックスで、 **DN**フィールドを空白のままにします。 [**エントリ属性の編集**] フィールドに「 **RunProtectAdminGroupsTask**」と入力し、[**値**] フィールドに「 **1**」と入力します。 **Enter キーを押し**て、次に示すように入力リストを設定します。  

   ![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_21.gif)  

8. [設定された**変更**] ダイアログボックスで、[**実行**] をクリックし、AdminSDHolder オブジェクトに対して行った変更がそのオブジェクトに表示されていることを確認します。  

LDIFDE またはスクリプトを使用して手動で SDProp を実行する場合は、次に示すように、変更エントリを作成できます。  

![保護されたアカウントとグループ](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_22.gif)  
