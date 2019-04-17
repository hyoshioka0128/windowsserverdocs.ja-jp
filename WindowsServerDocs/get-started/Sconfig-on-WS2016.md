---
title: Sconfig.cmd を使用して Windows Server の Server Core インストールを構成する
description: Sconfig.cmd の使用方法を説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 10/17/2017
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6cac074-c6fc-46dd-9664-fa0342c0a5e8
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: high
ms.openlocfilehash: 2473b4ffae79c29ec7505616c139c03b21a4427b
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2018
ms.locfileid: "1284351"
---
# <a name="configure-a-server-core-installation-of-windows-server-2016-or-windows-server-version-1709-with-sconfigcmd"></a>Sconfig.cmd を使用して Windows Server 2016 または Windows Server バージョン 1709 の Server Core インストールを構成する
> 適用対象: Windows Server (半期チャネル)、Windows Server 2016

Windows Server 2016 および Windows Server バージョン 1709 では、サーバー構成ツール (Sconfig.cmd) を使用して、Server Core インストールの一般的な設定のいくつかを構成および管理することができます。 このツールを使用するには、Administrators グループのメンバーである必要があります。  
  
Server Core のインストールやデスクトップ エクスペリエンス搭載サーバー (Windows Server 2016 のみ) のインストールで Sconfig.cmd を使用できます。 
  
## <a name="start-the-server-configuration-tool"></a>サーバー構成ツールを起動する  
  
1.  システム ドライブに移動します。  
  
2.  「`Sconfig.cmd`」と入力し、Enter キーを押します。 サーバー構成ツールのインターフェイスが開きます。  
  
 <img src="mainsconfigpage.png" style='float:left; padding:.5em;' alt="Screenshot of Sconfig.cmd user interface">  
Sconfig.cmd ユーザー インターフェイスのスクリーンショット  
  
##  <a name="BKMK_Domainworkgroup"></a> ドメイン/ワークグループの設定  
 サーバー構成ツールの既定の画面には、現在のドメイン/ワークグループの設定が表示されます。 メイン メニューから **[ドメイン/ワークグループ]** 設定ページにアクセスし、それ以降のページの指示に従って必要な情報を入力することで、ドメインやワークグループに参加できます。  
  
 ドメイン ユーザーがローカルの Administrator グループに追加されていないと、ドメイン ユーザーを使用して、システムの変更 (コンピューター名の変更など) を行うことはできません。 ドメイン ユーザーをローカルの Administrator グループに追加するには、コンピューターを再起動します。 次に、ローカルの管理者としてコンピューターにログオンし、後で説明する「[ローカル管理者の設定](assetId:///3c2f8ca4-6adc-4ebd-8daf-eb0de16c2c7d#BKMK_Localadministratorsettings)」セクションの手順に従います。  
  
> [!NOTE]
>  ドメインやワークグループのメンバーシップに変更を適用するには、サーバーを再起動する必要があります。 ただし、すべての変更が終了した後で、追加の変更を行い、サーバーを再起動することができます。これにより、サーバーを何度も再起動する必要がなくなります。 既定では、実行中の仮想マシンは、Hyper-V Server を再起動する前に自動的に保存されます。  
  
## <a name="computer-name-settings"></a>コンピューター名の設定  
 サーバー構成ツールの既定の画面には、現在のコンピューター名が表示されます。 メイン メニューから [コンピューター名] 設定ページにアクセスし、ページの指示に従うことで、コンピューター名を変更できます。  
  
> [!NOTE]
>  ドメインやワークグループのメンバーシップに変更を適用するには、サーバーを再起動する必要があります。 ただし、すべての変更が終了した後で、追加の変更を行い、サーバーを再起動することができます。これにより、サーバーを何度も再起動する必要がなくなります。 既定では、実行中の仮想マシンは、Hyper-V Server を再起動する前に自動的に保存されます。  
  
##  <a name="BKMK_Localadministratorsettings"></a> ローカル管理者の設定  
 ローカルの Administrators グループにユーザーを追加するには、メイン メニューの **[ローカル管理者の追加]** オプションを使用します。 ドメインに参加しているコンピューターで、ユーザーを "ドメイン\ユーザー名" の形式で入力します。 ドメインに参加していないコンピューター (ワークグループ コンピューター) で、ユーザー名のみを入力します。 変更はすぐに有効になります。  
  
## <a name="network-settings"></a>ネットワークの設定  
 DHCP サーバーによって自動的に割り当てられるように IP アドレスを構成することも、静的 IP アドレスを手動で割り当てることもできます。 このオプションでは、サーバーの DNS サーバー設定も構成できます。  
  
> [!NOTE]
>  これらのオプションおよび他の多数のオプションは現在、ネットワーキング Windows PowerShell コマンドレットで使用できます。 詳しくは、Windows Server ライブラリの「[Network Adapter Cmdlets](https://technet.microsoft.com/library/jj134956.aspx)」(ネットワーク アダプター コマンドレット) をご覧ください。  
  
## <a name="windows-update-settings"></a>Windows Update の設定  
 サーバー構成ツールの既定の画面には、現在の Windows Update の設定が表示されます。 メイン メニューの **[Windows Update の設定]** 構成オプションでは、自動更新または手動更新を使用するようにサーバーを構成できます。  
  
 **[自動更新]** を選ぶと、毎日午前 3 時に更新プログラムがシステムによってチェックされ、インストールが実行されます。 設定は直ちに有効になります。 **[手動]** を選ぶと、更新プログラムはシステムによって自動的にチェックされません。  
  
 メイン メニューの **[更新プログラムのダウンロードとインストール]** オプションでは、適用できる更新プログラムをいつでもダウンロードしてインストールできます。

 **[ダウンロードのみ]** オプションを使用すると、更新プログラムがスキャンされ、利用可能な更新プログラムがダウンロードされます。その後で、更新プログラムをインストールする準備ができたことがアクション センターで通知されます。 これは既定のオプションです。  
  
## <a name="remote-desktop-settings"></a>リモート デスクトップの設定  
 サーバー構成ツールの既定の画面には、リモート デスクトップ設定の現在の状態が表示されます。 **[リモート デスクトップ]** メイン メニュー オプションにアクセスして画面の指示に従うと、次のリモート デスクトップの設定を構成できます。  
  
-   ネットワーク レベル認証でリモート デスクトップを実行しているクライアントに対してリモート デスクトップを有効にする  
  
-   任意のバージョンのリモート デスクトップを実行しているクライアントに対してリモート デスクトップを有効にする  
  
-   リモートを無効にする  
  
## <a name="date-and-time-settings"></a>日付と時刻の設定  
 **[日付と時刻]** メイン メニュー オプションを利用することで、日付と時刻の設定にアクセスし変更することができます。 

## <a name="telemetry-settings"></a>利用統計情報の設定
このオプションを使用して、Microsoft に送信されるデータを構成できます。

## <a name="windows-activation-settings"></a>Windows のライセンス認証の設定
このオプションを使用して、Windows のライセンス認証を構成できます。
  
## <a name="to-enable-remote-management"></a>リモート管理を有効にするには  
**[リモート管理の構成]** メイン メニュー オプションを利用することで、次のようなさまざまなリモート管理のシナリオを有効にできます。  
  
-   Microsoft 管理コンソールのリモート管理  
-   Windows PowerShell  
-   サーバー マネージャー  
  
## <a name="to-log-off-restart-or-shut-down-the-server"></a>サーバーからのログオフ、およびサーバーの再起動やシャットダウンを行うには  
 サーバーからのログオフ、およびサーバーの再起動やシャットダウンを行うには、メイン メニューから対応するメニュー項目にアクセスします。 これらのオプションは、Windows セキュリティのメニューからも使用できます。Windows セキュリティのメニューには、Ctrl + Alt + Del キーを押すことでアプリケーションからいつでもアクセスできます。  
  
## <a name="to-exit-to-the-command-line"></a>終了してコマンド ラインに戻るには  
 終了してコマンド ラインに戻るには、**[終了してコマンド ラインに戻る]** オプションを選んで Enter キーを押します。 サーバー構成ツールに戻るには、「**Sconfig.cmd**」と入力して Enter キーを押します。