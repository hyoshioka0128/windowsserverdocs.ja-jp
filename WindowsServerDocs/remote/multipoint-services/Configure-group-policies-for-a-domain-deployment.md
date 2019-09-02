---
title: ドメイン展開用のグループ ポリシーを構成する
description: MultiPoint Services でグループポリシーを設定する方法について説明します。
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13e5fa90-d330-4155-a6b8-78eb650cbbfa
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 5c9d8efc1ed4a2f498ffce6c69d443ae819dced9
ms.sourcegitcommit: 1bc3c229e9688ac741838005ec4b88e8f9533e8a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68314320"
---
# <a name="configure-group-policies-for-a-domain-deployment"></a>ドメイン展開用のグループ ポリシーを構成する
MultiPoint Services のドメインの展開が正常に機能するようにするには、MultiPoint Services システムの WMSshell ユーザーアカウントに次のグループポリシー設定を適用します。  
  
> [!IMPORTANT]  
> 一部のグループポリシー設定では、必要な構成設定が MultiPoint Services に適用されないようにすることができます。 MultiPoint Services で正しく動作するように、グループポリシー設定を理解して定義してください。 たとえば、自動ログオンを禁止するグループポリシー設定では、MultiPoint Services のログオン動作で問題が発生する可能性があります。  
  
## <a name="update-group-policies-for-the-wmsshell-user-account"></a>WMSshell ユーザーアカウントのグループポリシーを更新する 
WMSshell ユーザーアカウントは、MultiPoint services がコンソールにサインインするために使用するシステムアカウントです。このアカウントでは、実際のステーションが作成されます。 このアカウントは、MultiPoint マネージャーによって管理されるものではありません。
  
> [!NOTE]  
> グループポリシーを更新する方法については、「[ローカルグループポリシーエディター](https://technet.microsoft.com/library/dn265982.aspx)」を参照してください。  
  
**ポリシー**コントロールパネルのユーザー構成 > 管理用テンプレート >**個人用設定**>  
  
次の値を割り当てます。  
  
|設定|値|  
|-----------|----------|  
|スクリーン セーバーを有効にする|Disabled|  
|スクリーン セーバーのタイムアウト|Disabled<br /><br />秒: xxx|  
|スクリーン セーバーをパスワードで保護する|Disabled|  
  
**ポリシー**コンピューターの構成 > Windows の設定 > セキュリティ設定 > ローカルポリシー > ユーザー権利**の割り当て > ローカルログオンを許可する**  
  
|設定|値|  
|-----------|----------|  
|ローカル ログオンを許可|アカウントの一覧に WMSshell アカウントが含まれていることを確認します。<br /><br />**注:** 既定では、WMSshell アカウントは Users グループのメンバーです。 ユーザーグループが一覧にあり、WMSshell が Users グループのメンバーである場合は、WMSshell アカウントを一覧に追加する必要はありません。|  
  
> [!IMPORTANT]  
> グループポリシーを設定する場合は、ポリシーによって自動更新が妨げられないようにし、MultiPoint サーバーで Windows エラー報告のエラーを報告するようにしてください。 これらは、Windows MultiPoint Server のインストール時に選択された [**更新プログラムを自動的にインストール**する] と [**自動 Windows エラー報告**設定] で設定されます。 [**サーバー設定の編集**] を使用して multipoint Manager で構成されます。ディスク保護のスケジュールされた更新プログラムで構成されます。  
  
## <a name="update-the-registry"></a>レジストリを更新する  
MultiPoint Services をドメインに展開する場合は、次のレジストリサブキーを更新する必要があります。  
  
> [!IMPORTANT]  
> レジストリを間違って編集すると、システムが壊れる可能性があります。 レジストリを変更する前に、コンピューターにある重要なデータをバックアップしてください。  
  
#### <a name="to-update-registry-subkeys-for-a-domain-deployment-of-multipoint-services"></a>MultiPoint Services のドメイン展開のレジストリサブキーを更新するには  
  
1.  レジストリエディターを開きます。 (コマンドプロンプトで、「 **regedit.exe**」と入力し、enter キーを押します)。  
  
2.  左側のウィンドウで、次のレジストリサブキーを見つけて選択します。  
  
    HKEY_USERS\<SIDofWMSshell > \Software\Policies\Microsoft\Windows\Control Panel\Desktop  
  
    ここで<SIDofWMSshell>、' ' は WMSshell アカウントのセキュリティ識別子 (SID) です。 SID の識別方法については、「[ユーザー名をセキュリティ識別子 (sid) に関連付ける方法](https://support.microsoft.com/kb/154599)」を参照してください。  
  
3.  右側の一覧で、次のサブキーを更新します。  
  
    |サブキー|値の名前|[値] に|  
    |----------|--------------|--------------|  
    |ScreenSaveActive|REG_SZ|0 (ゼロ)|  
    |ScreenSaveTimeout|REG_SZ|120|  
    |ScreenSaverIsSecure|REG_SZ|0 (ゼロ)|  
  
    レジストリサブキーを更新するには:  
  
    1.  左側のウィンドウでレジストリキーを選択し、右ペインでサブキーを右クリックして、[**変更**] をクリックします。  
  
    2.  [文字列の編集] ダイアログボックスで、[値の**データ**] に新しい値を入力し、[ **OK**] をクリックします。  
  
4.  レジストリサブキーの更新が完了したら、コンピューターを再起動して変更を有効にします。 
