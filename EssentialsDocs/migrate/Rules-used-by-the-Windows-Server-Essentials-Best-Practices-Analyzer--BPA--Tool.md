---
title: "Windows Server Essentials ベスト プラクティス アナライザー (BPA) ツールで使用される規則"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 37e1dae7-586c-4dd7-bf83-7e14a9567c8f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c205bc8ff75bf64d4a13a7d799988c9d1ebe1a22
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="rules-used-by-the-windows-server-essentials-best-practices-analyzer-bpa-tool"></a>Windows Server Essentials ベスト プラクティス アナライザー (BPA) ツールで使用される規則

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

この記事では、によって、Windows Server Essentials ベスト プラクティス アナライザー (BPA) を使用するルールについて説明します。 BPA サーバーを調べて、Windows Server Essentials を実行しているし、問題について説明し、それらを解決するための推奨事項を提供するレポートを表示します。 推奨事項は、Windows Server Essentials の製品サポート組織によって作成されます。  
  
## <a name="using-the-tool"></a>ツールの使用  
 設定とデータの移行が完了したら、移行先サーバーで、BPA を実行するには、Windows Server 2011 Essentials、Windows Small Business Server 2011 Essentials、または Windows Home Server 2011 から Windows Server Essentials に移行する場合は、標準的な手法を勧めします。 いつでも、ダッシュ ボードから、ツールを実行できます。  
  
#### <a name="to-run-the--windows-server-essentials-bpa-on-the-server"></a>サーバーで、Windows Server Essentials BPA を実行するには  
  
1.  管理者は、サーバーにログオンし、ダッシュ ボードを開きます。  
  
2.  ダッシュ ボードで、をクリックして、**デバイス**] タブ。  
  
3.  **サーバー タスク**] ウィンドウで、をクリックして**ベスト プラクティス アナライザー**します。  
  
4.  BPA の各メッセージを確認し、問題を解決するために必要な場合、指示に従います。  
  
## <a name="rules-used-by-the-best-practices-analyzer"></a>ベスト プラクティス アナライザーによって使用される規則  
  
### <a name="disable-ip-filtering"></a>IP フィルタ リングを無効にします。  
 **問題:** IP フィルタ リングは現在サーバーを有効にします。 IP フィルタ リングを無効にする必要があります。  
  
 **影響:** IP フィルタ リングが有効になっている場合、ネットワーク トラフィックをブロックする可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-disable-ip-filtering"></a>IP フィルタ リングを無効にするには  
  
1.  サーバーで regedit.exe を開きます。  
  
2.  Hkey_local_machine \system\currentcontrolset\services\tcpip\parameters に移動します。  
  
3.  右クリック**EnableSecurityFilters**、] をクリックし、**変更**します。  
  
4.  **編集 DWORD (32 ビット) 値**] ウィンドウで、変更、**値のデータ**フィールドを 0 にして、をクリックして**OK**します。  
  
5.  変更を適用するには、サーバーを再起動します。  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-set-to-start-automatically-by-default"></a>分散トランザクション コーディネータ (MSDTC) サービスを設定すると、既定で自動的に開始する必要があります。  
 **問題:**自動的に開始する MSDTC サービスが構成されていません。  
  
 **影響:** MSDTC サービスが自動的に開始しないサーバーが起動します。 サービスが停止すると、一部の SQL Server または COM 関数が失敗する可能性があります。 その結果、Microsoft SQL Server または COM 関数を使用するアプリケーションが正しく機能しない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-msdtc-service-to-start-automatically"></a>自動的に開始する MSDTC サービスを構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**分散トランザクション コーディネータ**をクリックし、**プロパティ**します。  
  
3.  **全般**] タブで、変更、**スタートアップの種類**に**自動 (遅延開始)**、] をクリックし、**[OK]**します。  
  
### <a name="the-netlogon-service-should-be-configured-to-start-automatically-by-default"></a>Netlogon サービスは、既定で自動的に開始するように構成する必要があります。  
 **問題:**自動的に開始する、Netlogon サービスが構成されていません。  
  
 **影響:** Netlogon サービスが自動的に起動しない、サーバーが開始されるときです。 サービスが停止している場合、ユーザーおよびサービス、サーバーによって認証されない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-netlogon-service-to-start-automatically"></a>Netlogon サービスが自動的に開始を構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**Netlogon**をクリックし、**プロパティ**します。  
  
3.  **全般**] タブで、変更、**スタートアップの種類**に**自動**、] をクリックし、**[OK]**します。  
  
### <a name="the-dns-client-service-should-be-configured-to-start-automatically-by-default"></a>DNS クライアント サービスは、既定で自動的に開始するように構成する必要があります。  
 **問題:**自動的に開始する DNS クライアント サービスが構成されていません。  
  
 **影響:** DNS クライアント サービスが自動的に開始しないサーバーが起動します。 このサービスが停止している場合、サーバーできないことがあります DNS 名を解決します。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-dns-client-service-to-start-automatically"></a>自動的に開始する DNS クライアント サービスを構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**DNS クライアント**をクリックし、**プロパティ**します。  
  
3.  **全般**] タブで、変更、**スタートアップの種類**に**自動**、] をクリックし、**[OK]**します。  
  
### <a name="the-dns-server-service-should-be-configured-to-start-automatically-by-default"></a>DNS サーバー サービスは、既定で自動的に開始するように構成する必要があります。  
 **問題:**自動的に開始する DNS サーバー サービスが構成されていません。  
  
 **影響:**、DNS サーバー サービスが自動的に起動しない、サーバーが開始されるときです。 このサービスが停止している場合、DNS の更新は発生しません。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-dns-server-service-to-start-automatically"></a>自動的に開始する DNS サーバー サービスを構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**DNS サーバー**をクリックし、**プロパティ**します。  
  
3.  **全般**] タブで、変更、**スタートアップの種類**に**自動**、] をクリックし、**[OK]**します。  
  
### <a name="active-directory-web-services-is-not-set-to-the-default-start-mode"></a>Active Directory Web サービスは、既定の開始モードに設定されていません。  
 **問題:** Active Directory Web サービスが自動の既定の開始モードに設定されていません。  
  
 **影響:** Active Directory Web サービス (ADWS) が自動の既定の開始モードに設定されていません。 サーバー上の ADWS が停止しているか、無効な場合は、Windows PowerShell 用 Active Directory モジュールのなどのクライアント アプリケーション、または Active Directory 管理センターのアクセスまたはこのサーバーで実行されているディレクトリ サービスのインスタンスを管理することはできません。 For more information, see [What's New in AD DS: Active Directory Web Services](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) in the Windows Server Technical Library.  
  
 **解決方法:**  
  
##### <a name="to-configure-the-active-directory-web-services-service-to-start-automatically"></a>自動的に開始する Active Directory Web Services サービスを構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**Active Directory Web Services**をクリックし、**プロパティ**します。  
  
3.  **全般**] タブで、変更、**スタートアップの種類**に**自動**、] をクリックし、**[OK]**します。  
  
### <a name="the-dhcp-client-service-should-be-configured-to-start-automatically-by-default"></a>DHCP クライアント サービスは、既定で自動的に開始するように構成する必要があります。  
 **問題:**自動的に開始する DHCP クライアント サービスが構成されていません。  
  
 **影響:** DHCP クライアント サービスは自動的に起動しないときにサーバーを起動します。 このサービスが停止している場合、クライアント コンピューターは、サーバーから IP アドレスを受信することはできません。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-dhcp-client-service-to-start-automatically"></a>自動的に開始する DHCP クライアント サービスを構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**DHCP クライアント**をクリックし、**プロパティ**します。  
  
3.  **全般**] タブで、変更、**スタートアップの種類**に**自動**、] をクリックし、**[OK]**します。  
  
### <a name="the-iis-admin-service-should-be-configured-to-start-automatically-by-default"></a>IIS 管理サービスは、既定で自動的に開始するように構成する必要があります。  
 **問題:**自動的に開始する IIS 管理サービスが構成されていません。  
  
 **影響:** IIS 管理サービスが自動的に起動しないときにサーバーを起動します。 このサービスが停止している場合リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性がありますできません。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-iis-admin-service-to-start-automatically"></a>自動的に開始する IIS 管理サービスを構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリック**IIS 管理サービス**、] をクリックし、**プロパティ**します。  
  
3.  **全般**] タブで、変更、**スタートアップの種類**に**自動**、] をクリックし、**[OK]**します。  
  
### <a name="the-world-wide-web-publishing-service-should-be-configured-to-start-automatically-by-default"></a>World Wide Web 発行サービスは、既定で自動的に開始するように構成する必要があります。  
 **問題:**自動的に開始する World Wide Web 発行サービスが構成されていません。  
  
 **影響:** World Wide Web 発行サービスが自動的に開始しないサーバーが起動します。 このサービスが停止している場合リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性がありますできません。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-world-wide-web-publishing-service-to-start-automatically"></a>自動的に開始する World Wide Web 発行サービスを構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリック**World Wide Web 発行サービス**、] をクリックし、**プロパティ**します。  
  
3.  **全般**] タブで、変更、**スタートアップの種類**に**自動**、] をクリックし、**[OK]**します。  
  
### <a name="the-remote-registry-service-should-be-configured-to-start-automatically-by-default"></a>リモート レジストリ サービスは、既定で自動的に開始するように構成する必要があります。  
 **問題:**自動的に開始する、リモート レジストリ サービスが構成されていません。  
  
 **影響:**  
  
 サーバーの起動時に、リモート レジストリ サービスが自動的に開始しない可能性があります。 このサービスが停止するできない場合がありますを一部のネットワーク操作をリモートで実行できること。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-remote-registry-service-to-start-automatically"></a>自動的に開始するリモート レジストリ サービスを構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**リモート レジストリ**をクリックし、**プロパティ**します。  
  
3.  **全般**] タブで、変更、**スタートアップの種類**に**自動**、] をクリックし、**[OK]**します。  
  
### <a name="the-remote-desktop-gateway-service-should-be-configured-to-start-automatically-by-default"></a>リモート デスクトップ ゲートウェイ サービスは、既定で自動的に開始するように構成する必要があります。  
 **問題:**自動的に開始するリモート デスクトップ ゲートウェイ サービスが構成されていません。  
  
 **影響:**場合、このサービスが停止しているユーザーできない可能性がありますリモート Web アクセスを使用してコンピューターにアクセスします。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-remote-desktop-gateway-service-to-start-automatically"></a>自動的に開始するリモート デスクトップ ゲートウェイ サービスを構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**リモート デスクトップ ゲートウェイ**をクリックし、**プロパティ**します。  
  
3.  **全般**] タブで、変更、**スタートアップの種類**に**自動 (遅延開始)**、] をクリックし、**[OK]**します。  
  
### <a name="the-windows-time-service-should-be-configured-to-start-automatically-by-default"></a>Windows タイム サービスは、既定で自動的に開始するように構成する必要があります。  
 **問題:**自動的に開始する、Windows タイム サービスが構成されていません。  
  
 **影響:**このサービスが停止している場合は日付と時刻の同期は使用できません。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-windows-time-service-to-start-automatically"></a>自動的に開始する Windows タイム サービスを構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**Windows タイム**をクリックし、**プロパティ**します。  
  
3.  **全般**] タブで、変更、**スタートアップの種類**に**自動**、] をクリックし、**[OK]**します。  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-started"></a>分散トランザクション コーディネータ (MSDTC) サービスを開始する必要があります。  
 **問題:** MSDTC サービスがサーバーで実行されていません。  
  
 **影響:**いくつかの SQL Server または COM 関数が失敗する場合、このサービスが停止しています。 その結果、Microsoft SQL Server または COM 関数を使用するアプリケーションが正しく機能しない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-distributed-transaction-coordinator-service"></a>分散トランザクション コーディネータ サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**分散トランザクション コーディネータ**をクリックし、**開始**します。  
  
### <a name="the-netlogon-service-should-be-started"></a>Netlogon サービスを開始する必要があります。  
 **問題:**サーバー上の Netlogon サービスが実行されていません。  
  
 **影響:**ユーザーおよびサービス場合、このサービスが開始されていないサーバーは認証可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-netlogon-service"></a>Netlogon サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**Netlogon**をクリックし、**開始**します。  
  
### <a name="the-dns-client-service-should-be-started"></a>DNS クライアント サービスを開始する必要があります。  
 **問題:**サーバーで、DNS クライアント サービスが実行されていません。  
  
 **影響:**このサービスが開始されていない場合、サーバーできない可能性があります DNS 名を解決します。  
  
 **解決方法:**  
  
##### <a name="to-start-the-dns-client-service"></a>DNS クライアント サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**DNS クライアント**をクリックし、**開始**します。  
  
### <a name="the-dns-server-service-should-be-started"></a>DNS サーバー サービスを開始する必要があります。  
 **問題:**サーバーで、DNS サーバー サービスが実行されていません。  
  
 **影響:** DNS の更新は発生しませんが、DNS サーバー サービスが開始されていない場合。  
  
 **解決方法:**  
  
##### <a name="to-start-the-dns-server-service"></a>DNS サーバー サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**DNS サーバー**をクリックし、**開始**します。  
  
### <a name="active-directory-web-services-is-not-started"></a>Active Directory Web サービスが開始されていません。  
 **問題:** Active Directory Web サービスは開始されません。  
  
 **影響:** Active Directory Web サービス (ADWS) が開始されていません。 サーバー上の ADWS が停止しているか、無効な場合は、Windows PowerShell 用 Active Directory モジュールのなどのクライアント アプリケーション、または Active Directory 管理センターのアクセスまたはこのサーバーで実行されているディレクトリ サービスのインスタンスを管理することはできません。 For more information, see [What's New in AD DS: Active Directory Web Services](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) in the Windows Server Technical Library.  
  
 **解決方法:**  
  
##### <a name="to-start-the-active-directory-web-services-service"></a>Active Directory Web Services サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリック**Active Directory Web Services**、] をクリックし、**開始**します。  
  
### <a name="the-dhcp-client-service-should-be-started"></a>DHCP クライアント サービスを開始する必要があります。  
 **問題:**サーバーで DHCP クライアント サービスが実行されていません。  
  
 **影響:**場合、このサービスが停止しているクライアント コンピューターがサーバーから IP アドレスを受信ことはできません。  
  
 **解決方法:**  
  
##### <a name="to-start-the-dhcp-client-service"></a>DHCP クライアント サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**DHCP クライアント**をクリックし、**開始**します。  
  
### <a name="the-iis-admin-service-should-be-started"></a>IIS 管理サービスを開始する必要があります。  
 **問題:** IIS 管理サービスがサーバーで実行されていません。  
  
 **影響:**このサービスが停止している場合は、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-iis-admin-service"></a>IIS 管理サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリック**IIS 管理サービス**、] をクリックし、**開始**します。  
  
### <a name="the-world-wide-web-publishing-service-should-be-started"></a>World Wide Web 発行サービスを開始する必要があります。  
 **問題:** World Wide Web 発行サービスがサーバーで実行されていません。  
  
 **影響:**このサービスが停止している場合は、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-world-wide-web-publishing-service"></a>World Wide Web 発行サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリック**World Wide Web 発行サービス**、] をクリックし、**開始**します。  
  
### <a name="the-remote-desktop-gateway-service-should-be-started"></a>リモート デスクトップ ゲートウェイ サービスを開始する必要があります。  
 **問題:**サーバーで Remote Desktop Gateway サービスが実行されていません。  
  
 **影響:**場合、このサービスが停止しているユーザーできない可能性がありますリモート Web アクセスを使用してコンピューターにアクセスします。  
  
 **解決方法:**  
  
##### <a name="to-start-the-remote-desktop-gateway-service"></a>リモート デスクトップ ゲートウェイ サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**リモート デスクトップ ゲートウェイ**をクリックし、**開始**します。  
  
### <a name="the-windows-time-service-should-be-started"></a>Windows タイム サービスを開始する必要があります。  
 **問題:**サーバーで Windows タイム サービスが実行されていません。  
  
 **影響:**場合このサービスを停止すると、日付と時刻の同期は使用できません。  
  
 **解決方法:**  
  
##### <a name="to-start-the-windows-time-service"></a>Windows タイム サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**Windows タイム**をクリックし、**開始**します。  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-logon-account-should-be-nt-authoritynetwork-service"></a>分散トランザクション コーディネータ (MSDTC) サービスのログオン アカウントは NT authority \network Service をする必要があります。  
 **問題:**分散トランザクション コーディネータ (MSDTC) サービスの既定のログオン アカウントが変更されています。  
  
 **影響:**サービスが期待どおりに動作するために必要なアクセス許可がないです。 その結果、SQL Server または COM 関数を使用するアプリケーションが正しく機能しない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-logon-account-for-the-service"></a>サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**分散トランザクション コーディネータ**をクリックし、**プロパティ**します。  
  
3.  **ログオン**] タブで [**このアカウント**、種類**NT authority \network Service**、] をクリックし、**[OK]**します。  
  
### <a name="the-netlogon-service-should-use-the-local-system-account-as-its-logon-account"></a>Netlogon サービスは、ログオン アカウントとしてローカル システム アカウントを使用する必要があります。  
 **問題:** Netlogon サービス用の既定のログオン アカウントが変更されています。  
  
 **影響:**サービスが期待どおりに動作するために必要なアクセス許可がないです。 その結果、ユーザーとサービス、サーバーによって認証されない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-netlogon-service-logon-account"></a>Netlogon サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**Netlogon**をクリックし、**プロパティ**します。  
  
3.  **ログオン**] タブで [**ローカル システム アカウント**します。  
  
### <a name="the-dns-client-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>DNS クライアント サービスは、ログオン アカウントとして NT authority \network Service アカウントを使用する必要があります。  
 **問題:** DNS クライアント サービス用の既定のログオン アカウントが変更されました。  
  
 **影響:**サービスが期待どおりに動作するために必要なアクセス許可がないです。 その結果、サーバーできない可能性があります DNS 名を解決します。  
  
 **解決方法:**  
  
##### <a name="to-change-the-dns-client-service-logon-account"></a>DNS クライアント サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**DNS クライアント**をクリックし、**プロパティ**します。  
  
3.  **ログオン**] タブで [**このアカウント**、し、入力**NT authority \network Service**します。  
  
### <a name="the-dns-server-service-should-use-the-local-system-account-as-its-logon-account"></a>DNS サーバー サービスは、ログオン アカウントとしてローカル システム アカウントを使用する必要があります。  
 **問題:** DNS サーバー サービスの既定のログオン アカウントが変更されています。  
  
 **影響:**サービスが期待どおりに動作するために必要なアクセス許可がないです。 その結果、DNS の更新が発生しません。  
  
 **解決方法:**  
  
##### <a name="to-change-the-dns-server-service-logon-account"></a>DNS サーバー サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます  
  
2.  右クリックし、**DNS サーバー**をクリックし、**プロパティ**します。  
  
3.  **ログオン**] タブで [**ローカル システム アカウント**します。  
  
### <a name="active-directory-web-services-is-not-the-default-logon-account"></a>Active Directory Web サービスは既定のログオン アカウントはありません。  
 **問題:** Active Directory Web サービスは、既定のログオン アカウントではありません。 既定では、ログオン アカウントに設定が**ローカル システム アカウント**します。  
  
 **影響:** Active Directory Web サービス (ADWS) が開始されていません。 サーバー上の ADWS が停止しているか、無効な場合は、Windows PowerShell 用 Active Directory モジュールのなどのクライアント アプリケーション、または Active Directory 管理センターのアクセスまたはこのサーバーで実行されているディレクトリ サービスのインスタンスを管理することはできません。 For more information, see [What's New in AD DS: Active Directory Web Services](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) in the Windows Server Technical Library.  
  
 **解決方法:**  
  
##### <a name="to-change-the-active-directory-web-services-logon-account"></a>Active Directory Web サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリック**Active Directory Web Services**、] をクリックし、**プロパティ**します。  
  
3.  変更、**スタートアップの種類**に**自動**、] をクリックし、**OK**します。  
  
4.  Active Directory Web services**プロパティ**、] をクリックして、**ログオン**] タブ。  
  
5.  選択、**ローカル システム アカウント**オプションをクリックして**OK**します。  
  
### <a name="the-windows-update-service-should-use-the-local-system-account-as-its-logon-account"></a>Windows Update サービスは、ログオン アカウントとしてローカル システム アカウントを使用する必要があります。  
 **問題:**自動更新サービスの既定のログオン アカウントが変更されています。  
  
 **影響:**サービスが期待どおりに動作するために必要なアクセス許可がないです。 その結果、自動更新をサーバーが受信できません。  
  
 **解決方法:**  
  
##### <a name="to-change-the-windows-update-service-logon-account"></a>Windows Update サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**Windows Update**し、[プロパティ] をクリックします。  
  
3.  **ログオン**] タブで [**ローカル システム アカウント**します。  
  
### <a name="the-dhcp-client-service-should-use-the-nt-authoritylocalservice-account-as-its-logon-account"></a>DHCP クライアント サービスは、ログオン アカウントとして NT authority \localservice アカウントを使用する必要があります。  
 **問題:** DHCP クライアント サービス用の既定のログオン アカウントが変更されました。  
  
 **影響:**サービスが期待どおりに動作するために必要なアクセス許可がないです。 その結果、サーバーからは IP アドレス、クライアント コンピューターは受け取りません。  
  
 **解決方法:**  
  
##### <a name="to-change-the-dhcp-client-service-logon-account"></a>DHCP クライアント サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**DHCP クライアント**をクリックし、**プロパティ**します。  
  
3.  **ログオン**] タブで [**このアカウント**、し、入力**NT authority \localservice**します。  
  
### <a name="the-iis-admin-service-should-use-the-local-system-account-as-its-logon-account"></a>IIS 管理サービスは、ログオン アカウントとしてローカル システム アカウントを使用する必要があります。  
 **問題:** IIS 管理サービス用の既定のログオン アカウントが変更されました。  
  
 **影響:**サービスが必要なアクセス許可がない期待どおりに動作するために必要なです。 その結果、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-service-logon-account"></a>サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリック**IIS 管理サービス**、] をクリックし、**プロパティ**します。  
  
3.  **ログオン**] タブで [**ローカル システム アカウント**します。  
  
### <a name="the-world-wide-web-publishing-service-should-use-the-local-system-account-as-its-logon-account"></a>World Wide Web 発行サービスは、ログオン アカウントとしてローカル システム アカウントを使用する必要があります。  
 **問題:** World Wide Web 発行サービスの既定のログオン アカウントが変更されています。  
  
 **影響:**サービスが期待どおりに動作するために必要なアクセス許可がないです。 その結果、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-world-wide-web-publishing-service-logon-account"></a>World Wide Web 発行サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリック**World Wide Web 発行サービス**、] をクリックし、**プロパティ**します。  
  
3.  **ログオン**] タブで [**ローカル システム アカウント**します。  
  
### <a name="the-remote-desktop-gateway-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>リモート デスクトップ ゲートウェイ サービスは、ログオン アカウントとして NT authority \network Service アカウントを使用する必要があります。  
 **問題:**、リモート デスクトップ ゲートウェイ サービス用の既定のログオン アカウントが変更されました。  
  
 **影響:**サービスを適切なアクセス許可が期待どおりに機能していない可能性があります。 その結果、ユーザーはリモート Web アクセスを使用してコンピューターにアクセスできません可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-remote-desktop-gateway-service-logon-account"></a>リモート デスクトップ ゲートウェイ サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**リモート デスクトップ ゲートウェイ**をクリックし、**プロパティ**します。  
  
3.  **ログオン**] タブで [**このアカウント**、し、入力**NT authority \network Service**します。  
  
### <a name="the-windows-time-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>Windows タイム サービスは、ログオン アカウントとして NT authority \network Service アカウントを使用する必要があります。  
 **問題:** Windows タイム サービスの既定のログオン アカウントが変更されています。  
  
 **影響:**サービスを適切なアクセス許可が期待どおりに機能していない可能性があります。 その結果、日付と時刻の同期が使用可能なない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-windows-time-service-logon-account"></a>Windows タイム サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  右クリックし、**Windows タイム**をクリックし、**プロパティ**します。  
  
3.  **ログオン**] タブで [**このアカウント**、し、入力**NT authority \localservice**します。  
  
### <a name="the-built-in-administrators-group-does-not-have-the-right-to-log-on-as-batch-job"></a>組み込み Administrators グループにバッチ ジョブとしてログオンする権限がないです。  
 **問題:**組み込み Administrators グループにバッチ ジョブとしてログオンする権利はありません。  
  
 **影響:** 2147943785 のエラー コードと、アラートは失敗場合は、管理者にアラートを作成、管理者がログオンしていないときに実行するように設定します。  
  
 **Resolution:**  For information about how to give the built-in Administrators group permission to log on as a batch job, see [Give the built-in Administrator group the right to log on as a batch job](https://technet.microsoft.com/library/jj635076) (https://technet.microsoft.com/library/jj635076).  
  
### <a name="the-windows-firewall-is-turned-off"></a>Windows ファイアウォールが無効します。  
 **問題:** Windows ファイアウォールがオフにします。 既定値は、上です。  
  
 **影響:**悪意のあるアクティビティからサーバーを通過から一部の情報をブロックすることにより、サーバーとネットワークを保護ファイアウォールの設定に応じて Windows ファイアウォールが役立つことができます。  
  
 **解決方法:**  
  
##### <a name="to-turn-on-windows-firewall-on-the-server"></a>サーバーで Windows ファイアウォールを有効にするには  
  
1.  サーバーでコントロール パネルを開きます。  
  
2.  コントロール パネルで、をクリックして**システムとセキュリティ**、] をクリックし、**Windows ファイアウォール**します。  
  
3.  Windows ファイアウォール、] をクリックして**Windows ファイアウォールを有効または無効**を選択、**Windows ファイアウォールを有効にする**オプションをクリックして**OK**します。  
  
### <a name="the-internal-network-adapter-is-not-configured-to-register-ip-address-in-dns"></a>IP アドレスを DNS に登録する内部ネットワーク アダプターが構成されていません。  
 **問題:**その IP アドレスを DNS に登録する内部ネットワーク アダプターが構成されていません。  
  
 **影響:**内部ネットワーク アダプターの IP アドレスが DNS に登録されていない場合、できない可能性がありますサーバーのコンピューター名を使用してサーバーにアクセスします。  
  
 **解決方法:** DNS に登録する内部ネットワーク アダプターが構成されていることを確認します。  
  
### <a name="dns-the-values-for-the-dns-forwardingtimeout-and-recursiontimeout-registry-key-are-identical"></a>DNS: DNS の ForwardingTimeout および RecursionTimeout レジストリ キーの値は同じ  
 **問題:** DNS の ForwardingTimeout レジストリ キーの値は RecursionTimeout レジストリ キーの値と同じする必要がありますできません。  
  
 **影響:**名前でインターネット リソースにアクセスできない可能性があります。  
  
 **解決方法:**を ForwardingTimeout キーの値より大きい値は RecursionTimeout レジストリ キーの値を設定、\system\currentcontrolset\services\dns\parameters のレジストリにします。  
  
### <a name="the-forward-dns-zone-for-your-active-directory-domain-does-not-allow-secure-updates"></a>Active Directory ドメインの前方 DNS ゾーンがセキュリティで保護された更新プログラムを許可しません。  
 **問題:**保護された動的更新のみを許可するように、前方参照ゾーンを構成する必要があります。  
  
 **影響:**ときに許可されたユーザーのみ保護された動的更新を有効にして、ホストは、レコードに変更を加えることができます。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-forward-lookup-zone-for-your-active-directory-domain"></a>Active Directory ドメインの前方参照ゾーンを構成するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  Active Directory ドメインの前方参照ゾーンを右クリックし、をクリックして**プロパティ**します。  
  
3.  **動的更新**ドロップダウン リストで、**のみをセキュリティで保護**、] をクリックし、**OK**します。  
  
### <a name="the-forward-dns-zone-does-not-allow-secure-updates"></a>更新プログラムのサーバーに転送する DNS ゾーンをセキュリティで保護できません。  
 **問題:**保護された動的更新のみを許可するように _msdcs.* ゾーンの前方参照ゾーンを構成する必要があります。  
  
 **影響:**ときに許可されたユーザーのみ保護された動的更新を有効にして、ホストは、msdcs.* ゾーン内のレコードに変更を加えることができます。  
  
 **解決方法:**  
  
##### <a name="to-allow-secure-updates-in-the-msdcs-zone"></a>_Msdcs ゾーンのセキュリティで保護された更新を許可するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  _Msdcs ゾーンの前方参照ゾーンを右クリックし、をクリックして**プロパティ**します。  
  
3.  **動的更新**ドロップダウン リストで、**のみをセキュリティで保護**、] をクリックし、**OK**します。  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Internet Explorer セキュリティ強化の構成が有効になっていません。  
 **問題:** Internet Explorer セキュリティ強化の構成 (IE ESC) が現在無効になって、Administrators グループ。  
  
 **影響:** Administrators グループの Internet Explorer セキュリティ強化の構成が無効の場合、サーバーと Internet Explorer がコンテンツ Web を介して発生する悪意のある攻撃およびアプリケーション スクリプトへの露出増加します。  
  
 **解決方法:**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>Internet Explorer セキュリティ強化の構成を有効にするには  
  
1.  開いている**サーバー マネージャー** server、およびクリック**ローカル サーバー**します。  
  
2.  **プロパティ**] ウィンドウで、設定を変更**IE セキュリティ強化の構成**に**で**、] をクリックし、**[OK]**します。  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Internet Explorer セキュリティ強化の構成が有効になっていません。  
 **問題:** Internet Explorer セキュリティ強化の構成 (IE ESC) が現在無効になって、ユーザー グループ。  
  
 **影響:**、サーバーと Internet Explorer によってコンテンツ Web を介して発生する悪意のある攻撃およびアプリケーション スクリプトへの露出が増加 Internet Explorer セキュリティ強化の構成が有効でない場合、ユーザー グループ。  
  
 **解決方法:**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>Internet Explorer セキュリティ強化の構成を有効にするには  
  
1.  開いている**サーバー マネージャー**、] をクリックし、**ローカル サーバー**します。  
  
2.  **プロパティ**] ウィンドウで、設定を変更**IE セキュリティ強化の構成**に**で**、] をクリックし、**[OK]**します。  
  
### <a name="the-source-server-remains-in-active-directory-sites-and-services"></a>移行元サーバーが Active Directory サイトとサービスに残っています。  
 **問題:** Active Directory サイトとサービスの Windows Small Business Server を実行している移行元サーバーがまだ存在して、Default-First-Site-Name にします。  
  
 **影響:**アクティブ ディレクター サイトとサービスで、移行元サーバーが残っているクライアント コンピューターは接続の問題を発生する可能性が: s します。  
  
 **解決方法:**、移行元サーバーを降格、ドメインから削除して、および Active Directory サイトとサービスおよび Active Directory ユーザーとコンピューターから、移行元サーバーを削除します。  
  
### <a name="source-server-remains-in-sbscomputer-ou"></a>移行元サーバーが SBSComputer OU に  
 **問題:** Windows Small Business Server を実行している移行元サーバーが Active Directory ユーザーとコンピューターにまだ存在しています。  
  
 **影響:**ディレクターのアクティブ ユーザーとコンピューターに、移行元サーバーが残っているクライアント コンピューターは接続の問題を発生する可能性が: s します。  
  
 **解決方法:**、移行元サーバーを降格、ドメインから削除して、および Active Directory サイトとサービスおよび Active Directory ユーザーとコンピューターから、移行元サーバーを削除します。  
  
### <a name="a-group-policy-is-missing"></a>グループ ポリシーが見つかりません  
 **問題:**既定のドメイン ポリシーのグループ ポリシーが見つかりません。  
  
 **影響:**既定のドメイン ポリシーが正しい定義域関数に必要です。  
  
 **解決方法:**  
  
##### <a name="to-restore-a-missing-group-policy"></a>不足しているグループ ポリシーを復元するには  
  
1.  サーバーで gpmc.msc を開きます。  
  
2.  グループ ポリシー マネージャーが、ドメイン フォレストを展開しのコンソール ツリーを検索、**Default Domain Policy**グループ ポリシー オブジェクト。  
  
3.  ポリシーがツリーに表示されない場合は、システム状態のバックアップから復元します。  
  
### <a name="no-dns-name-server-resource-records"></a>DNS ネーム サーバー リソース レコード  
 **問題:**サーバーの前方参照ゾーンに DNS ネーム サーバー (NS) リソース レコードがありません。  
  
 **影響:** Active Directory ドメインの前方参照ゾーンに DNS ネーム サーバー (NS) リソース レコードが存在しない場合は、ユーザーは、ネットワークまたはインターネット上のリソースにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-restore-missing-dns-name-server-resource-records"></a>復元するに DNS ネーム サーバー リソース レコード  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  DNS マネージャーでは、Active Directory ドメインの前方参照ゾーンを右クリックし、をクリックして**プロパティ**します。  
  
3.  **ネーム サーバー**タブで、設定が正しいことを確認します。  
  
4.  必要な変更を行い] をクリックし、**OK**設定を保存します。  
  
### <a name="no-dns-name-server-records"></a>ない DNS ネーム サーバー レコード  
 **問題:**ない DNS ネーム サーバー (NS) リソース レコードが、サーバーの _msdcs ゾーン (例: _msdcs.contoso.local)。  
  
 **影響:** Active Directory ドメイン用の _msdcs ゾーンに DNS ネーム サーバー (NS) リソース レコードが存在しない場合は、ユーザーは、ネットワークまたはインターネット上のリソースにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-restore-missing-dns-name-server-records"></a>不足している DNS ネーム サーバー レコードを復元するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  DNS マネージャーで、_msdcs ゾーンの前方参照ゾーンを右クリックし、をクリックして**プロパティ**します。  
  
3.  **ネーム サーバー**タブで、設定が正しいことを確認します。  
  
4.  必要な変更を行い] をクリックし、**OK**設定を保存します。  
  
### <a name="no-dns-name-server-records"></a>ない DNS ネーム サーバー レコード  
 **問題:**ない DNS ネーム サーバー (NS) リソース レコードが委任された _msdcs 前方参照ゾーン用です。  
  
 **影響:** DNS ネーム サーバー (NS) リソース レコードがない場合、委任された _msdcs 前方参照ゾーンの DNS サーバー サービスがドメインの DNS リソース レコードを解決することはできず、起動しません。  
  
 **解決方法:**  
  
##### <a name="to-reconfigure-missing-dns-name-server-records"></a>不足している DNS ネーム サーバー レコードを再構成するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  DNS マネージャーでは、サーバー名を展開し、展開**前方参照ゾーン**します。  
  
3.  Active Directory ドメインの前方参照ゾーン] をクリックして (例: contoso.local)。  
  
4.  委任された _msdcs ゾーンが灰色のフォルダーとして表示されます。 _Msdcs ゾーンを右クリックし、をクリックして**プロパティ**します。  
  
5.  **ネーム サーバー**タブで、設定が正しいことを確認します。  
  
6.  必要な変更を行い] をクリックし、**OK**設定を保存します。  
  
### <a name="authenticated-users-not-a-member-of-the-pre-windows-2000-compatible-access-group"></a>認証されたユーザー、Pre-Windows 2000 Compatible Access グループのメンバーではないです。  
 **問題:** Authenticated Users グループが Pre-Windows 2000 Compatible Access グループのメンバーではありません。  
  
 **影響:**ネットワーク ユーザーが「アクセスが拒否されました」エラーを発生可能性がある場合は、組み込みの Authenticated Users グループが Pre-Windows 2000 Compatible Access グループのメンバーでないです。  
  
 **解決方法:**  
  
##### <a name="to-add-authenticated-users-to-the-pre-windows-2000-compatible-access-group"></a>認証されたユーザーを Pre-Windows 2000 Compatible Access グループに追加するには  
  
1.  サーバーで dsa.msc を開きます。  
  
2.  **Builtin**フォルダーを右クリックして**Pre-Windows 2000 Compatible Access**、] をクリックし、**プロパティ**します。  
  
3.  をクリックして**追加**、種類**Authenticated Users**、] をクリックし、**OK** 2 回します。  
  
### <a name="dns-client-not-configured"></a>DNS クライアントが構成されていません。  
 **問題:**のみ、サーバーの内部 IP アドレスを指定する DNS クライアントが構成されていません。  
  
 **影響:** DNS クライアントは、構成しなかった場合、サーバーの内部 IP アドレスのみを指定する、DNS 名前解決が失敗することができます。  
  
 **解決方法:**  
  
##### <a name="to-configure-dns-to-point-only-to-the-server-s-internal-ip-address"></a>サーバーの内部 IP アドレスのみを指定する DNS を構成するには  
  
1.  クライアント コンピューターからを起動、**プロパティ**ネットワーク接続のページです。  
  
2.  サーバーの内部 IP アドレスのみを指定する DNS が構成されていることを確認します。  
  
### <a name="default-application-pool-value-changed"></a>既定のアプリケーション プールの値が変更されました  
 **問題:** DefaultAppPool アプリケーション プールのワーカー プロセスの最大数が既定値を 1 に設定されていません。  
  
 **影響:**ユーザーは、Windows Small Business Server からの Web ベース サービスに接続できない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-reset-maximum-worker-processes-for-the-default-application-pool"></a>既定のアプリケーション プールのワーカー プロセスの最大数をリセットするには  
  
1.  サーバー上のインターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、をクリックして**アプリケーション プール**します。  
  
3.  **アプリケーション プール**、右クリック**DefaultAppPool**、] をクリックし、**高度な設定**します。  
  
4.  **高度な設定**の値を変更**ワーカー プロセスの最大数**をクリックして、1 **OK**します。  
  
5.  閉じる**Advanced Settings**、右クリックして**DefaultAppPool**、し、アプリケーション プールを再起動します。  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-account"></a>リモート Web アクセス用のアプリケーション プールが既定のアカウントを使用していません。  
 **問題:** RemoteAppPool アプリケーション プールが既定のアカウントで実行されていません。  
  
 **影響:**ネットワーク ユーザーがリモート Web アクセス Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-reset-the-remote-application-pool-to-use-the-default-account"></a>既定のアカウントを使用するリモート アプリケーション プールをリセットするには  
  
1.  サーバー上のインターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、をクリックして**アプリケーション プール**します。  
  
3.  **アプリケーション プール**、右クリック**RemoteAppPool**、] をクリックし、**高度な設定**します。  
  
4.  **Advanced Settings**、変更、**Identity**に**NetworkService**、] をクリックし、**[OK]**します。  
  
5.  閉じる**Advanced Settings**、右クリックして**RemoteAppPool**、し、アプリケーション プールを再起動します。  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-net-framework-version"></a>リモート Web アクセス用のアプリケーション プールが既定の .NET Framework のバージョンを使用していません。  
 **問題:** RemoteAppPool アプリケーション プールが Microsoft .NET Framework の既定のバージョンで実行されていません。  
  
 **影響:**ネットワーク ユーザーがリモート Web アクセス Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-net-framework-version-used-by-the-remoteapppool"></a>RemoteAppPool で使用される .NET Framework バージョンを変更するには  
  
1.  サーバー上のインターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、をクリックして**アプリケーション プール**します。  
  
3.  **アプリケーション プール**、右クリック**RemoteAppPool**、] をクリックし、**高度な設定**します。  
  
4.  **Advanced Settings**、変更、**.NET Framework バージョン**v4.0、] をクリックして**[OK]**します。  
  
5.  閉じる**Advanced Settings**、右クリックして**RemoteAppPool**、し、アプリケーション プールを再起動します。  
  
### <a name="the-remoteaccesslog-file-is-larger-than-1-gb-in-size"></a>RemoteAccess.log ファイルが 1 GB のサイズより大きい  
 **問題:** Remoteaccess.log ファイルのサイズが 1 GB を超えている場合、システム ドライブ上のディスクの空き領域エラーが発生することができます。  
  
 **影響:** Remoteaccess.log ファイルが大きすぎる場合は、空き領域の問題をしまう可能性があります。c: ドライブに s します。  
  
 **解決方法:**サーバーをバックアップした後、%ProgramData%\Microsoft\Windows \logs\webapps フォルダーにある Remoteaccess.log ファイルを削除することができます。  
  
### <a name="default-web-sites-log-directory-is-over-1-gb-in-size"></a>既定の Web サイトのログ ディレクトリが 1 GB を超えるサイズです。  
 **問題:**既定の Web サイトのログ フォルダーのサイズが 1 GB を超えている場合、システム ドライブ上のディスクの空き領域エラーが発生することができます。  
  
 **影響:**空き領域の問題が生じる場合は、既定の Web サイトのログ フォルダーが大きすぎる: c: ドライブに s  
  
 **解決方法:**後、サーバーをバックアップして、既定の Web サイトが停止している間は、C:\inetpub\logs\LogFiles\W3SVC1 フォルダー内のログ ファイルを削除することができます。 既定の Web サイトを開始します。  
  
### <a name="no-binding-for-ssl-on-all-ip-addresses"></a>すべての IP アドレスに SSL のバインドがないです。  
 **問題:**、サーバー上のすべての IP アドレスに Secure Sockets Layer (SSL) のバインドがありません。  
  
 **影響:** SSL がサーバーですべての IP アドレスにバインドされていない場合は、一部の Web サイトは使用できませんをユーザーにします。  
  
 **解決方法:**  
  
##### <a name="to-bind-ssl-to-all-ip-addresses-on-the-server"></a>サーバー上のすべての IP アドレスに SSL をバインドするには  
  
1.  サーバー上のインターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、**接続**] ウィンドウで、サーバーを展開し、[**サイト**、右クリック**既定の Web サイト**、] をクリックし、**バインドの編集]**します。  
  
3.  **サイト バインド**、] をクリックして**追加**、次の設定を選択します。  
  
    -   **種類** = **https**  
  
    -   **IP アドレス** = **All Unassigned**  
  
    -   **ポート**= 443  
  
4.  SSL 証明書を選択し、クリックして**OK**、変更を保存します。  
  
### <a name="no-binding-for-ssl-on-the-default-web-site"></a>既定の Web サイトに SSL のバインドがないです。  
 **問題:**既定の Web サイトに SSL のバインドはありません。  
  
 **影響:**場合は、既定の Web サイトに SSL がバインドされていない、一部の Web サイトはユーザーが利用できない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-bind-ssl-to-the-default-website"></a>既定の Web サイトに SSL をバインドするには  
  
1.  サーバー上のインターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、**接続**] ウィンドウで、サーバーを展開し、[**サイト**、右クリック**既定の Web サイト**、] をクリックし、**バインドの編集]**します。  
  
3.  **サイト バインド**、] をクリックして**追加**、次のオプションを選択します。  
  
    -   **種類** = **https**  
  
    -   **IP アドレス** = **All Unassigned**  
  
    -   **ポート**= 443  
  
    > [!NOTE]
    >  特定の IP アドレスのポート 443 の HTTPS バインドが存在する場合は、変更、**IP アドレス**属性には、そのバインド**すべて割り当てられていない**します。 この例外は IP アドレス 127.0.0.1 します。 127.0.0.1 のバインドは変更されません。  
  
4.  SSL 証明書を選択し、クリックして**OK**、変更を保存します。  
  
### <a name="a-certificate-expires-within-30-days"></a>30 日以内に失効する証明書  
 **問題:** 30 日以内、サーバー証明書が期限切れにします。  
  
 **影響:**サーバーは、有効期限が切れた証明書を使用できません。 証明書を過ぎると、ユーザーは Anywhere Access 機能を使用できない可能性があります。  
  
 **解決方法:**期限が切れないように、証明書を防ぐため、信頼された証明機関の証明書を更新します。  
  
### <a name="certificate-subject-does-not-match-the-name-configured-by-domain-name-wizard"></a>証明書のサブジェクトがドメイン名] ウィザードで設定した名前と一致しません。  
 **問題:**証明書のサブジェクトがドメイン名] ウィザードで設定した名前と一致しません。  
  
 **影響:**証明書のサブジェクトにドメイン名] ウィザードで設定した名前が一致しない場合、一部の Web サイトは初期化されません。 他のサイトは、エラーが表示「問題がある Web サイトのセキュリティ証明書を使用します」。  
  
 **解決方法:**この問題を解決するのには: Anywhere Access のウィザードのセットアップをもう一度実行し、証明書の正しいドメイン名を指定またはドメイン名を使用する場合に一致する新しい証明書を購入します。  
  
### <a name="one-or-more-user-accounts-have-duplicate-cn-names"></a>1 つまたは複数のユーザー アカウント重複した CN 名  
 **問題:** 1 つまたは複数のユーザー アカウント重複した CN 名: {0}。  
  
 **影響:**ユーザー アカウントには、重複した CN 名がある、ユーザーは、ネットワークにログオンできない可能性があります。 さらに、ユーザーを Active Directory の検索では、正しくない値を返すことができます。  
  
 **解決方法:**この問題を解決するのには: ネットワーク ユーザー アカウントに、重複がないことを確認"CN ="の名前。 これを簡単にするには、Active Directory の内容をレビューのテキスト ファイルにエクスポートする検討してください。 For information about how to do this, see [Using LDIFDE to import and export directory objects to Active Directory (Knowledge Base article 237677)](https://support.microsoft.com/kb/237677) (https://support.microsoft.com/kb/237677).  
  
### <a name="nt-backup-is-installed"></a>NT バックアップがインストールされています。  
 **問題:** Windows NT バックアップ プログラムがサーバーにインストールします。  
  
 **影響:** Windows Server Essentials は、Windows Server バックアップを使用します。 Windows NT バックアップ プログラムもインストールされている場合は、2 つのバックアップ プログラムの間で競合が存在します。 これには、Windows Server バックアップ プロセスが失敗する可能性があります。 競合もできない場合があります、サーバーを復元するバックアップを使用します。  
  
 **解決方法:**この問題を解決するのには: サーバーから NT バックアップ プログラムをアンインストールします。  
  
### <a name="iis-does-not-own-port-80-000080-or-port-443-0000443"></a>IIS がポート 80 (0.0.0.0:80) またはポート 443 (0.0.0.0:443) を所有していません。  
 **問題:**インターネット インフォメーション サービス (IIS) ではポート 80 (0.0.0.0:80) またはポート 443 を所有していません。 これらのポートは、他のアプリケーションによってバインドされています。  
  
 **影響:** Web アプリケーションの Windows Server Essentials がポート 80 の入力を求めるし、ポート 443 をユーザーにサービスを利用できるようにします。 別のプロセスまたはアプリケーションが既にポート 80 またはポート 443 を使用する場合は、Windows Server Essentials の Web アプリケーションは実行できません。 この場合、リモート Web アクセスおよびその他のアプリケーションがご利用いただけませんをユーザーにします。  
  
 **解決方法:**この問題を解決するのには: アプリケーションが既にポート 80 またはポート 443 を使用するか、そのアプリケーションは、別のポートを割り当てるをアンインストールするか。  
  
### <a name="the-default-website-is-not-running"></a>既定の Web サイトが実行されていません  
 **問題:**既定の Web サイトは、Windows Server Essentials 環境で実行されていません。  
  
 **影響:** Web アプリケーションの Windows Server Essentials の既定の Web サイトの使用を必要とします。 既定の Web サイトが実行されていない場合は、リモート Web アクセスおよびその他のアプリケーションがご利用いただけませんをユーザーにします。  
  
 **解決方法:**  
  
##### <a name="to-start-the-default-website"></a>既定の Web サイトを開始するには  
  
1.  サーバー上のインターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、をクリックして**サイト**します。  
  
3.  右クリック**既定の Web サイト**、] をポイント**Web サイトの管理**、] をクリックし、**開始**します。  
  
### <a name="read-and-script-permissions-for-the-remote-virtual-directory-are-incorrect"></a>/Remote 仮想ディレクトリに対する読み取りとスクリプトのアクセス許可が正しくないです。  
 **問題:** /Remote 仮想ディレクトリに読み取りとスクリプトのアクセス許可が割り当てられていません。  
  
 **影響:** /Remote 仮想ディレクトリの読み取りとスクリプトのアクセス許可が正しくない場合、ユーザーはリモート Web アクセスを使用できません。 リモート Web アクセスを使用して、インターネットを閲覧しようとすると、"HTTP Error 403.1 Forbidden"エラーを発生した可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-assign-read-and-script-permissions-to-the-remote-directory"></a>/Remote ディレクトリに読み取りとスクリプトのアクセス許可を割り当てる  
  
1.  サーバー上のインターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、をクリックして**サイト**します。  
  
3.  展開**既定の Web サイト**、し、展開**リモート**します。  
  
4.  **機能ビュー**、] をダブルクリック**ハンドラー マッピング**します。  
  
5.  **アクション**] ウィンドウで、をクリックして**機能のアクセス許可の編集**します。  
  
6.  選択、**読み取り**と**スクリプト**チェック ボックスをクリックして**OK**します。  
  
### <a name="http-redirect-is-either-set-or-inherited-on-the-remote-virtual-directory"></a>HTTP リダイレクトが、設定または/Remote 仮想ディレクトリの継承  
 **問題:** HTTP リダイレクト属性が予期せず設定または/Remote 仮想ディレクトリの継承します。  
  
 **影響:** HTTP リダイレクト属性が/Remote 仮想ディレクトリの設定は、リモート Web ワークプ レースは正しく機能しません。  
  
 **解決方法:**  
  
##### <a name="to-remove-the-http-redirect-attribute"></a>HTTP リダイレクト属性を削除するには  
  
1.  サーバー上のインターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、をクリックして**サイト**します。  
  
3.  展開**既定の Web サイト**、し、展開**リモート**します。  
  
4.  **機能ビュー**、] をダブルクリック**HTTP リダイレクト**します。  
  
5.  クリア、**この宛先に要求をリダイレクト**チェック ボックスをオンにし**適用**上、**アクション**ウィンドウ。  
  
### <a name="a-host-name-exists-for-port-80-on-the-default-website"></a>既定の Web サイト上のポート 80 にホスト名が存在します。  
 **問題:**既定の Web サイト上のポート 80 にホスト名が割り当てられます。  
  
 **影響:**のポート 80、既定の Web サイトに割り当てられるホスト名と、一部の Web アプリケーションの Windows Server Essentials に接続できません可能性があります。 ホスト名は不要であり、このような状況には推奨されません。  
  
 **解決方法:**  
  
##### <a name="to-clear-the-host-name-entry-for-port-80-on-the-default-website"></a>既定の Web サイト上のポート 80 にホスト名のエントリを消去するには  
  
1.  サーバー上のインターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、をクリックして**サイト**します。  
  
3.  **機能ビュー**、右クリックして**既定の Web サイト**、] をクリックし、**バインド**します。  
  
4.  **サイト バインド**を選択、**ポート 80 の http**に設定して、をクリックして**編集**します。  
  
5.  **サイト バインドの編集**をオフ、**ホスト名**エントリをクリックして**OK**します。  
  
### <a name="backup-does-not-succeed-because-of-a-hidden-partition"></a>隠しパーティションのためバックアップが成功しません。  
 **問題:** NTFS 以外のパーティションが Windows Server バックアップによってバックアップをスケジュールします。  
  
 **影響:** Windows Server バックアップが NTFS でフォーマットされたパーティションをバックアップできますのみです。  
  
 **解決方法:** NTFS 以外のパーティションをバックアップする Windows Server バックアップを構成しません。 For more information, see [Event IDs 12290 and 16387 are logged when system state backup fails on a Windows Server 2008-based computer (Knowledge Base article 968128)](https://support.microsoft.com/kb/968128) (https://support.microsoft.com/kb/968128).  
  
### <a name="the-most-recent-backup-did-not-succeed"></a>最新のバックアップは成功しませんでした。  
 **問題:**最近のバックアップの試行が正常に完了しませんでした。  
  
 **影響:**システムのバックアップの状態が正しくありません。  
  
 **解決方法:**イベント ログとバックアップのログの最新のバックアップ中に発生したエラーを確認します。  
  
### <a name="the-startup-type-for-the-file-replication-service-is-not-set-to-automatic"></a>ファイル レプリケーション サービスのスタートアップの種類が自動に設定されていません。  
 **問題:**スタートアップの種類が自動の既定値に設定されていない場合、ファイル レプリケーション サービス (FRS) は開始しない可能性があります。  
  
 **影響:**ファイル レプリケーション サービスが実行されていない場合、ドメイン コントローラーがそのサービスのアドバタイズを停止する可能性があります。 ログオン エラーやグループ ポリシー エラーなどの他の問題が生じる可能性が。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-file-replication-service-for-automatic-startup"></a>ファイル レプリケーション サービスが自動的に開始を構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、ダブルクリック**ファイル レプリケーション**します。  
  
3.  **スタートアップの種類**[**自動**、] をクリックし、**適用**します。  
  
### <a name="the-file-replication-service-is-not-running"></a>ファイル レプリケーション サービスが実行されていません  
 **問題:**ファイル レプリケーション サービスが実行されていません。  
  
 **影響:**ファイル レプリケーション サービスが実行されていない場合、ドメイン コントローラーがそのサービスのアドバタイズを停止する可能性があります。 この動作は、ログオン エラーやグループ ポリシー エラーなどの他の問題につながることができます。  
  
 **解決方法:**  
  
##### <a name="to-start-the-file-replication-service"></a>ファイル レプリケーション サービスを開始するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、ダブルクリック**ファイル レプリケーション サービス**します。  
  
3.  をクリックして**開始**します。  
  
### <a name="the-logon-account-for-the-file-replication-service-is-not-set-to-use-the-local-system-account"></a>ファイル レプリケーション サービスのログオン アカウントがローカル システム アカウントを使用して設定されていません。  
 **問題:**既定のログオン アカウントとしてローカル システム アカウントを使用するファイル レプリケーション サービスが構成されていません。  
  
 **影響:**ファイル レプリケーション サービスは既定のログオン アカウントとしてローカル システムを使用していない場合、アクセス許可に関連するエラーが発生する可能性があります。 これらのエラーは、他のエラーをトリガーすることができ、サービスのアドバタイズを停止するドメイン コントローラーが最終的に発生することができます。  
  
 **解決方法:**  
  
##### <a name="to-configure-local-system-as-the-default-logon-account-for-file-replication"></a>ファイル レプリケーションの既定のログオン アカウントとしてローカル システムを構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、ダブルクリック**ファイル レプリケーション**します。  
  
3.  **サービスのプロパティ**] ページで [、**ログオン**] タブ。  
  
4.  選択、**ローカル システム アカウント**オプションをクリックして**適用**します。  
  
5.  サービスを再起動します。  
  
### <a name="the-startup-type-for-the-dfs-replication-service-is-not-set-to-automatic"></a>DFS Replication サービスのスタートアップの種類が自動に設定されていません。  
 **問題:**スタートアップの種類が自動の既定値に設定されていない場合、DFS Replication サービスが開始しない可能性があります。  
  
 **影響:** DFS Replication サービスが実行されていない場合、ドメイン コントローラーがそのサービスのアドバタイズを停止する可能性があります。 ログオン エラーやグループ ポリシー エラーなどの他の問題が生じる可能性が。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-dfs-replication-service-for-automatic-startup"></a>DFS レプリケーション サービスが自動的に開始を構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、ダブルクリック**DFS レプリケーション**します。  
  
3.  **スタートアップの種類**[**自動**、] をクリックし、**適用**します。  
  
### <a name="the-dfs-replication-service-is-not-running"></a>DFS Replication サービスが実行されていません  
 **問題:** DFS Replication サービスが実行されていません。  
  
 **影響:** DFS Replication サービスが実行されていない場合、ドメイン コントローラーがそのサービスのアドバタイズを停止する可能性があります。 この動作は、ログオン エラーやグループ ポリシー エラーなどの他の問題につながることができます。  
  
 **解決方法:**  
  
##### <a name="to-start-the-dfs-replication-service"></a>DFS レプリケーション サービスを開始するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、ダブルクリック**DFS レプリケーション**します。  
  
3.  をクリックして**開始**します。  
  
### <a name="the-dfs-replication-service-is-not-is-not-set-to-use-the-local-system-account"></a>ローカル システム アカウントを使用するサービスは、DFS レプリケーションが設定されていません。  
 **問題:**既定のログオン アカウントとしてローカル システム アカウントを使用する、DFS Replication サービスが設定されていません。  
  
 **影響:**場合は、DFS Replication サービスは既定のログオン アカウントとしてローカル システムを使用していない、アクセス許可に関連するエラーが発生する可能性があります。 これらのエラーは、他のエラーをトリガーすることができ、サービスのアドバタイズを停止するドメイン コントローラーが最終的に発生することができます。  
  
 **解決方法:**  
  
##### <a name="to-configure-dfs-replication-to-use-local-system-as-the-default-logon-account"></a>既定のログオン アカウントとしてローカル システムを使用する DFS レプリケーションを構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、ダブルクリック**DFS レプリケーション**します。  
  
3.  **サービスのプロパティ**] ページで [、**ログオン**] タブ。  
  
4.  選択、**ローカル システム アカウント**オプションをクリックして**適用**します。  
  
5.  サービスを再起動します。  
  
### <a name="the-windows-server-office-365-integration-service-is-not-set-to-use-the-local-system-account"></a>Windows Server Office 365 統合サービスがローカル システム アカウントを使用して設定されていません。  
 **問題:**既定のログオン アカウントとしてローカル システム アカウントを使用する Windows Server Office 365 統合サービスが設定されていません。  
  
 **影響:**場合は、Windows Server Office 365 統合サービスは既定のログオン アカウントとしてローカル システムを使用していない、Office 365 の一部の機能が正常に機能しない可能性があります。 アクセス許可に関連するエラーが発生することも可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-office-365-integration-service-to-use-local-system-as-the-default-logon-account"></a>既定のログオン アカウントとしてローカル システムを使用する Office 365 統合サービスを構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、ダブルクリック**Windows Server Office 365 統合サービス**します。  
  
3.  **サービスのプロパティ**] ページで [、**ログオン**] タブ。  
  
4.  選択、**ローカル システム アカウント**オプションをクリックして**適用**します。  
  
5.  サービスを再起動します。  
  
### <a name="the-windows-server-office-365-integration-service-is-not-running"></a>Windows Server Office 365 統合サービスが実行されていません  
 **問題:** Windows Server Office 365 統合サービスが実行されていません。  
  
 **影響:** Windows Server Office 365 統合サービスが実行されていない場合は、Office 365 のクラウド ベースの機能は利用できません。  
  
 **解決方法:**  
  
##### <a name="to-start-the-windows-server-office-365-integration-service"></a>Windows Server Office 365 統合サービスを開始するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、ダブルクリック**Windows Server Office 365 統合サービス**します。  
  
3.  をクリックして**開始**します。  
  
### <a name="the-startup-type-for-the-windows-server-office-365-integration-service-is-not-set-to-automatic"></a>Windows Server Office 365 統合サービスのスタートアップの種類が自動に設定されていません。  
 **問題:**スタートアップの種類が自動の既定値に設定されていない場合、Windows Server Office 365 統合サービスが開始しない可能性があります。  
  
 **影響:** Windows Server Office 365 統合サービスが実行されていない場合は、Office 365 のクラウド ベースの機能は利用できません。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-office-365-integration-service-for-automatic-startup"></a>Office 365 の統合サービスが自動的に開始を構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、ダブルクリック**Windows Server Office 365 統合サービス**します。  
  
3.  **スタートアップの種類**[**自動**、] をクリックし、**適用**します。  
  
### <a name="a-registry-value-is-missing-or-set-incorrectly"></a>レジストリの値が不足しているか、正しく設定  
 **問題:** HKEY_LOCAL_MACHINE \Software\Microsoft\Rpc\RpcProxy の下にあるレジストリ キーが正しくない値が含まれますか存在しません。  
  
 **影響:** RPCProxy のレジストリ キーが正しく設定されていない場合は、次のようなエラー メッセージが表示される可能性があります:"コンピューターは、リモート デスクトップ ゲートウェイ サーバーが一時的に使用できないために、リモート コンピューターに接続できません。 後で再接続するか、ネットワーク管理者に問い合わせてください。"  
  
 **解決方法:**  
  
##### <a name="to-correct-the-registry-setting"></a>レジストリ設定を修正するには  
  
1.  レジストリ エディターを開きます。  
  
2.  次のレジストリ キーに移動します。  
  
     HKEY_LOCAL_MACHINE\Software\Microsoft\Rpc\RpcProxy  
  
3.  "Website"という名前の文字列が既定の Web サイトのデータ値を持つことを確認します。  
  
    -   データ値が正しくない場合は、正しい値を使用する文字列を変更します。  
  
    -   文字列が存在しない場合、"Website"という名前の新しい文字列を作成し、既定の Web サイトにデータの値を設定します。"  
  
### <a name="the-startup-type-for-the-block-level-backup-engine-service-is-not-set-to-manual"></a>ブロック レベルのバックアップ エンジン サービスのスタートアップの種類が手動に設定されていません。  
 **問題:**ブロック レベルのバックアップ エンジン サービスは、手動の既定のスタートアップの種類を使用していません。  
  
 **影響:**スタートアップの種類が手動に設定されていない場合、ブロック レベルのバックアップ エンジン サービスは開始しない可能性があります。 : この問題には、Windows Server バックアップ ジョブが失敗する可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-for-manual-startup"></a>ブロック レベルのバックアップ エンジン サービスで手動スタートアップを構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、ダブルクリック**ブロック レベルのバックアップ エンジン サービス**します。  
  
3.  **スタートアップの種類**[**手動**、] をクリックし、**適用**します。  
  
### <a name="the-logon-account-for-the-block-level-backup-engine-service-is-not-set-to-use-the-local-system-account"></a>ブロック レベルのバックアップ エンジン サービスのログオン アカウントがローカル システム アカウントを使用して設定されていません。  
 **問題:**ブロック レベルのバックアップ エンジン サービスが既定のログオン アカウントとしてローカル システム アカウントを使用する設定されていません。  
  
 **影響:**ブロック レベルのバックアップ エンジン サービスは既定のログオン アカウントとしてローカル システムを使用していない場合、アクセス許可に関連するエラーが発生する可能性があります。 これらのエラーは、Windows Server バックアップのジョブを正常に完了しないようにできます。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-to-use-local-system-as-the-default-logon-account"></a>既定のログオン アカウントとしてローカル システムを使用する、ブロック レベルのバックアップ エンジン サービスを構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、ダブルクリック**ブロック レベルのバックアップ エンジン サービス**します。  
  
3.  **サービスのプロパティ**] ページで [、**ログオン**] タブ。  
  
4.  選択、**ローカル システム アカウント**オプションをクリックして**適用**します。  
  
5.  サービスを再起動します。  
  
### <a name="the-common-name-on-the-certificate-that-is-bound-to-the-wss-certificate-web-service-website-does-not-match-the-server-name"></a>WSS Certificate Web Service Web サイトにバインドされている証明書の共通名がサーバー名と一致しません。  
 **問題:**有効でない証明書は IIS で、WSS Certificate Web Service Web サイトにバインドします。 この証明書の共通名がサーバー名と一致しません。  
  
 **影響:**、WSS Certificate Web Service Web サイトに有効でない証明書をバインドすると、[接続] ウィザードが正しく機能しません。  
  
 **解決方法:**  
  
##### <a name="to-configure-a-valid-certificate-for-the-wss-certificate-web-service"></a>WSS Certificate Web Service の有効な証明書を構成するには  
  
1.  サーバー上のインターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、をクリックして**サイト**します。  
  
3.  右クリック**WSS Certificate Web Service**、] をクリックし、**バインドの編集]**します。  
  
4.  **サイト バインド**、] をクリックして**HTTPS**、] をクリックし、**編集**します。  
  
5.  **サイト バインドの編集**の**SSL 証明書**、サーバーと同じ名前を持つ証明書を選択します。  
  
6.  複数の証明書のエントリに、サーバーと同じ名前がある場合は、クリックして**ビュー**をどの証明書が有効な場合を特定し、適切な証明書を選択します。  
  
### <a name="there-appears-to-be-a-problem-with-the-certificate-binding-for-the-remote-desktop-gateway-service"></a>リモート デスクトップ ゲートウェイ サービスの証明書のバインドに問題の可能性があります。  
 **問題:**、リモート デスクトップ ゲートウェイ サービス用の証明書が正しくバインドされていないと思われます。  
  
 **影響:**、リモート デスクトップ ゲートウェイ サービス用の証明書が正しく構成されていない場合、ユーザーは、リモート Web アクセスに接続できません。  
  
 **解決方法:**  
  
##### <a name="to-fix-the-binding-for-the-remote-desktop-gateway-service"></a>リモート デスクトップ ゲートウェイ サービスのバインドを修正するには  
  
-   管理者としてコマンド プロンプトを開き、次のコマンドを入力します。  
  
    ```  
    REG ADD HKLM\SYSTEM\CurrentControlSet\services\HTTP\Parameters\SslBindingInfo\0.0.0.0:443  /v DefaultFlags /t REG_DWORD /d 1 /f  
    net stop tsgateway  
    net start tsgateway  
    ```  
  
     For more information, see [How to Manage the Remote Desktop Gateway Service in Windows Server Essentials (Knowledge Base article 2472211)](https://support.microsoft.com/kb/2472211) (https://support.microsoft.com/kb/2472211).
