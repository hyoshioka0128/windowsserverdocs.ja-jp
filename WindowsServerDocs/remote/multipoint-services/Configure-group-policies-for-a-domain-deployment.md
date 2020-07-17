---
title: ドメイン展開用のグループ ポリシーを構成する
description: MultiPoint Services でグループポリシーを設定する方法について説明します。
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 13e5fa90-d330-4155-a6b8-78eb650cbbfa
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: e851d12dad29de8b3498aad220354d31917fadee
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862185"
---
# <a name="configure-group-policies-for-a-domain-deployment"></a>ドメイン展開用のグループ ポリシーを構成する
MultiPoint Services のドメインの展開が正常に機能するようにするには、MultiPoint Services システムの WMSshell ユーザーアカウントに次のグループポリシー設定を適用します。  
  
> [!IMPORTANT]  
> 一部のグループポリシー設定では、必要な構成設定が MultiPoint Services に適用されないようにすることができます。 MultiPoint Services で正しく動作するように、グループポリシー設定を理解して定義してください。 たとえば、自動ログオンを禁止するグループポリシー設定では、MultiPoint Services のログオン動作で問題が発生する可能性があります。  
  
## <a name="update-group-policies-for-the-wmsshell-user-account"></a>WMSshell ユーザーアカウントのグループポリシーを更新する 
WMSshell ユーザーアカウントは、MultiPoint services がコンソールにサインインするために使用するシステムアカウントです。このアカウントでは、実際のステーションが作成されます。 このアカウントは、MultiPoint マネージャーによって管理されるものではありません。
  
> [!NOTE]  
> グループポリシーを更新する方法については、「[ローカルグループポリシーエディター](https://technet.microsoft.com/library/dn265982.aspx)」を参照してください。  
  
**ポリシー:** コントロールパネルのユーザー構成 > 管理用テンプレート >**個人用設定**>  
  
次の値を割り当てます。  
  
|設定|値|  
|-----------|----------|  
|スクリーン セーバーを有効にする|無効|  
|スクリーン セーバーのタイムアウト|無効<p>秒: xxx|  
|スクリーン セーバーをパスワードで保護する|無効|  
  
**ポリシー:** コンピューターの構成 > Windows の設定 > セキュリティ設定 > ローカルポリシー > ユーザー権利**の割り当て > ローカルログオンを許可する**  
  
|設定|値|  
|-----------|----------|  
|ローカル ログオンを許可する|アカウントの一覧に WMSshell アカウントが含まれていることを確認します。<p>**注:** 既定では、WMSshell アカウントは Users グループのメンバーです。 ユーザーグループが一覧にあり、WMSshell が Users グループのメンバーである場合は、WMSshell アカウントを一覧に追加する必要はありません。|  
  
> [!IMPORTANT]  
> グループポリシーを設定する場合は、ポリシーによって自動更新が妨げられないようにし、MultiPoint サーバーで Windows エラー報告のエラーを報告するようにしてください。 これらの設定は、Windows MultiPoint Server のインストール中に選択された **[更新プログラムを自動的にインストール]** する と **[自動 Windows エラー報告]** 設定 で設定します。 **[サーバー設定の編集]** を使用して multipoint マネージャーで構成するか、ディスク保護のスケジュールされた更新プログラムで構成します。  
  
## <a name="update-the-registry"></a>レジストリを更新する  
MultiPoint Services をドメインに展開する場合は、次のレジストリサブキーを更新する必要があります。  
  
> [!IMPORTANT]  
> レジストリの編集を誤ると、システムに重大な損害を与える可能性があります。 レジストリを変更する前に、コンピューター上の重要なデータのバックアップを作成する必要があります。  
  
#### <a name="to-update-registry-subkeys-for-a-domain-deployment-of-multipoint-services"></a>MultiPoint Services のドメイン展開のレジストリサブキーを更新するには  
  
1.  レジストリエディターを開きます。 (コマンドプロンプトで、「 **regedit.exe**」と入力し、enter キーを押します)。  
  
2.  左側のウィンドウで、次のレジストリサブキーを見つけて選択します。  
  
    HKEY_USERS\<SIDofWMSshell > \Software\Policies\Microsoft\Windows\Control Panel\Desktop  
  
    ここで、'<SIDofWMSshell>' は WMSshell アカウントのセキュリティ識別子 (SID) です。 SID の識別方法については、「[ユーザー名をセキュリティ識別子 (sid) に関連付ける方法](https://support.microsoft.com/kb/154599)」を参照してください。  
  
3.  右側の一覧で、次のサブキーを更新します。  
  
    |サブキー|値の名前|[値] に|  
    |----------|--------------|--------------|  
    |ScreenSaveActive|REG_SZ|0 (ゼロ)|  
    |ScreenSaveTimeout|REG_SZ|120|  
    |ScreenSaverIsSecure|REG_SZ|0 (ゼロ)|  
  
    レジストリサブキーを更新するには:  
  
    1.  左側のウィンドウでレジストリキーを選択し、右ペインでサブキーを右クリックして、 **[変更]** をクリックします。  
  
    2.  文字列の編集 ダイアログボックスで、値の**データ** に新しい値を入力し、**OK** をクリックします。  
  
4.  レジストリサブキーの更新が完了したら、コンピューターを再起動して変更を有効にします。 
