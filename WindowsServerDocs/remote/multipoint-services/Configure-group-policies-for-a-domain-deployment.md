---
title: ドメイン展開用のグループ ポリシーを構成する
description: MultiPoint Services のグループ ポリシーを設定する方法について説明します
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
ms.openlocfilehash: f661fbdc40fd7dd2562d51756bc7642c8e9a4a82
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888043"
---
# <a name="configure-group-policies-for-a-domain-deployment"></a>ドメイン展開用のグループ ポリシーを構成する
MultiPoint Services のドメイン配置が正常に動作するためには、MultiPoint Services システムで WMSshell ユーザー アカウントに、次のグループ ポリシー設定を適用します。  
  
> [!IMPORTANT]  
> 一部のグループ ポリシー設定は、MultiPoint Services に適用されてから、必要な構成設定を回避できます。 必ず、理解し、MultiPoint Services で正しく動作するために、グループ ポリシー設定を定義します。 たとえば、自動ログオンを妨げるグループ ポリシー設定には、MultiPoint Services のログオンの動作に関する問題を表示できます。  
  
## <a name="update-group-policies-for-the-wmsshell-user-account"></a>WMSshell ユーザー アカウントのグループ ポリシーを更新します。 
WMSshell ユーザー アカウントとは、割合のステーションを作成する場所をコンソールにサインインする MultiPoint サービスを使用して、システム アカウントです。 このアカウントでない明 MultiPoint マネージャーで管理します。
  
> [!NOTE]  
> グループ ポリシーを更新する方法についてを参照してください。[ローカル グループ ポリシー エディター](https://technet.microsoft.com/library/dn265982.aspx)します。  
  
**ポリシー:** ユーザーの構成 > 管理用テンプレート > コントロール パネル >**パーソナル化**  
  
次の値を割り当てます。  
  
|設定|値|  
|-----------|----------|  
|スクリーン セーバーを有効にする|Disabled|  
|スクリーン セーバーのタイムアウト|Disabled<br /><br />秒: xxx|  
|スクリーン セーバーをパスワードで保護する|Disabled|  
  
**ポリシー:** コンピューターの構成 > Windows の設定 > セキュリティ設定 > ローカル ポリシー > ユーザー権利の割り当て >**ローカル ログオンを許可します。**  
  
|設定|値|  
|-----------|----------|  
|ローカル ログオンを許可|アカウントの一覧に WMSshell アカウントが含まれていることを確認します。<br /><br />**注:** 既定では、WMSshell アカウントは、ユーザー グループのメンバーが。 ユーザー グループは、一覧に WMSshell Users グループのメンバーである場合は、WMSshell アカウントを一覧に追加する必要はありません。|  
  
> [!IMPORTANT]  
> グループ ポリシーを設定すると、ポリシーが自動更新とエラー Windows MultiPoint server のレポートが妨げられないようにを確認します。 によって設定される、**更新プログラムを自動的にインストール**と**自動 Windows エラー報告**MultiPoint で構成されている Windows MultiPoint Server のインストール時に選択された設定使用してマネージャー**サーバー設定の編集**、ディスク保護のスケジュールされた更新プログラムで構成されているか。  
  
## <a name="update-the-registry"></a>レジストリを更新します。  
MultiPoint Services のドメインの展開の次のレジストリ サブキーを更新する必要があります。  
  
> [!IMPORTANT]  
> レジストリを正しく編集しないと、システムが正常に動作しなくなる場合があります。 レジストリを変更する前に、コンピューター上の重要なデータのバックアップを作成する必要があります。  
  
#### <a name="to-update-registry-subkeys-for-a-domain-deployment-of-multipoint-services"></a>MultiPoint Services のドメイン展開用のレジストリ サブキーを更新するには  
  
1.  レジストリ エディターを開きます。 (コマンド プロンプトで「 **regedit.exe**、ENTER キーを押します)。  
  
2.  左側のウィンドウで検索し、次のレジストリ サブキーを選択します。  
  
    HKEY_USERS\<SIDofWMSshell > \Software\Policies\Microsoft\Windows\Control Panel\Desktop  
  
    場所 '<SIDofWMSshell>' WMSshell アカウントのセキュリティ識別子 (SID)。 SID を特定する方法についてを参照してください。[にセキュリティ識別子 (SID) と、ユーザー名を関連付ける方法](https://support.microsoft.com/kb/154599)します。  
  
3.  右側のボックスの一覧で、次のサブキーを更新します。  
  
    |サブキー|値の名前|[値] に|  
    |----------|--------------|--------------|  
    |ScreenSaveActive|REG_SZ|0 (ゼロ)|  
    |ScreenSaveTimeout|REG_SZ|120|  
    |ScreenSaverIsSecure|REG_SZ|0 (ゼロ)|  
  
    レジストリ サブキーを更新します。  
  
    1.  左側のペインで選択したレジストリ キーを持つ、右側のウィンドウで、サブキーを右クリックし、**変更**します。  
  
    2.  文字列の編集 ダイアログ ボックスに新しい値を入力します。**値のデータ**、順にクリックします**OK**します。  
  
4.  レジストリ サブキーの更新が完了したら、変更をアクティブ化するコンピューターを再起動します。 