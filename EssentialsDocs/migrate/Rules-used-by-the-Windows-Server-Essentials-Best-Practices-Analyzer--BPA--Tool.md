---
title: Windows Server Essentials ベスト プラクティス アナライザー (BPA) ツールで使用される規則
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850693"
---
# <a name="rules-used-by-the-windows-server-essentials-best-practices-analyzer-bpa-tool"></a>Windows Server Essentials ベスト プラクティス アナライザー (BPA) ツールで使用される規則

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

この記事では、によって、Windows Server Essentials ベスト プラクティス アナライザー (BPA) を使用するルールについて説明します。 BPA サーバーを調べて、Windows Server Essentials を実行しているし、問題について説明し、それらを解決するための推奨事項を提供するレポートを表示します。 推奨事項は、Windows Server essentials 製品サポート組織によって開発されています。  
  
## <a name="using-the-tool"></a>ツールの使用  
 Windows Server 2011 Essentials、Small Business Server の Windows 2011 Essentials、または Windows Home Server 2011 に移行が完了したら、移行先サーバーで BPA を実行してから、Windows Server Essentials に移行する場合、標準のプラクティスは、設定とデータ。 ツールは、いつでもダッシュボードから実行できます。  
  
#### <a name="to-run-the--windows-server-essentials-bpa-on-the-server"></a>サーバーで、Windows Server Essentials BPA を実行するには  
  
1.  サーバーに管理者としてログオンしてから、ダッシュボードを開きます。  
  
2.  ダッシュボードで **[デバイス]** タブをクリックします。  
  
3.  **[サーバー タスク]** ウィンドウで、**[ベスト プラクティス アナライザー]** をクリックします。  
  
4.  BPA の各メッセージを確認し、必要な場合は指示に従って問題を解決します。  
  
## <a name="rules-used-by-the-best-practices-analyzer"></a>ベスト プラクティス アナライザーが使用する規則  
  
### <a name="disable-ip-filtering"></a>IP フィルタリングを無効にする  
 **問題点:** IP フィルタリングは現在サーバー上で有効になっています。 IP フィルタリングを無効にする必要があります。  
  
 **影響:** IP フィルタリングが有効になっていると、ネットワーク トラフィックがブロックされる可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-disable-ip-filtering"></a>IP フィルタリングを無効にするには  
  
1.  サーバーで regedit.exe を開きます。  
  
2.  HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters に移動します。  
  
3.  **[EnableSecurityFilters]** を右クリックして、**[修正]** をクリックします。  
  
4.  **[DWORD (32 ビット) 値の編集]** ウィンドウで、**[値のデータ]** フィールドをゼロ (0) にしてから、**[OK]** をクリックします。  
  
5.  変更を適用するには、サーバーを再起動します。  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-set-to-start-automatically-by-default"></a>分散トランザクション コーディネーター (MSDTC) サービスは、既定で自動的に開始するように設定する必要がある  
 **問題点:** MSDTC サービスは、自動的に開始するように構成されていません  
  
 **影響:** サーバーを起動したときに、MSDTC サービスが自動的に開始しない可能性があります。 このサービスが停止している場合、SQL または COM の機能の一部が正常に機能しない可能性があります。 結果として、Microsoft SQL Server または COM 機能を使用するアプリケーションが正しく機能しなくなる可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-msdtc-service-to-start-automatically"></a>MSDTC サービスが自動的に開始するように設定するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[分散トランザクション コーディネーター]** サービスを右クリックし、**[プロパティ]**.をクリックします。  
  
3.  **[全般]** タブで、**[スタートアップの種類]** を **[自動 (遅延開始)]** に変更し、**[OK]** をクリックします。  
  
### <a name="the-netlogon-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように Netlogon サービスを構成する必要がある  
 **問題点:** Netlogon サービスは、自動的に開始するように構成されていません。  
  
 **影響:** サーバーを起動したときに、Netlogon サービスが自動的に開始しない可能性があります。 このサービスが停止している場合、ユーザーおよびサービスがサーバーによって認証されない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-netlogon-service-to-start-automatically"></a>Netlogon サービスが自動的に開始するように設定するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Netlogon]** サービスを右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、**[スタートアップの種類]** を **[自動]** に変更し、**[OK]** をクリックします。  
  
### <a name="the-dns-client-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように DNS クライアント サービスを構成する必要がある  
 **問題点:** DNS クライアント サービスが自動的に開始するように構成されていません。  
  
 **影響:** サーバーを起動したときに、DNS Client サービスが自動的に開始しない可能性があります。 このサービスが停止している場合、サーバーが DNS 名を解決できない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-dns-client-service-to-start-automatically"></a>DNS クライアント サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DNS クライアント]** サービスを右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、**[スタートアップの種類]** を **[自動]** に変更し、**[OK]** をクリックします。  
  
### <a name="the-dns-server-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように DNS サーバー サービスを構成する必要がある  
 **問題点:** DNS サーバー サービスは、自動的に開始するように構成されていません。  
  
 **影響:** サーバーを起動したときに、DNS サーバー サービスが自動的に開始しない可能性があります。 このサービスが停止している場合、DNS の更新が行われません。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-dns-server-service-to-start-automatically"></a>DNS サーバー サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DNS サーバー]** サービスを右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、**[スタートアップの種類]** を **[自動]** に変更し、**[OK]** をクリックします。  
  
### <a name="active-directory-web-services-is-not-set-to-the-default-start-mode"></a>Active Directory Web サービスが既定の開始モードに設定されていない  
 **問題点:** Active Directory Web サービスの開始モードが、既定の [自動] に設定されていません。  
  
 **影響:** Active Directory Web サービス (ADWS) が既定の開始モードの [自動] に設定されません。 サーバー上の ADWS が停止しているか、無効になっている場合、Windows PowerShell 用 Active Directory モジュールや Active Directory 管理センターなどのクライアント アプリケーションは、このサーバー上で実行されているディレクトリ サービス インスタンスにアクセスして、管理することができません。 詳細については、次を参照してください。 [AD DS では新機能。Active Directory Web Services](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) Windows Server テクニカル ライブラリにします。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-active-directory-web-services-service-to-start-automatically"></a>Active Directory Web サービスのサービスを自動的に開始するように設定するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Active Directory Web サービス]** サービスを右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、**[スタートアップの種類]** を **[自動]** に変更し、**[OK]** をクリックします。  
  
### <a name="the-dhcp-client-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように DHCP クライアント サービスを構成する必要がある  
 **問題点:** DHCP Client サービスは、自動的に開始するように構成されていません。  
  
 **影響:** サーバーを起動したときに、DHCP クライアント サービスが自動的に開始しません。 このサービスが停止している場合、クライアント コンピューターはサーバーから IP アドレスを受信できません。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-dhcp-client-service-to-start-automatically"></a>DHCP クライアント サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DHCP クライアント]** サービスを右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、**[スタートアップの種類]** を **[自動]** に変更し、**[OK]** をクリックします。  
  
### <a name="the-iis-admin-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように IIS 管理サービスを構成する必要がある  
 **問題点:** IIS 管理サービスは、自動的に開始するように構成されていません。  
  
 **影響:** サーバーを起動したときにIIS 管理サービスが自動的に開始しません。 このサービスが停止している場合、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-iis-admin-service-to-start-automatically"></a>IIS 管理サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[IIS 管理サービス]** を右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、**[スタートアップの種類]** を **[自動]** に変更し、**[OK]** をクリックします。  
  
### <a name="the-world-wide-web-publishing-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように World Wide Web 発行サービスを構成する必要がある  
 **問題点:** World Wide Web 発行サービスは、自動的に開始するように構成されていません。  
  
 **影響:** サーバーを起動したときに、World Wide Web 発行サービスが自動的に開始しない可能性があります。 このサービスが停止している場合、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-world-wide-web-publishing-service-to-start-automatically"></a>World Wide Web 発行サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[World Wide Web 発行サービス]** を右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、**[スタートアップの種類]** を **[自動]** に変更し、**[OK]** をクリックします。  
  
### <a name="the-remote-registry-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように リモート レジストリ サービスを構成する必要がある  
 **問題点:** リモート レジストリ サービスは、自動的に開始するように構成されていません。  
  
 **影響:**  
  
 サーバーを起動したときにリモート レジストリ サービスが自動的に開始しない可能性があります。 このサービスが停止している場合、一部のネットワーク操作をリモートで実行できない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-remote-registry-service-to-start-automatically"></a>リモート レジストリ サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[リモート レジストリ]** サービスを右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、**[スタートアップの種類]** を **[自動]** に変更し、**[OK]** をクリックします。  
  
### <a name="the-remote-desktop-gateway-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように リモート デスクトップ ゲートウェイ サービスを構成する必要がある  
 **問題点:** リモート デスクトップ ゲートウェイ サービスは、自動的に開始するように構成されていません。  
  
 **影響:** このサービスが停止している場合、ユーザーはリモート Web アクセスを使用してコンピューターにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-remote-desktop-gateway-service-to-start-automatically"></a>リモート デスクトップ ゲートウェイ サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[リモート デスクトップ ゲートウェイ]** を右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、**[スタートアップの種類]** を **[自動 (遅延開始)]** に変更し、**[OK]** をクリックします。  
  
### <a name="the-windows-time-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように Windows タイム サービスを構成する必要がある  
 **問題点:** Windows タイム サービスは、自動的に開始するように構成されていません。  
  
 **影響:** このサービスが停止している場合、データと時間の同期が使用できません。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-windows-time-service-to-start-automatically"></a>Windows タイム サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Windows タイム]** サービスを右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、**[スタートアップの種類]** を **[自動]** に変更し、**[OK]** をクリックします。  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-started"></a>分散トランザクション コーディネーター (MSDTC) サービスを開始する必要がある  
 **問題点:** MSDTC サービスがサーバー上で実行していません。  
  
 **影響:** このサービスが停止している場合、一部の SQL Server または COM 関数が失敗する可能性があります。 結果として、Microsoft SQL Server または COM 機能を使用するアプリケーションが正しく機能しなくなる可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-distributed-transaction-coordinator-service"></a>分散トランザクション コーディネーター サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[分散トランザクション コーディネーター]** サービスを右クリックしてから、**[開始]** をクリックします。  
  
### <a name="the-netlogon-service-should-be-started"></a>Netlogon サービスを開始する必要がある  
 **問題点:** Netlogon サービスがサーバー上で実行していません。  
  
 **影響:** サービスが開始していないと、サーバーはユーザーとサービスを認証しない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-netlogon-service"></a>Netlogon サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Netlogon]** サービスを右クリックしてから、**[開始]** をクリックします。  
  
### <a name="the-dns-client-service-should-be-started"></a>DNS クライアント サービスを開始する必要がある  
 **問題点:** DNS クライアント サービスがサーバー上で実行していません。  
  
 **影響:** このサービスが開始していない場合、サーバーが DNS 名を解決できない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-dns-client-service"></a>DNS クライアント サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DNS クライアント]** サービスを右クリックしてから、**[開始]** をクリックします。  
  
### <a name="the-dns-server-service-should-be-started"></a>DNS サーバー サービスを開始する必要がある  
 **問題点:** DNS サーバー サービスがサーバー上で実行していません。  
  
 **影響:** DNS サーバー サービスが開始していない場合、DNS の更新が発生しない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-dns-server-service"></a>DNS サーバー サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DNS サーバー]** サービスを右クリックしてから、**[開始]** をクリックします。  
  
### <a name="active-directory-web-services-is-not-started"></a>Active Directory Web サービスが開始していない  
 **問題点:** Active Directory Web サービスが開始していません。  
  
 **影響:** Active Directory Web サービス (ADWS) が開始していません。 サーバー上の ADWS が停止しているか、無効になっている場合、Windows PowerShell 用 Active Directory モジュールや Active Directory 管理センターなどのクライアント アプリケーションは、このサーバー上で実行されているディレクトリ サービス インスタンスにアクセスして、管理することができません。 詳細については、次を参照してください。 [AD DS では新機能。Active Directory Web Services](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) Windows Server テクニカル ライブラリにします。  
  
 **解決方法:**  
  
##### <a name="to-start-the-active-directory-web-services-service"></a>Active Directory Web サービスのサービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Active Directory Web サービス]** を右クリックし、**[開始]** をクリックします。  
  
### <a name="the-dhcp-client-service-should-be-started"></a>DHCP クライアント サービスを開始する必要がある  
 **問題点:** DHCP クライアント サービスがサーバー上で実行していません。  
  
 **影響:** このサービスが停止している場合、クライアント コンピューターはサーバーから IP アドレスを受信できません。  
  
 **解決方法:**  
  
##### <a name="to-start-the-dhcp-client-service"></a>DHCP クライアント サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DHCP クライアント]** サービスを右クリックしてから、**[開始]** をクリックします。  
  
### <a name="the-iis-admin-service-should-be-started"></a>IIS 管理サービスを開始する必要がある  
 **問題点:** IIS 管理サービスは、サーバー上で実行されていません。  
  
 **影響:** このサービスが停止している場合、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-iis-admin-service"></a>IIS 管理サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[IIS 管理サービス]** を右クリックしてから、**[開始]** をクリックします。  
  
### <a name="the-world-wide-web-publishing-service-should-be-started"></a>World Wide Web 発行サービスを開始する必要がある  
 **問題点:** World Wide Web 発行サービスがサーバー上で実行していません。  
  
 **影響:** このサービスが停止している場合、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-world-wide-web-publishing-service"></a>World Wide Web 発行サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[World Wide Web 発行サービス]** を右クリックしてから、**[開始]** をクリックします。  
  
### <a name="the-remote-desktop-gateway-service-should-be-started"></a>リモート デスクトップ ゲートウェイ サービスを開始する必要がある  
 **問題点:** リモート デスクトップ ゲートウェイ サービスがサーバー上で実行していません。  
  
 **影響:** このサービスが停止している場合、ユーザーはリモート Web アクセスを使用してコンピューターにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-remote-desktop-gateway-service"></a>リモート デスクトップ ゲートウェイ サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[リモート デスクトップ ゲートウェイ]** サービスを右クリックしてから、**[開始]** をクリックします。  
  
### <a name="the-windows-time-service-should-be-started"></a>Windows タイム サービスを開始する必要がある  
 **問題点:** Windows タイム サービスがサーバー上で実行していません。  
  
 **影響:** このサービスが停止している場合、データと時間の同期が使用できなくなります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-windows-time-service"></a>Windows タイム サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Windows タイム]** サービスを右クリックしてから、**[開始]** をクリックします。  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-logon-account-should-be-nt-authoritynetwork-service"></a>分散トランザクション コーディネーター (MSDTC) サービスのログオン アカウントは NT AUTHORITY\Network Service とする必要がある  
 **問題点:** 分散トランザクション コーディネーター (MSDTC) サービス用の既定のログオン アカウントが変更されています。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 その結果、SQL Server または COM 関数を使用するアプリケーションが正常に動作しない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-logon-account-for-the-service"></a>サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[分散トランザクション コーディネーター]** サービスを右クリックし、**[プロパティ]**.をクリックします。  
  
3.  **[ログオン]** タブで **[このアカウント]** をクリックし、「**NT AUTHORITY\Network Service**」と入力してから、**[OK]** をクリックします。  
  
### <a name="the-netlogon-service-should-use-the-local-system-account-as-its-logon-account"></a>Netlogon サービスはローカル システム アカウントをログオン アカウントとして使用する必要がある  
 **問題点:** Netlogon サービス用の既定のログオン アカウントが変更されています。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、ユーザーおよびサービスがサーバーによって認証されない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-netlogon-service-logon-account"></a>Netlogon サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Netlogon]** サービスを右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[ローカル システム アカウント]** をクリックします。  
  
### <a name="the-dns-client-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>DNS クライアント サービスでは、ログオン アカウントとして NT AUTHORITY\Network Service アカウントを使用する必要がある  
 **問題点:** DNS クライアント サービス用の既定のログオン アカウントが変更されています。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、サーバーが DNS の名前を解決できない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-dns-client-service-logon-account"></a>DNS クライアント サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DNS クライアント]** サービスを右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[このアカウント]** をクリックしてから、「**NT AUTHORITY\Network Service**」と入力します。  
  
### <a name="the-dns-server-service-should-use-the-local-system-account-as-its-logon-account"></a>DNS サーバー サービスは、ログオン アカウントとしてローカル システム アカウントを使用する必要があります。  
 **問題点:** DNS サーバー サービス用の既定のログオン アカウントが変更されています。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、DNS の更新が行われない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-dns-server-service-logon-account"></a>DNS サーバー サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DNS サーバー]** サービスを右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[ローカル システム アカウント]** をクリックします。  
  
### <a name="active-directory-web-services-is-not-the-default-logon-account"></a>Active Directory Web サービスは既定のログオン アカウントではない  
 **問題点:** Active Directory Web サービスは、既定のログオン アカウントではありません。 既定では、ログオン アカウントは ”**ローカル システム アカウント**" に設定されています。  
  
 **影響:** Active Directory Web サービス (ADWS) が開始していません。 サーバー上の ADWS が停止しているか、無効になっている場合、Windows PowerShell 用 Active Directory モジュールや Active Directory 管理センターなどのクライアント アプリケーションは、このサーバー上で実行されているディレクトリ サービス インスタンスにアクセスして、管理することができません。 詳細については、次を参照してください。 [AD DS では新機能。Active Directory Web Services](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) Windows Server テクニカル ライブラリにします。  
  
 **解決方法:**  
  
##### <a name="to-change-the-active-directory-web-services-logon-account"></a>Active Directory Web サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Active Directory Web サービス]** を右クリックし、**[プロパティ]** をクリックします。  
  
3.  **[スタートアップの種類]** を **[自動]** に変更し、**[OK]** をクリックします。  
  
4.  [Active Directory Web サービス] の **[プロパティ]** にある **[ログオン]** タブをクリックします。  
  
5.  **[ローカル システム アカウント]** オプションをクリックしてから、**[OK]** をクリックします。  
  
### <a name="the-windows-update-service-should-use-the-local-system-account-as-its-logon-account"></a>Windows Update サービスはローカル システム アカウントをログオン アカウントとして使用する必要がある  
 **問題点:** 自動更新サービス用の既定のログオン アカウントが変更されています。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、サーバーは自動更新を受信しない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-windows-update-service-logon-account"></a>Windows Update サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Windows Update]** サービスを右クリックしてから、[プロパティ] をクリックします。  
  
3.  **[ログオン]** タブで **[ローカル システム アカウント]** をクリックします。  
  
### <a name="the-dhcp-client-service-should-use-the-nt-authoritylocalservice-account-as-its-logon-account"></a>DHCP クライアント サービスでは、ログオン アカウントとして NT AUTHORITY\LocalService アカウントを使用する必要がある  
 **問題点:** DHCP クライアント サービス用の既定のログオン アカウントが変更されています。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、クライアント コンピューターは、サーバーから IP アドレスを受信しません。  
  
 **解決方法:**  
  
##### <a name="to-change-the-dhcp-client-service-logon-account"></a>DHCP クライアント サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DHCP クライアント]** サービスを右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[このアカウント]** をクリックしてから、「**NT AUTHORITY\LocalService**」と入力します。  
  
### <a name="the-iis-admin-service-should-use-the-local-system-account-as-its-logon-account"></a>IIS 管理サービスはローカル システム アカウントをログオン アカウントとして使用する必要がある  
 **問題点:** IIS 管理サービス用の既定のログオン アカウントが変更されています。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-service-logon-account"></a>サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[IIS 管理サービス]** を右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[ローカル システム アカウント]** をクリックします。  
  
### <a name="the-world-wide-web-publishing-service-should-use-the-local-system-account-as-its-logon-account"></a>World Wide Web 発行サービスはローカル システム アカウントをログオン アカウントとして使用する必要がある  
 **問題点:** World Wide Web 発行サービス用の既定のログオン アカウントが変更されています。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-world-wide-web-publishing-service-logon-account"></a>World Wide Web 発行サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[World Wide Web 発行サービス]** を右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[ローカル システム アカウント]** をクリックします。  
  
### <a name="the-remote-desktop-gateway-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>リモート デスクトップ ゲートウェイ サービスでは、ログオン アカウントとして NT AUTHORITY\Network Service アカウントを使用する必要がある  
 **問題点:** リモート デスクトップ ゲートウェイ サービス用の既定のログオン アカウントが変更されています。  
  
 **影響:** サービスに、想定どおりに動作するための適切なアクセス許可がない可能性があります。 結果として、ユーザーは、リモート Web アクセスを使用してコンピューターにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-remote-desktop-gateway-service-logon-account"></a>リモート デスクトップ ゲートウェイ サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[リモート デスクトップ ゲートウェイ]** を右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[このアカウント]** をクリックしてから、「**NT AUTHORITY\Network Service**」と入力します。  
  
### <a name="the-windows-time-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>Windows タイム サービスでは、ログオン アカウントとして NT AUTHORITY\Network Service アカウントを使用する必要がある  
 **問題点:** Windows タイム サービス用の既定のログオン アカウントが変更されています。  
  
 **影響:** サービスに、想定どおりに動作するための適切なアクセス許可がない可能性があります。 結果として、日付と時刻の同期が使用できない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-windows-time-service-logon-account"></a>Windows タイム サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Windows タイム]** サービスを右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[このアカウント]** をクリックしてから、「**NT AUTHORITY\LocalService**」と入力します。  
  
### <a name="the-built-in-administrators-group-does-not-have-the-right-to-log-on-as-batch-job"></a>ビルトイン Administrators グループに、バッチ ジョブとしてログオンする権限がない  
 **問題点:** ビルトイン Administrators グループに、バッチ ジョブとしてログオンする権限がありません。  
  
 **影響:** 管理者がアラートを作成し、管理者がログオンしていないときに実行するように設定すると、アラートはエラー コード 2147943785 で失敗します。  
  
 **解決方法:** 組み込みの Administrators グループ バッチ ジョブとしてログオンするためのアクセス許可を付与する方法については、次を参照してください。[組み込みの Administrator グループにバッチ ジョブとしてログオンする権利を付与](https://technet.microsoft.com/library/jj635076)(https://technet.microsoft.com/library/jj635076)します。  
  
### <a name="the-windows-firewall-is-turned-off"></a>Windows ファイアウォールが無効になっている  
 **問題点:** Windows ファイアウォールが無効になっています。 既定値は有効です。  
  
 **影響:** ファイアウォールの設定に応じて、Windows ファイアウォールは、一部の情報がサーバーを通過するのをブロックして、悪意のあるアクティビティからサーバーとネットワークを保護します。  
  
 **解決方法:**  
  
##### <a name="to-turn-on-windows-firewall-on-the-server"></a>サーバーで Windows ファイアウォールを有効にするには  
  
1.  サーバーの [コントロール パネル] を開きます。  
  
2.  [コントロール パネル] で、**[システムとセキュリティ]**、**[Windows ファイアウォール]** の順にクリックします。  
  
3.  [Windows ファイアウォール] で、**[Windows ファイアウォールを有効または無効にする]** をクリックします。**[Windows ファイアウォールを有効にする]** オプションを選択してから、**[OK]** をクリックします。  
  
### <a name="the-internal-network-adapter-is-not-configured-to-register-ip-address-in-dns"></a>内部ネットワーク アダプターが、IP アドレスを DNS に登録するように構成されていない  
 **問題点:** 内部ネットワーク アダプターが、IP アドレスを DNS に登録するように構成されていません。  
  
 **影響:** 内部ネットワーク アダプターの IP アドレスが DNS に登録されていない場合、サーバーのコンピューター名を使用してサーバーにアクセスできない可能性があります。  
  
 **解決方法:** 内部ネットワーク アダプターが DNS に登録するように構成されていることを確認します。  
  
### <a name="dns-the-values-for-the-dns-forwardingtimeout-and-recursiontimeout-registry-key-are-identical"></a>DNS:DNS のレジストリ キー ForwardingTimeout および RecursionTimeout の値が同一である  
 **問題点:** DNS の ForwardingTimeout レジストリ キーの値は RecursionTimeout レジストリ キーの値と同じでない必要があります。  
  
 **影響:** 名前でインターネット リソースにアクセスできない可能性があります。  
  
 **解決方法:** RecursionTimeout レジストリ キーの値を ForwardingTimeout キーの値より大きい値に設定します。これらのキーは HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters のレジストリにあります。  
  
### <a name="the-forward-dns-zone-for-your-active-directory-domain-does-not-allow-secure-updates"></a>Active Directory ドメインの前方 DNS ゾーンで、セキュリティで保護された更新が許可されていない  
 **問題点:** 前方参照ゾーンがセキュリティで保護された動的更新のみを許可するように設定する必要があります。  
  
 **影響:** セキュリティで保護された動的更新を有効にすると、承認済みのユーザーとホスト以外はレコードを変更できなくなります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-forward-lookup-zone-for-your-active-directory-domain"></a>Active Directory ドメインの前方参照ゾーンを構成するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  Active Directory ドメインの前方参照ゾーンを右クリックし、**[プロパティ]** をクリックします。  
  
3.  **[動的更新]** ドロップダウン リストで、**[セキュリティ保護のみ]**、**[OK]** の順にクリックします。  
  
### <a name="the-forward-dns-zone-does-not-allow-secure-updates"></a>セキュリティで保護された更新が、前方 DNS ゾーンで許可されない  
 **問題点:**_msdcs.* ゾーンの前方参照ゾーンを、セキュリティで保護された動的更新のみを許可するように設定する必要があります。  
  
 **影響:** セキュリティで保護された動的更新を有効にすると、承認済みユーザーとホスト以外は、msdcs.* ゾーン内のレコードを変更できなくなります。  
  
 **解決方法:**  
  
##### <a name="to-allow-secure-updates-in-the-msdcs-zone"></a>_msdcs ゾーンでセキュリティで保護された更新を許可するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  _msdcs ゾーンの [前方参照ゾーン] を右クリックし、**[プロパティ]** をクリックします。  
  
3.  **[動的更新]** ドロップダウン リストで、**[セキュリティ保護のみ]**、**[OK]** の順にクリックします。  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Internet Explorer セキュリティ強化の構成が無効になっている  
 **問題点:** 現在 Internet Explorer セキュリティ強化の構成 (IE ESC) が、Administrators グループのない有効。 にします。  
  
 **影響:** Administrators グループで Internet Explorer セキュリティ強化の構成が無効の場合、サーバーと Internet Explorer は Web コンテンツおよびアプリケーション スクリプトを介して発生する悪意のある攻撃への露出が増加しています。  
  
 **解決方法:**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>Internet Explorer セキュリティ強化の構成を有効にするには  
  
1.  サーバーで **[サーバー マネージャー]** を開き、**[ローカル サーバー]** をクリックします。  
  
2.  **[プロパティ]** ウィンドウで、**[IE セキュリティ強化の構成]** の設定を **[有効]** にしてから、**[OK]** をクリックします。  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Internet Explorer セキュリティ強化の構成が無効になっている  
 **問題点:** Internet Explorer セキュリティ強化の構成 (IE ESC) は現在無効なユーザー グループです。  
  
 **影響:** Users グループで Internet Explorer セキュリティ強化の構成が無効の場合、サーバーと Internet Explorer は Web コンテンツおよびアプリケーション スクリプトを介して発生する悪意のある攻撃への露出が増加しています。  
  
 **解決方法:**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>Internet Explorer セキュリティ強化の構成を有効にするには  
  
1.  **[サーバー マネージャー]** を開いて、**[ローカル サーバー]** をクリックします。  
  
2.  **[プロパティ]** ウィンドウで、**[IE セキュリティ強化の構成]** の設定を **[有効]** にしてから、**[OK]** をクリックします。  
  
### <a name="the-source-server-remains-in-active-directory-sites-and-services"></a>移行元サーバーが Active Directory サイトとサービスに残っている  
 **問題点:** Windows Small Business Server を実行している移行元サーバーが、Default-First-Site-Name の Active Directory サイトおよびサービスにまだ存在しています。  
  
 **影響:** クライアント コンピューターが接続の問題を発生する場合は、ソース サーバーは、Active Director サイトとサービスでは、: %s。  
  
 **解決方法:** 移行元サーバーを降格し、ドメインから削除した後、Active Directory サイトとサービスおよび Active Directory ユーザーとコンピューターから移行元サーバーを削除する必要があります。  
  
### <a name="source-server-remains-in-sbscomputer-ou"></a>移行元サーバーが SBSComputer OU に残っている  
 **問題点:** Windows Small Business Server を実行している移行元サーバーが、Active Directory ユーザーとコンピューターにまだ存在しています。  
  
 **影響:** クライアント コンピューターが接続の問題を発生する場合は、ソース サーバーは、Active Director ユーザーとコンピューターでは、: %s。  
  
 **解決方法:** 移行元サーバーを降格し、ドメインから削除した後、Active Directory サイトとサービスおよび Active Directory ユーザーとコンピューターから移行元サーバーを削除する必要があります。  
  
### <a name="a-group-policy-is-missing"></a>グループ ポリシーが見つからない  
 **問題点:** 既定のドメイン ポリシーのグループ ポリシーが見つかりません。  
  
 **影響:** 正しい定義域関数には、既定のドメイン ポリシーが必要です。  
  
 **解決方法:**  
  
##### <a name="to-restore-a-missing-group-policy"></a>不足しているグループ ポリシーを復元するには  
  
1.  サーバーで gpmc.msc を開きます。  
  
2.  [グループ ポリシー マネージャー] で、ドメイン フォレストを展開し、**既定のドメイン ポリシー**のグループ ポリシー オブジェクトのコンソール ツリーを検索します。  
  
3.  ツリーにポリシーが表示されない場合は、システム状態のバックアップから復元します。  
  
### <a name="no-dns-name-server-resource-records"></a>DNS ネーム サーバー リソース レコードがない  
 **問題点:** サーバーの前方参照ゾーンに、DNS ネーム サーバー (NS) リソース レコードがありません。  
  
 **影響:** Active Directory ドメインの前方参照ゾーンに DNS ネーム サーバー (NS) のリソース レコードが存在しない場合、ユーザーは、ネットワークまたはインターネットにあるリソースにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-restore-missing-dns-name-server-resource-records"></a>DNS ネーム サーバー リソース レコードを復元するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  DNS マネージャーで、Active Directory ドメインの前方参照ゾーンを右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[ネーム サーバー]** タブで、設定が正しいことを確認します。  
  
4.  必要な変更を行ってから、**[OK]** をクリックして設定を保存します。  
  
### <a name="no-dns-name-server-records"></a>DNS ネーム サーバー レコードがない  
 **問題点:** サーバーの _msdcs ゾーン (例: _msdcs.contoso.local) に DNS ネーム サーバー (NS) のリソース レコードがありません。  
  
 **影響:** Active Directory ドメイン用の _msdcs ゾーンに DNS ネーム サーバー (NS) リソース レコードが存在しない場合、ユーザーは、ネットワークまたはインターネットにあるリソースにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-restore-missing-dns-name-server-records"></a>DNS ネーム サーバー レコードを復元するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  [DNS マネージャー] で、_msdcs ゾーンの [前方参照ゾーン] を右クリックし、**[プロパティ]** をクリックします。  
  
3.  **[ネーム サーバー]** タブで、設定が正しいことを確認します。  
  
4.  必要な変更を行ってから、**[OK]** をクリックして設定を保存します。  
  
### <a name="no-dns-name-server-records"></a>DNS ネーム サーバー レコードがない  
 **問題点:** 委任された _msdcs 前方参照ゾーン用の DNS ネーム サーバー (NS) リソース レコードがありません。  
  
 **影響:** 委任された _msdcs 前方参照ゾーン用の DNS ネーム サーバー (NS) のリソース レコードが存在しない場合、DNS サーバー サービスは、ドメインの DNS リソース レコードを解決できず、開始に失敗します。  
  
 **解決方法:**  
  
##### <a name="to-reconfigure-missing-dns-name-server-records"></a>不足している DNS ネーム サーバー レコードを再構成するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  [DNS マネージャー] で、サーバー名を展開し、**[前方参照ゾーン]** を展開します。  
  
3.  Active Directory ドメインの前方参照ゾーン (例: contoso.local) をクリックします。  
  
4.  委任された _msdcs ゾーンが灰色のフォルダーとして表示されます。 _msdcs ゾーンを右クリックし、**[プロパティ]** をクリックします。  
  
5.  **[ネーム サーバー]** タブで、設定が正しいことを確認します。  
  
6.  必要な変更を行ってから、**[OK]** をクリックして設定を保存します。  
  
### <a name="authenticated-users-not-a-member-of-the-pre-windows-2000-compatible-access-group"></a>認証されたユーザーは、Pre-Windows 2000 Compatible Access グループのメンバーではない  
 **問題点:** Authenticated Users グループが、Pre-Windows 2000 Compatible Access グループのメンバーではありません。  
  
 **影響:** 組み込みの Authenticated Users グループが Pre-Windows 2000 Compatible Access グループのメンバーではない場合、ネットワークのユーザーに対して "アクセスが拒否されました” エラーが発生する可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-add-authenticated-users-to-the-pre-windows-2000-compatible-access-group"></a>認証されたユーザーを Pre-Windows 2000 Compatible Access グループのメンバーに追加するには  
  
1.  サーバーで dsa.msc を開きます。  
  
2.  **Builtin** フォルダーで、**[Pre-Windows 2000 Compatible Access]** を右クリックしてから、**[プロパティ]** をクリックします。  
  
3.  **[追加]** をクリックし、「**Authenticated Users**」と入力してから、**[OK]** を 2 回クリックします。  
  
### <a name="dns-client-not-configured"></a>DNS クライアントが構成されていない  
 **問題点:** DNS クライアントが、サーバーの内部 IP アドレスのみを指定するように構成されていません。  
  
 **影響:** DNS クライアントが、サーバーの内部 IP アドレスのみを指定するように構成されていない場合、DNS の名前の解決が失敗する可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-dns-to-point-only-to-the-server-s-internal-ip-address"></a>サーバーの内部 IP アドレスのみを指定する DNS を構成するには  
  
1.  クライアント コンピューターから、ネットワーク接続の **[プロパティ]** ページを開きます。  
  
2.  DNS がサーバーの内部 IP アドレスのみを指定するように構成されていることを確認します。  
  
### <a name="default-application-pool-value-changed"></a>既定のアプリケーション プールの値が変更されている  
 **問題点:** DefaultAppPool アプリケーション プールのワーカー プロセスの最大数が既定値の 1 に設定されていません。  
  
 **影響:** ユーザーが Windows Small Business Server の Web ベースのサービスに接続できない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-reset-maximum-worker-processes-for-the-default-application-pool"></a>既定のアプリケーション プールのワーカー プロセスの最大数をリセットするには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、**[アプリケーション プール]** をクリックします。  
  
3.  **[アプリケーション プール]** で、**[DefaultAppPool]** を右クリックし、**[詳細設定]** をクリックします。  
  
4.  **[詳細設定]** で、**[ワーカー プロセスの最大数]** の値を 1 に変更してから、**[OK]** をクリックします。  
  
5.  **[詳細設定]** を閉じ、**[DefaultAppPool]** を右クリックしてから、アプリケーション プールを停止して再開します。  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-account"></a>リモート Web アクセス用のアプリケーション プールが既定のアカウントを使用していない  
 **問題点:** RemoteAppPool アプリケーション プールが、既定のアカウントで実行されていません。  
  
 **影響:** ネットワーク ユーザーがリモート Web アクセスの Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-reset-the-remote-application-pool-to-use-the-default-account"></a>既定のアカウントを使用するためにリモート アプリケーション プールをリセットするには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、**[アプリケーション プール]** をクリックします。  
  
3.  **[アプリケーション プール]** で、**[RemoteAppPool]** を右クリックしてから、**[詳細設定]** をクリックします。  
  
4.  **[詳細設定]** で、**[ID]** を**NetworkService** に変更してから、**[OK]** をクリックします。  
  
5.  **[詳細設定]** を閉じ、**[RemoteAppPool]** を右クリックしてから、アプリケーション プールを停止して再開します。  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-net-framework-version"></a>リモート Web アクセス用のアプリケーション プールが既定の .NET Framework バージョンを使用していない  
 **問題点:** RemoteAppPool のアプリケーション プールが Microsoft .NET Framework の既定のバージョンで実行されていません。  
  
 **影響:** ネットワーク ユーザーがリモート Web アクセスの Web サイトにアクセスできない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-change-the-net-framework-version-used-by-the-remoteapppool"></a>RemoteAppPool で使用される .NET Framework のバージョンを変更するには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、**[アプリケーション プール]** をクリックします。  
  
3.  **[アプリケーション プール]** で、**[RemoteAppPool]** を右クリックしてから、**[詳細設定]** をクリックします。  
  
4.  **[詳細設定]** で、**[.NET Framework バージョン]** を v4.0 に変更してから、**[OK]** をクリックします。  
  
5.  **[詳細設定]** を閉じ、**[RemoteAppPool]** を右クリックしてから、アプリケーション プールを停止して再開します。  
  
### <a name="the-remoteaccesslog-file-is-larger-than-1-gb-in-size"></a>RemoteAccess.log ファイルのサイズが 1 GB より大きい  
 **問題点:** Remoteaccess.log ファイルのサイズが 1 GB を超えている場合、システム ドライブ上のディスクの空き領域が少ないというエラーが発生する可能性があります。  
  
 **影響:** Remoteaccess.log ファイルが大きすぎる場合に、空き領域の問題があります: c: ドライブで s。  
  
 **解決方法:** サーバーのバックアップ後、%ProgramData%\Microsoft\Windows Server\Logs\WebApps フォルダーにある Remoteaccess.log ファイルを削除することができます。  
  
### <a name="default-web-sites-log-directory-is-over-1-gb-in-size"></a>既定の Web サイトのログ ディレクトリのサイズが 1 GB を超える  
 **問題点:** 既定の web サイトのログ フォルダーのサイズが 1 GB を超える場合、システム ドライブ上のディスク領域不足領域エラーが発生したことができます。  
  
 **影響:** 空き領域の問題が生じる場合は、既定の web サイトのログ フォルダーが大きすぎます c: ドライブに s。  
  
 **解決方法:** サーバーのバックアップ後、既定の Web サイトの停止中に、C:\inetpub\logs\LogFiles\W3SVC1 フォルダー内のログ ファイルを削除することができます。 その後、既定の Web サイトを開始します。  
  
### <a name="no-binding-for-ssl-on-all-ip-addresses"></a>すべての IP アドレスに SSL のバインドがない  
 **問題点:** サーバー上のすべての IP アドレスに Secure Sockets Layer (SSL) のバインドがありません。  
  
 **影響:** SSL がサーバー上のすべての IP アドレスにバインドされていない場合、ユーザーは一部の Web サイトを使用できなくなります。  
  
 **解決方法:**  
  
##### <a name="to-bind-ssl-to-all-ip-addresses-on-the-server"></a>サーバー上のすべての IP アドレスに SSL をバインドするには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] の **[接続]** ウィンドウで、サーバー、**[サイト]** の順に展開し、**[既定の Web サイト]** を右クリックしてから、**[バインドの編集]** をクリックします。  
  
3.  **[サイトのバインド]** で、**[追加]** をクリックしてから、次の設定を選択します。  
  
    -   **型** = **https**  
  
    -   **IP アドレス** = **すべて未割り当て**  
  
    -   **[ポート]** = 443  
  
4.  SSL 証明書を選択し、**[OK]** をクリックして変更を保存します。  
  
### <a name="no-binding-for-ssl-on-the-default-web-site"></a>既定の Web サイトに SSL のバインドがない  
 **問題点:** 既定の Web サイトに SSL のバインドがありません。  
  
 **影響:** 既定の Web サイトに SSL がバインドされていない場合、ユーザーは一部の Web サイトを使用できない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-bind-ssl-to-the-default-website"></a>既定の Web サイトに SSL をバインドするには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] の **[接続]** ウィンドウで、サーバー、**[サイト]** の順に展開し、**[既定の Web サイト]** を右クリックしてから、**[バインドの編集]** をクリックします。  
  
3.  **[サイトのバインド]** で、**[追加]** をクリックしてから、次のオプションを選択します。  
  
    -   **型** = **https**  
  
    -   **IP アドレス** = **すべて未割り当て**  
  
    -   **[ポート]** = 443  
  
    > [!NOTE]
    >  特定の IP アドレスにポート 443 の HTTPS バインドが存在する場合は、そのバインドの **[IP アドレス]** 属性を**未使用の IP アドレスすべて**に変更します。 この場合の例外は IP アドレス 127.0.0.1 です。 127.0.0.1 のバインドは変更しないでください。  
  
4.  SSL 証明書を選択し、**[OK]** をクリックして変更を保存します。  
  
### <a name="a-certificate-expires-within-30-days"></a>証明書の有効期限が 30 日以内に切れる  
 **問題点:** サーバー証明書は、30 日以内に有効期限が切れます。  
  
 **影響:** サーバーは有効期限が切れた証明書を使用できません。 証明書の有効期限が切れると、ユーザーは Anywhere Access 機能を使用できない可能性があります。  
  
 **解決方法:** 証明書が期限切れにならないようにするには、証明書を信頼された証明機関の証明書に更新してください。  
  
### <a name="certificate-subject-does-not-match-the-name-configured-by-domain-name-wizard"></a>証明書のサブジェクトが [ドメイン名] ウィザードで設定した名前と一致しない  
 **問題点:** 証明書のサブジェクトが [ドメイン名] ウィザードで設定した名前と一致しません。  
  
 **影響:** 証明書のサブジェクトが [ドメイン名] ウィザードで設定した名前と一致しない場合、一部の Web サイトは初期化されません。 他のサイト、エラーが表示されます「問題があるこの web サイトのセキュリティ証明書を使用します」。  
  
 **解決方法:** この問題を解決するのには: Anywhere Access のウィザードのセットアップをもう一度実行し、証明書の適切なドメイン名を指定またはのいずれかを使用するドメイン名に一致する新しい証明書を購入します。  
  
### <a name="one-or-more-user-accounts-have-duplicate-cn-names"></a>1 つ以上のユーザー アカウントに重複した CN 名がある  
 **問題点:** 1 つまたは複数のユーザー アカウントがある重複した CN 名:{0}します。  
  
 **影響:** ユーザー アカウントに重複する CN 名がある場合、ユーザーはネットワークにログオンできない可能性があります。 さらに、Active Directory でユーザーを検索すると、正しくない値が返される可能性があります。  
  
 **解決方法:** この問題を解決するのには: ネットワーク ユーザー アカウントに、重複がないことを確認"CN ="の名前。 より簡単に行うため、確認用に Active Directory の内容をテキスト ファイルにエクスポートすることを検討してください。 これを行う方法については、次を参照してください。[をインポートおよびディレクトリ オブジェクトを Active Directory (サポート技術情報の記事 237677) にエクスポートを使用して LDIFDE](https://support.microsoft.com/kb/237677) (https://support.microsoft.com/kb/237677)します。  
  
### <a name="nt-backup-is-installed"></a>NT のバックアップがインストールされている  
 **問題点:** Windows NT バックアップ プログラムがサーバーにインストールされています。  
  
 **影響:** Windows Server Essentials では、Windows Server バックアップを使用します。 Windows NT バックアップ プログラムもインストールされている場合、2 つのバックアップ プログラムの間に競合が存在する可能性があります。 これにより、Windows Server バックアップのプロセスが失敗することがあります。 また、競合により、バックアップを使用してサーバーを復元できなくなる場合があります。  
  
 **解決方法:** この問題を解決するのには: のサーバーから NT バックアップ プログラムをアンインストールします。  
  
### <a name="iis-does-not-own-port-80-000080-or-port-443-0000443"></a>IIS がポート 80 (0.0.0.0:80) またはポート 443 (0.0.0.0:443) を保有していない  
 **問題点:** インターネット インフォメーション サービス (IIS) がポート 80 (0.0.0.0:80) またはポート 443 を保有していません。 これらのポートは、現在他のアプリケーションによってバインドされています。  
  
 **影響:** Windows Server Essentials の web アプリケーションでは、ポート 80 とポート 443 をユーザーにサービスを利用できるようにの使用が必要です。 別のプロセスやアプリケーションは、ポート 80 またはポート 443 に既に使用して、Windows Server Essentials の web アプリケーションは実行できません。 このような場合は、ユーザーはリモート Web アクセスおよびその他のアプリケーションを使用できません。  
  
 **解決方法:** この問題を解決するのには: 既にポート 80 またはポート 443 を使用してか、別のポートには、そのアプリケーションに割り当てるアプリケーションをアンインストールするか。  
  
### <a name="the-default-website-is-not-running"></a>既定の Web サイトが実行されていない  
 **問題点:** 既定の web サイトは、Windows Server Essentials 環境で実行されていません。  
  
 **影響:** Windows Server Essentials の web アプリケーションでは、既定の web サイトの使用が必要です。 既定の Web サイトが実行されていない場合、ユーザーはリモート Web アクセスおよびその他のアプリケーションを使用できません。  
  
 **解決方法:**  
  
##### <a name="to-start-the-default-website"></a>既定の Web サイトを開始するには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] で、サーバー名を展開し、**[サイト]** をクリックします。  
  
3.  **[既定の Web サイト]** を右クリックし、**[Web サイトの管理]** をポイントしてから、**[開始]** をクリックします。  
  
### <a name="read-and-script-permissions-for-the-remote-virtual-directory-are-incorrect"></a>/Remote 仮想ディレクトリに対する読み取りとスクリプトのアクセス許可が正しくない  
 **問題点:**/Remote 仮想ディレクトリに対して読み取りとスクリプトのアクセス許可が割り当てられていません。  
  
 **影響:**/Remote 仮想ディレクトリに対する読み取りとスクリプトのアクセス許可が正しくない場合、ユーザーはリモート Web アクセスを使用できません。 リモート Web アクセスを使用して、インターネットを参照しようとすると、エラー「HTTP Error 403.1 アクセス不可」に到達した可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-assign-read-and-script-permissions-to-the-remote-directory"></a>/Remote ディレクトリに対して読み取りとスクリプトのアクセス許可を割り当てるには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] で、サーバー名を展開し、**[サイト]** をクリックします。  
  
3.  **[既定の Web サイト]**、**[リモート]** の順に展開します。  
  
4.  **[機能ビュー]** で、**[ハンドラー マッピング]** をダブルクリックします。  
  
5.  **[操作]** ウィンドウで、**[機能のアクセス許可の編集]** をクリックします。  
  
6.  **[読み取り]** と **[スクリプト]** チェック ボックスをオンにし、**[OK]** をクリックします。  
  
### <a name="http-redirect-is-either-set-or-inherited-on-the-remote-virtual-directory"></a>HTTP リダイレクトが、/Remote 仮想ディレクトリに設定または継承されている  
 **問題点:** HTTP リダイレクト属性が、予期せず /Remote 仮想ディレクトリに設定または継承されています。  
  
 **影響:** HTTP リダイレクト属性が /Remote 仮想ディレクトリに設定されている場合、リモート Web ワークプレースの削除は正常に機能しません。  
  
 **解決方法:**  
  
##### <a name="to-remove-the-http-redirect-attribute"></a>HTTP リダイレクト属性を削除するには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] で、サーバー名を展開し、**[サイト]** をクリックします。  
  
3.  **[既定の Web サイト]**、**[リモート]** の順に展開します。  
  
4.  **[機能ビュー]** で **[HTTP リダイレクト]** をダブルクリックします。  
  
5.  **[この宛先に要求をリダイレクト]** チェック ボックスをオフにしてから、**[操作]** ウィンドウで **[適用]** をクリックします。  
  
### <a name="a-host-name-exists-for-port-80-on-the-default-website"></a>既定の Web サイトのポート 80 にホスト名が存在する  
 **問題点:** 既定の Web サイトのポート 80 にホスト名が割り当てられています。  
  
 **影響:** ポート 80、既定の web サイトにホスト名が割り当てられる場合は、Windows Server Essentials の一部の web アプリケーションに接続できない可能性がありますできません。 ホスト名は不要であり、このような状況ではお勧めしません。  
  
 **解決方法:**  
  
##### <a name="to-clear-the-host-name-entry-for-port-80-on-the-default-website"></a>既定の Web サイトのポート 80 にあるホスト名のエントリを消去するには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] で、サーバー名を展開し、**[サイト]** をクリックします。  
  
3.  **[機能] ビュー**で、**[既定の Web サイト]** を右クリックしてから、**[バインド]** をクリックします。  
  
4.  **[サイト バインド]** で、**[ポート 80 の http]** の設定を選択してから、**[編集]** をクリックします。  
  
5.  **[サイト バインドの編集]** で、**[ホスト名]** エントリを消去してから、**[OK]** をクリックします。  
  
### <a name="backup-does-not-succeed-because-of-a-hidden-partition"></a>隠れたパーティションのため、バックアップが成功しない  
 **問題点:** Windows Server バックアップによって、バックアップに NTFS 以外のパーティションがスケジュールされています。  
  
 **影響:** Windows Server バックアップは、NTFS でフォーマットされているパーティションのみをバックアップできます。  
  
 **解決方法:** Windows Server バックアップが NTFS 以外のパーティションをバックアップしないように構成してください。 詳細については、次を参照してください。[システム状態のバックアップは、Windows Server 2008 ベースのコンピューター (サポート技術情報の記事 968128) が失敗したときに、ログ記録イベント Id 12290 および 16387](https://support.microsoft.com/kb/968128) (https://support.microsoft.com/kb/968128)します。  
  
### <a name="the-most-recent-backup-did-not-succeed"></a>直近のバックアップが成功しなかった  
 **問題点:** 直近のバックアップが正常に完了しませんでした。  
  
 **影響:** システムのバックアップ状態が正しくありません。  
  
 **解決方法:** イベント ログおよびバックアップのログで、直近のバックアップ中に発生したエラーを確認します。  
  
### <a name="the-startup-type-for-the-file-replication-service-is-not-set-to-automatic"></a>ファイル レプリケーション サービスのスタートアップの種類が ”自動" に設定されていない  
 **問題点:** スタートアップの種類が既定値の "自動” に設定されていない場合、ファイル レプリケーション サービス (FRS) は開始されない可能性があります。  
  
 **影響:** ファイル レプリケーション サービスが実行されていない場合、ドメイン コントローラーは、サービスのアドバタイズを停止する可能性があります。 これにより、ログオン エラーやグループ ポリシー エラーなど、その他の問題につながる可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-file-replication-service-for-automatic-startup"></a>ファイル レプリケーション サービスが自動的に開始するように構成するには  
  
1.  [サービス] コンソールを開きます。  
  
2.  サービスの一覧で、**[ファイル レプリケーション]** をダブルクリックします。  
  
3.  **[スタートアップの種類]** で **[自動]** を選択し、**[適用]** をクリックします。  
  
### <a name="the-file-replication-service-is-not-running"></a>ファイル レプリケーション サービスが実行されていない  
 **問題点:** ファイル レプリケーション サービスが実行されていません。  
  
 **影響:** ファイル レプリケーション サービスが実行されていない場合、ドメイン コントローラーは、サービスのアドバタイズを停止する可能性があります。 この動作は、ログオン エラーやグループ ポリシー エラーなど、その他の問題につながる可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-file-replication-service"></a>ファイル レプリケーション サービスを開始するには  
  
1.  [サービス] コンソールを開きます。  
  
2.  サービスの一覧で、**[ファイル レプリケーション サービス]** をダブルクリックします。  
  
3.  **[開始]** をクリックします。  
  
### <a name="the-logon-account-for-the-file-replication-service-is-not-set-to-use-the-local-system-account"></a>ファイル レプリケーション サービスのログオン アカウントが、ローカル システム アカウントを使用するように設定されていない  
 **問題点:** ファイル レプリケーション サービスが、既定のログオン アカウントとしてローカル システム アカウントを使用するように構成されていません。  
  
 **影響:** ファイル レプリケーション サービスが既定のログオン アカウントとして ローカル システムを使用しない場合、アクセス許可に関連するエラーが発生する可能性があります。 これらのエラーは、他のエラーのトリガーとなり、最終的にドメイン コント ローラーがそのサービスのアドバタイズを停止する可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-local-system-as-the-default-logon-account-for-file-replication"></a>ファイル レプリケーションの既定のログオン アカウントとしてローカル システムを構成するには  
  
1.  [サービス] コンソールを開きます。  
  
2.  サービスの一覧で、**[ファイル レプリケーション]** をダブルクリックします。  
  
3.  **[サービスのプロパティ]** ページで、**[ログオン]** タブをクリックします。  
  
4.  **[ローカル システム アカウント]** オプションをクリックしてから、**[適用]** をクリックします。  
  
5.  サービスを再起動します。  
  
### <a name="the-startup-type-for-the-dfs-replication-service-is-not-set-to-automatic"></a>DFS レプリケーション サービスのスタートアップの種類が ”自動" に設定されていない  
 **問題点:** スタートアップの種類が既定値の "自動” に設定されていない場合、DFS レプリケーション サービスは開始しない可能性があります。  
  
 **影響:** DFS レプリケーション サービスが実行されていない場合、ドメイン コントローラーは、サービスのアドバタイズを停止する可能性があります。 これにより、ログオン エラーやグループ ポリシー エラーなど、その他の問題につながる可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-dfs-replication-service-for-automatic-startup"></a>DFS レプリケーション サービスが自動的に開始するように構成するには  
  
1.  [サービス] コンソールを開きます。  
  
2.  サービスの一覧で、**[DFS レプリケーション]** をダブルクリックします。  
  
3.  **[スタートアップの種類]** で **[自動]** を選択し、**[適用]** をクリックします。  
  
### <a name="the-dfs-replication-service-is-not-running"></a>DFS レプリケーション サービスが実行されていない  
 **問題点:** DFS レプリケーション サービスが現在実行されていません。  
  
 **影響:** DFS レプリケーション サービスが実行されていない場合、ドメイン コントローラーは、サービスのアドバタイズを停止する可能性があります。 この動作は、ログオン エラーやグループ ポリシー エラーなど、その他の問題につながる可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-start-the-dfs-replication-service"></a>DFS レプリケーション サービスを開始するには  
  
1.  [サービス] コンソールを開きます。  
  
2.  サービスの一覧で、**[DFS レプリケーション]** をダブルクリックします。  
  
3.  **[開始]** をクリックします。  
  
### <a name="the-dfs-replication-service-is-not-is-not-set-to-use-the-local-system-account"></a>DFS レプリケーション サービスがローカル システム アカウントを使用するように設定されていない  
 **問題点:** DFS レプリケーション サービスが、既定のログオン アカウントとしてローカル システム アカウントを使用するように設定されていません。  
  
 **影響:** DFS レプリケーション サービスが既定のログオン アカウントとして ローカル システムを使用しない場合、アクセス許可に関連するエラーが発生する可能性があります。 これらのエラーは、他のエラーのトリガーとなり、最終的にドメイン コント ローラーがそのサービスのアドバタイズを停止する可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-dfs-replication-to-use-local-system-as-the-default-logon-account"></a>DFS レプリケーションが既定のログオン アカウントとしてローカル システムを使用するように構成するには  
  
1.  [サービス] コンソールを開きます。  
  
2.  サービスの一覧で、**[DFS レプリケーション]** をダブルクリックします。  
  
3.  **[サービスのプロパティ]** ページで、**[ログオン]** タブをクリックします。  
  
4.  **[ローカル システム アカウント]** オプションをクリックしてから、**[適用]** をクリックします。  
  
5.  サービスを再起動します。  
  
### <a name="the-windows-server-office-365-integration-service-is-not-set-to-use-the-local-system-account"></a>Windows Server Office 365 統合サービスがローカル システム アカウントを使用するように設定されていない  
 **問題点:** Windows Server Office 365 統合サービスが、既定のアカウントとしてローカル システム アカウントを使用するように設定されていません。  
  
 **影響:** Windows Server Office 365 統合サービスが既定のアカウントとしてローカル システム アカウントを使用しない場合、Office 365 の一部の機能が正常に機能しない可能性があります。 また、アクセス許可に関連するエラーが発生する可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-office-365-integration-service-to-use-local-system-as-the-default-logon-account"></a>Office 365 統合サービスが既定のログオン アカウントとしてローカル システムを使用するように構成するには  
  
1.  [サービス] コンソールを開きます。  
  
2.  サービスの一覧で、**[Windows Server Office 365 統合サービス]** をダブルクリックします。  
  
3.  **[サービスのプロパティ]** ページで、**[ログオン]** タブをクリックします。  
  
4.  **[ローカル システム アカウント]** オプションをクリックしてから、**[適用]** をクリックします。  
  
5.  サービスを再起動します。  
  
### <a name="the-windows-server-office-365-integration-service-is-not-running"></a>Windows Server Office 365 統合サービスが実行されていない  
 **問題点:** Windows Server Office 365 統合サービスが現在実行されていません。  
  
 **影響:** Windows Server Office 365 統合サービスが実行されていない場合、Office 365 のクラウド ベースの機能は使用できません。  
  
 **解決方法:**  
  
##### <a name="to-start-the-windows-server-office-365-integration-service"></a>Windows Server Office 365 統合サービスを開始するには  
  
1.  [サービス] コンソールを開きます。  
  
2.  サービスの一覧で、**[Windows Server Office 365 統合サービス]** をダブルクリックします。  
  
3.  **[開始]** をクリックします。  
  
### <a name="the-startup-type-for-the-windows-server-office-365-integration-service-is-not-set-to-automatic"></a>Windows Server Office 365 統合サービスのスタートアップの種類が ”自動” に設定されていない  
 **問題点:** Windows Server Office 365 統合サービスのスタートアップの種類が、既定値の ”自動" に設定されていません。  
  
 **影響:** Windows Server Office 365 統合サービスが実行されていない場合、Office 365 のクラウド ベースの機能は使用できません。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-office-365-integration-service-for-automatic-startup"></a>Windows Server Office 365 統合サービスが自動的に開始するように構成するには  
  
1.  [サービス] コンソールを開きます。  
  
2.  サービスの一覧で、**[Windows Server Office 365 統合サービス]** をダブルクリックします。  
  
3.  **[スタートアップの種類]** で **[自動]** を選択し、**[適用]** をクリックします。  
  
### <a name="a-registry-value-is-missing-or-set-incorrectly"></a>レジストリの値が不足しているか、正しく設定されていない  
 **問題点:** HKEY_LOCAL_MACHINE \Software\Microsoft\Rpc\RpcProxy のレジストリ キーが正しくない値を含んでいるか、存在していません。  
  
 **影響:** RPCProxy のレジストリ キーが正しく設定されていない場合、次のようなエラー メッセージが表示される可能性があります。"リモート デスクトップ ゲートウェイ サーバーが一時的に使用不能であるため、ご使用のコンピューターはリモート コンピューターに接続できません。 後で再接続するか、ネットワーク管理者にお問い合わせください。"  
  
 **解決方法:**  
  
##### <a name="to-correct-the-registry-setting"></a>レジストリの設定を修正するには  
  
1.  レジストリ エディターを開きます。  
  
2.  次のレジストリ キーに移動します。  
  
     HKEY_LOCAL_MACHINE\Software\Microsoft\Rpc\RpcProxy  
  
3.  "Website"という名前の文字列が既定の Web サイトのデータ値を持つことを確認します。  
  
    -   データ値が正しくない場合は、適切な値を使用するように文字列を変更します。  
  
    -   文字列が存在しない場合、"Website"という名前の新しい文字列を作成および既定の Web サイトにデータ値を設定します。"  
  
### <a name="the-startup-type-for-the-block-level-backup-engine-service-is-not-set-to-manual"></a>ブロック レベルのバックアップ エンジン サービスのスタートアップの種類が ”手動" に設定されていない  
 **問題点:** ブロック レベルのバックアップ エンジン サービスで、既定のスタートアップの種類の ”手動" が使用されていません。  
  
 **影響:** ブロック レベルのバックアップ エンジン サービスは、スタートアップの種類が ”手動" に設定されていないと開始しない場合があります。 : この問題には、Windows Server バックアップ ジョブが失敗する可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-for-manual-startup"></a>ブロック レベルのバックアップ エンジン サービスで手動スタートアップを構成するには  
  
1.  [サービス] コンソールを開きます。  
  
2.  サービスの一覧で、**[ブロック レベルのバックアップ エンジン サービス]** をダブルクリックします。  
  
3.  **[スタートアップの種類]** で **[手動]** を選択し、**[適用]** をクリックします。  
  
### <a name="the-logon-account-for-the-block-level-backup-engine-service-is-not-set-to-use-the-local-system-account"></a>ブロック レベルのバックアップ エンジン サービスのログオン アカウントが、ローカル システム アカウントを使用するように設定されていない  
 **問題点:** ブロック レベルのバックアップ エンジン サービスが、既定のログオン アカウントとしてローカル システム アカウントを使用するように設定されていません。  
  
 **影響:** ブロック レベルのバックアップ エンジン サービスが既定のログオン アカウントとして ローカル システムを使用しない場合、アクセス許可に関連するエラーが発生する可能性があります。 これらのエラーにより、Windows Server バックアップのジョブが正常に完了しない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-to-use-local-system-as-the-default-logon-account"></a>ブロック レベルのバックアップ エンジン サービスが、既定のログオン アカウントとしてローカル システムを使用するように構成するには  
  
1.  [サービス] コンソールを開きます。  
  
2.  サービスの一覧で、**[ブロック レベルのバックアップ エンジン サービス]** をダブルクリックします。  
  
3.  **[サービスのプロパティ]** ページで、**[ログオン]** タブをクリックします。  
  
4.  **[ローカル システム アカウント]** オプションをクリックしてから、**[適用]** をクリックします。  
  
5.  サービスを再起動します。  
  
### <a name="the-common-name-on-the-certificate-that-is-bound-to-the-wss-certificate-web-service-website-does-not-match-the-server-name"></a>WSS Certificate Web Service Web サイトにバインドしている証明書の共通名がサーバー名と一致しない  
 **問題点:** IIS で、WSS Certificate Web Service Web サイトに有効でない証明書がバインドされています。 この証明書の共通名がサーバー名と一致しません。  
  
 **影響:** WSS Certificate Web Service Web サイトに有効でない証明書をバインドすると、[接続] ウィザードが正常に機能しない可能性があります。  
  
 **解決方法:**  
  
##### <a name="to-configure-a-valid-certificate-for-the-wss-certificate-web-service"></a>WSS Certificate Web Service に有効な証明書を構成するには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] で、サーバー名を展開し、**[サイト]** をクリックします。  
  
3.  **[WSS Certificate Web Service]** を右クリックしてから、**[バインドの編集]** をクリックします。  
  
4.  **[サイト バインド]** で、**[HTTPS]**、**[編集]** の順にクリックします。  
  
5.  **[サイト バインドの編集]** の **[SSL 証明書]** で、サーバーと同じ名前を持つ証明書を選択します。  
  
6.  サーバーと同じ名前を持つ証明書のエントリが複数ある場合は、**[表示]** をクリックして、どの証明書が有効かを判断し、適切な証明書を選択します。  
  
### <a name="there-appears-to-be-a-problem-with-the-certificate-binding-for-the-remote-desktop-gateway-service"></a>リモート デスクトップ ゲートウェイ サービスにバインドされている証明書に問題があるように見える  
 **問題点:** リモート デスクトップ ゲートウェイ サービスの証明書が正しくバインドされていないようです。  
  
 **影響:** リモート デスクトップ ゲートウェイ サービスの証明書が正しく構成されていない場合、ユーザーはリモート Web アクセスに接続できません。  
  
 **解決方法:**  
  
##### <a name="to-fix-the-binding-for-the-remote-desktop-gateway-service"></a>リモート デスクトップ ゲートウェイ サービスのバインドを修復するには  
  
-   管理者としてコマンド プロンプトを開き、次のコマンドを入力します。  
  
    ```  
    REG ADD HKLM\SYSTEM\CurrentControlSet\services\HTTP\Parameters\SslBindingInfo\0.0.0.0:443  /v DefaultFlags /t REG_DWORD /d 1 /f  
    net stop tsgateway  
    net start tsgateway  
    ```  
  
     詳細については、次を参照してください。 [Windows Server Essentials (サポート技術情報の記事 2472211) でリモート デスクトップ ゲートウェイ サービスを管理する方法](https://support.microsoft.com/kb/2472211)(https://support.microsoft.com/kb/2472211)します。
