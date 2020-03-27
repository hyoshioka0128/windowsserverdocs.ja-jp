---
title: Windows Server Essentials ベスト プラクティス アナライザー (BPA) ツールで使用される規則
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 37e1dae7-586c-4dd7-bf83-7e14a9567c8f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 5a737c777e1af25a59dc878fd0b3e99a6ee3ce24
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318799"
---
# <a name="rules-used-by-the-windows-server-essentials-best-practices-analyzer-bpa-tool"></a>Windows Server Essentials ベスト プラクティス アナライザー (BPA) ツールで使用される規則

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

この記事では、Windows Server Essentials ベストプラクティスアナライザー (BPA) で使用される規則について説明します。 BPA は、Windows Server Essentials を実行しているサーバーを調べ、問題を説明するレポートを表示して、問題を解決するための推奨事項を提示します。 推奨事項は、Windows Server Essentials の製品サポート組織によって開発されています。  
  
## <a name="using-the-tool"></a>ツールの使用  
 標準的な方法として、windows Server 2011 Essentials、Windows Small Business Server 2011 Essentials、または Windows Home Server 2011 から Windows Server Essentials に移行して、移行の完了後に移行先サーバーで BPA を実行することができます。設定とデータ。 ツールは、いつでもダッシュボードから実行できます。  
  
#### <a name="to-run-the--windows-server-essentials-bpa-on-the-server"></a>サーバーで Windows Server Essentials BPA を実行するには  
  
1.  サーバーに管理者としてログオンしてから、ダッシュボードを開きます。  
  
2.  ダッシュボードで **[デバイス]** タブをクリックします。  
  
3.  **[サーバー タスク]** ウィンドウで、 **[ベスト プラクティス アナライザー]** をクリックします。  
  
4.  BPA の各メッセージを確認し、必要な場合は指示に従って問題を解決します。  
  
## <a name="rules-used-by-the-best-practices-analyzer"></a>ベスト プラクティス アナライザーが使用する規則  
  
### <a name="disable-ip-filtering"></a>IP フィルタリングを無効にする  
 **問題:** 現在、サーバーでは IP フィルタリングが有効になっています。 IP フィルタリングを無効にする必要があります。  
  
 **影響:** IP フィルタリングが有効になっている場合、ネットワークトラフィックがブロックされる可能性があります。  
  
 **解決**  
  
##### <a name="to-disable-ip-filtering"></a>IP フィルタリングを無効にするには  
  
1.  サーバーで regedit.exe を開きます。  
  
2.  HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters に移動します。  
  
3.  **[EnableSecurityFilters]** を右クリックして、 **[修正]** をクリックします。  
  
4.  **[DWORD (32 ビット) 値の編集]** ウィンドウで、 **[値のデータ]** フィールドをゼロ (0) にしてから、 **[OK]** をクリックします。  
  
5.  変更を適用するには、サーバーを再起動します。  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-set-to-start-automatically-by-default"></a>分散トランザクション コーディネーター (MSDTC) サービスは、既定で自動的に開始するように設定する必要がある  
 **問題:** MSDTC サービスは自動的に開始するように構成されていません  
  
 **影響:** MSDTC サービスは、サーバーの起動時に自動的に開始されない場合があります。 このサービスが停止している場合、SQL または COM の機能の一部が正常に機能しない可能性があります。 結果として、Microsoft SQL Server または COM 機能を使用するアプリケーションが正しく機能しなくなる可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-the-msdtc-service-to-start-automatically"></a>MSDTC サービスが自動的に開始するように設定するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[分散トランザクション コーディネータ]** サービスを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、 **[スタートアップの種類]** を **[自動 (遅延開始)]** に変更し、 **[OK]** をクリックします。  
  
### <a name="the-netlogon-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように Netlogon サービスを構成する必要がある  
 **問題:** Netlogon サービスが自動的に開始するように構成されていません。  
  
 **影響:** サーバーの起動時に Netlogon サービスが自動的に開始しない場合があります。 このサービスが停止している場合、ユーザーおよびサービスがサーバーによって認証されない可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-the-netlogon-service-to-start-automatically"></a>Netlogon サービスが自動的に開始するように設定するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Netlogon]** サービスを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、 **[スタートアップの種類]** を **[自動]** に変更し、 **[OK]** をクリックします。  
  
### <a name="the-dns-client-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように DNS クライアント サービスを構成する必要がある  
 **問題:** DNS クライアントサービスが自動的に開始するように構成されていません。  
  
 **影響:** サーバーの起動時に、DNS クライアントサービスが自動的に開始しない場合があります。 このサービスが停止している場合、サーバーが DNS 名を解決できない可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-the-dns-client-service-to-start-automatically"></a>DNS クライアント サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DNS クライアント]** サービスを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、 **[スタートアップの種類]** を **[自動]** に変更し、 **[OK]** をクリックします。  
  
### <a name="the-dns-server-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように DNS サーバー サービスを構成する必要がある  
 **問題:** DNS サーバーサービスが自動的に開始するように構成されていません。  
  
 **影響:** サーバーの起動時に、DNS サーバーサービスが自動的に開始しないことがあります。 このサービスが停止している場合、DNS の更新が行われません。  
  
 **解決**  
  
##### <a name="to-configure-the-dns-server-service-to-start-automatically"></a>DNS サーバー サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DNS サーバー]** サービスを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、 **[スタートアップの種類]** を **[自動]** に変更し、 **[OK]** をクリックします。  
  
### <a name="active-directory-web-services-is-not-set-to-the-default-start-mode"></a>Active Directory Web サービスが既定の開始モードに設定されていない  
 **問題:** Active Directory Web サービスが、既定の開始モード 自動 (自動) に設定されていません。  
  
 **影響:** Active Directory Web サービス (ADWS) が、既定の開始モード [自動] に設定されていません。 サーバー上の ADWS が停止しているか、無効になっている場合、Windows PowerShell 用 Active Directory モジュールや Active Directory 管理センターなどのクライアント アプリケーションは、このサーバー上で実行されているディレクトリ サービス インスタンスにアクセスして、管理することができません。 詳細については、Windows Server テクニカルライブラリの「 [AD DS の新機能: Active Directory Web サービス](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx)」 (https://technet.microsoft.com/library/dd391908(WS.10).aspx) を参照してください。  
  
 **解決**  
  
##### <a name="to-configure-the-active-directory-web-services-service-to-start-automatically"></a>Active Directory Web サービスのサービスを自動的に開始するように設定するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Active Directory Web サービス]** サービスを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、 **[スタートアップの種類]** を **[自動]** に変更し、 **[OK]** をクリックします。  
  
### <a name="the-dhcp-client-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように DHCP クライアント サービスを構成する必要がある  
 **問題:** DHCP クライアントサービスが自動的に開始するように構成されていません。  
  
 **影響:** DHCP クライアントサービスは、サーバーの起動時に自動的に開始されません。 このサービスが停止している場合、クライアント コンピューターはサーバーから IP アドレスを受信できません。  
  
 **解決**  
  
##### <a name="to-configure-the-dhcp-client-service-to-start-automatically"></a>DHCP クライアント サービスが自動的に開始されるように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DHCP クライアント]** サービスを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、 **[スタートアップの種類]** を **[自動]** に変更し、 **[OK]** をクリックします。  
  
### <a name="the-iis-admin-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように IIS 管理サービスを構成する必要がある  
 **問題:** IIS 管理サービスが自動的に開始するように構成されていません。  
  
 **影響:** IIS 管理サービスは、サーバーの起動時に自動的に開始されません。 このサービスが停止している場合、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-the-iis-admin-service-to-start-automatically"></a>IIS 管理サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[IIS 管理サービス]** を右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、 **[スタートアップの種類]** を **[自動]** に変更し、 **[OK]** をクリックします。  
  
### <a name="the-world-wide-web-publishing-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように World Wide Web 発行サービスを構成する必要がある  
 **問題:** World Wide Web 発行サービスが自動的に開始するように構成されていません。  
  
 **影響:** サーバーの起動時に World Wide Web 発行サービスが自動的に開始しない場合があります。 このサービスが停止している場合、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-the-world-wide-web-publishing-service-to-start-automatically"></a>World Wide Web 発行サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[World Wide Web 発行サービス]** を右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、 **[スタートアップの種類]** を **[自動]** に変更し、 **[OK]** をクリックします。  
  
### <a name="the-remote-registry-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように リモート レジストリ サービスを構成する必要がある  
 **問題:** リモートレジストリサービスが自動的に開始するように構成されていません。  
  
 **影響**:  
  
 サーバーを起動したときにリモート レジストリ サービスが自動的に開始しない可能性があります。 このサービスが停止している場合、一部のネットワーク操作をリモートで実行できない可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-the-remote-registry-service-to-start-automatically"></a>リモート レジストリ サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[リモート レジストリ]** サービスを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、 **[スタートアップの種類]** を **[自動]** に変更し、 **[OK]** をクリックします。  
  
### <a name="the-remote-desktop-gateway-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように リモート デスクトップ ゲートウェイ サービスを構成する必要がある  
 **問題:** リモートデスクトップゲートウェイサービスは、自動的に開始するように構成されていません。  
  
 **影響:** このサービスが停止している場合、ユーザーはリモート Web アクセスを使用してコンピューターにアクセスできない可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-the-remote-desktop-gateway-service-to-start-automatically"></a>リモート デスクトップ ゲートウェイ サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[リモート デスクトップ ゲートウェイ]** を右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、 **[スタートアップの種類]** を **[自動 (遅延開始)]** に変更し、 **[OK]** をクリックします。  
  
### <a name="the-windows-time-service-should-be-configured-to-start-automatically-by-default"></a>既定で自動的に開始するように Windows タイム サービスを構成する必要がある  
 **問題:** Windows タイムサービスが自動的に開始するように構成されていません。  
  
 **影響:** このサービスが停止している場合、データと時間の同期は使用できません。  
  
 **解決**  
  
##### <a name="to-configure-the-windows-time-service-to-start-automatically"></a>Windows タイム サービスが自動的に開始するように構成するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Windows タイム]** サービスを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[全般]** タブで、 **[スタートアップの種類]** を **[自動]** に変更し、 **[OK]** をクリックします。  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-started"></a>分散トランザクション コーディネーター (MSDTC) サービスを開始する必要がある  
 **問題:** MSDTC サービスがサーバー上で実行されていません。  
  
 **影響:** このサービスが停止している場合は、一部の SQL Server または COM 関数が失敗する可能性があります。 結果として、Microsoft SQL Server または COM 機能を使用するアプリケーションが正しく機能しなくなる可能性があります。  
  
 **解決**  
  
##### <a name="to-start-the-distributed-transaction-coordinator-service"></a>分散トランザクション コーディネーター サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[分散トランザクション コーディネーター]** サービスを右クリックしてから、 **[開始]** をクリックします。  
  
### <a name="the-netlogon-service-should-be-started"></a>Netlogon サービスを開始する必要がある  
 **問題:** Netlogon サービスがサーバー上で実行されていません。  
  
 **影響:** このサービスが開始されていない場合、サーバーはユーザーとサービスを認証しない可能性があります。  
  
 **解決**  
  
##### <a name="to-start-the-netlogon-service"></a>Netlogon サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Netlogon]** サービスを右クリックしてから、 **[開始]** をクリックします。  
  
### <a name="the-dns-client-service-should-be-started"></a>DNS クライアント サービスを開始する必要がある  
 **問題:** DNS クライアントサービスがサーバー上で実行されていません。  
  
 **影響:** このサービスが開始されていない場合、サーバーは DNS 名を解決できない可能性があります。  
  
 **解決**  
  
##### <a name="to-start-the-dns-client-service"></a>DNS クライアント サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DNS クライアント]** サービスを右クリックしてから、 **[開始]** をクリックします。  
  
### <a name="the-dns-server-service-should-be-started"></a>DNS サーバー サービスを開始する必要がある  
 **問題:** DNS サーバーサービスがサーバー上で実行されていません。  
  
 **影響:** DNS サーバーサービスが開始されていない場合、DNS の更新が行われない可能性があります。  
  
 **解決**  
  
##### <a name="to-start-the-dns-server-service"></a>DNS サーバー サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DNS サーバー]** サービスを右クリックしてから、 **[開始]** をクリックします。  
  
### <a name="active-directory-web-services-is-not-started"></a>Active Directory Web サービスが開始していない  
 **問題:** Active Directory Web サービスが開始されていません。  
  
 **影響:** Active Directory Web サービス (ADWS) が開始されていません。 サーバー上の ADWS が停止しているか、無効になっている場合、Windows PowerShell 用 Active Directory モジュールや Active Directory 管理センターなどのクライアント アプリケーションは、このサーバー上で実行されているディレクトリ サービス インスタンスにアクセスして、管理することができません。 詳細については、Windows Server テクニカルライブラリの「 [AD DS の新機能: Active Directory Web サービス](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx)」 (https://technet.microsoft.com/library/dd391908(WS.10).aspx) を参照してください。  
  
 **解決**  
  
##### <a name="to-start-the-active-directory-web-services-service"></a>Active Directory Web サービスのサービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Active Directory Web サービス]** を右クリックし、 **[開始]** をクリックします。  
  
### <a name="the-dhcp-client-service-should-be-started"></a>DHCP クライアント サービスを開始する必要がある  
 **問題:** DHCP クライアントサービスがサーバー上で実行されていません。  
  
 **影響:** このサービスが停止している場合、クライアントコンピューターはサーバーから IP アドレスを受け取ることができません。  
  
 **解決**  
  
##### <a name="to-start-the-dhcp-client-service"></a>DHCP クライアント サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DHCP クライアント]** サービスを右クリックしてから、 **[開始]** をクリックします。  
  
### <a name="the-iis-admin-service-should-be-started"></a>IIS 管理サービスを開始する必要がある  
 **問題:** サーバーで IIS 管理サービスが実行されていません。  
  
 **影響:** このサービスが停止している場合は、リモート Web アクセスなど、サーバーで実行されている web サイトにアクセスできない可能性があります。  
  
 **解決**  
  
##### <a name="to-start-the-iis-admin-service"></a>IIS 管理サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[IIS 管理サービス]** を右クリックしてから、 **[開始]** をクリックします。  
  
### <a name="the-world-wide-web-publishing-service-should-be-started"></a>World Wide Web 発行サービスを開始する必要がある  
 **問題:** World Wide Web 公開サービスがサーバーで実行されていません。  
  
 **影響:** このサービスが停止している場合は、リモート Web アクセスなど、サーバーで実行されている web サイトにアクセスできない可能性があります。  
  
 **解決**  
  
##### <a name="to-start-the-world-wide-web-publishing-service"></a>World Wide Web 発行サービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[World Wide Web 発行サービス]** を右クリックしてから、 **[開始]** をクリックします。  
  
### <a name="the-remote-desktop-gateway-service-should-be-started"></a>リモート デスクトップ ゲートウェイ サービスを開始する必要がある  
 **問題:** リモートデスクトップゲートウェイサービスがサーバー上で実行されていません。  
  
 **影響:** このサービスが停止している場合、ユーザーはリモート Web アクセスを使用してコンピューターにアクセスできない可能性があります。  
  
 **解決**  
  
##### <a name="to-start-the-remote-desktop-gateway-service"></a>リモートデスクトップゲートウェイサービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[リモート デスクトップ ゲートウェイ]** サービスを右クリックしてから、 **[開始]** をクリックします。  
  
### <a name="the-windows-time-service-should-be-started"></a>Windows タイム サービスを開始する必要がある  
 **問題:** Windows タイムサービスがサーバー上で実行されていません。  
  
 **影響:** このサービスが停止している場合、データと時間の同期は使用できません。  
  
 **解決**  
  
##### <a name="to-start-the-windows-time-service"></a>Windows タイムサービスを開始するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Windows タイム]** サービスを右クリックしてから、 **[開始]** をクリックします。  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-logon-account-should-be-nt-authoritynetwork-service"></a>分散トランザクション コーディネーター (MSDTC) サービスのログオン アカウントは NT AUTHORITY\Network Service とする必要がある  
 **問題:** 分散トランザクションコーディネーター (MSDTC) サービスの既定のログオンアカウントが変更されます。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 その結果、SQL Server または COM 関数を使用するアプリケーションが正常に動作しないことがあります。  
  
 **解決**  
  
##### <a name="to-change-the-logon-account-for-the-service"></a>サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[分散トランザクション コーディネータ]** サービスを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[このアカウント]** をクリックし、「**NT AUTHORITY\Network Service**」と入力してから、 **[OK]** をクリックします。  
  
### <a name="the-netlogon-service-should-use-the-local-system-account-as-its-logon-account"></a>Netlogon サービスはローカル システム アカウントをログオン アカウントとして使用する必要がある  
 **問題:** Netlogon サービスの既定のログオンアカウントが変更されます。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、ユーザーおよびサービスがサーバーによって認証されない可能性があります。  
  
 **解決**  
  
##### <a name="to-change-the-netlogon-service-logon-account"></a>Netlogon サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Netlogon]** サービスを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[ローカル システム アカウント]** をクリックします。  
  
### <a name="the-dns-client-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>DNS クライアント サービスでは、ログオン アカウントとして NT AUTHORITY\Network Service アカウントを使用する必要がある  
 **問題:** DNS クライアントサービスの既定のログオンアカウントが変更されます。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、サーバーが DNS の名前を解決できない可能性があります。  
  
 **解決**  
  
##### <a name="to-change-the-dns-client-service-logon-account"></a>DNS クライアント サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DNS クライアント]** サービスを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[このアカウント]** をクリックしてから、「**NT AUTHORITY\Network Service**」と入力します。  
  
### <a name="the-dns-server-service-should-use-the-local-system-account-as-its-logon-account"></a>DNS サーバーサービスは、ログオンアカウントとしてローカルシステムアカウントを使用する必要があります。  
 **問題:** DNS サーバーサービスの既定のログオンアカウントが変更されます。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、DNS の更新が行われない可能性があります。  
  
 **解決**  
  
##### <a name="to-change-the-dns-server-service-logon-account"></a>DNS サーバー サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DNS サーバー]** サービスを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[ローカル システム アカウント]** をクリックします。  
  
### <a name="active-directory-web-services-is-not-the-default-logon-account"></a>Active Directory Web サービスは既定のログオン アカウントではない  
 **問題:** Active Directory Web サービスは、既定のログオンアカウントではありません。 既定では、ログオン アカウントは ”**ローカル システム アカウント**" に設定されています。  
  
 **影響:** Active Directory Web サービス (ADWS) が開始されていません。 サーバー上の ADWS が停止しているか、無効になっている場合、Windows PowerShell 用 Active Directory モジュールや Active Directory 管理センターなどのクライアント アプリケーションは、このサーバー上で実行されているディレクトリ サービス インスタンスにアクセスして、管理することができません。 詳細については、Windows Server テクニカルライブラリの「 [AD DS の新機能: Active Directory Web サービス](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx)」 (https://technet.microsoft.com/library/dd391908(WS.10).aspx) を参照してください。  
  
 **解決**  
  
##### <a name="to-change-the-active-directory-web-services-logon-account"></a>Active Directory Web サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Active Directory Web サービス]** を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[スタートアップの種類]** を **[自動]** に変更し、 **[OK]** をクリックします。  
  
4.  [Active Directory Web サービス] の **[プロパティ]** にある **[ログオン]** タブをクリックします。  
  
5.  **[ローカル システム アカウント]** オプションをクリックしてから、 **[OK]** をクリックします。  
  
### <a name="the-windows-update-service-should-use-the-local-system-account-as-its-logon-account"></a>Windows Update サービスはローカル システム アカウントをログオン アカウントとして使用する必要がある  
 **問題:** 自動更新サービスの既定のログオンアカウントが変更されます。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、サーバーは自動更新を受信しない可能性があります。  
  
 **解決**  
  
##### <a name="to-change-the-windows-update-service-logon-account"></a>Windows Update サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Windows Update]** サービスを右クリックしてから、[プロパティ] をクリックします。  
  
3.  **[ログオン]** タブで **[ローカル システム アカウント]** をクリックします。  
  
### <a name="the-dhcp-client-service-should-use-the-nt-authoritylocalservice-account-as-its-logon-account"></a>DHCP クライアント サービスでは、ログオン アカウントとして NT AUTHORITY\LocalService アカウントを使用する必要がある  
 **問題:** DHCP クライアントサービスの既定のログオンアカウントが変更されます。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、クライアント コンピューターは、サーバーから IP アドレスを受信しません。  
  
 **解決**  
  
##### <a name="to-change-the-dhcp-client-service-logon-account"></a>DHCP クライアント サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[DHCP クライアント]** サービスを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[このアカウント]** をクリックしてから、「**NT AUTHORITY\LocalService**」と入力します。  
  
### <a name="the-iis-admin-service-should-use-the-local-system-account-as-its-logon-account"></a>IIS 管理サービスはローカル システム アカウントをログオン アカウントとして使用する必要がある  
 **問題:** IIS 管理サービスの既定のログオンアカウントが変更されます。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決**  
  
##### <a name="to-change-the-service-logon-account"></a>サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[IIS 管理サービス]** を右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[ローカル システム アカウント]** をクリックします。  
  
### <a name="the-world-wide-web-publishing-service-should-use-the-local-system-account-as-its-logon-account"></a>World Wide Web 発行サービスはローカル システム アカウントをログオン アカウントとして使用する必要がある  
 **問題:** World Wide Web 公開サービスの既定のログオンアカウントが変更されています。  
  
 **影響:** サービスに、想定どおりに動作するために必要なアクセス許可がない可能性があります。 結果として、リモート Web アクセスなど、サーバーで実行されている Web サイトにアクセスできない可能性があります。  
  
 **解決**  
  
##### <a name="to-change-the-world-wide-web-publishing-service-logon-account"></a>World Wide Web 発行サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[World Wide Web 発行サービス]** を右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[ローカル システム アカウント]** をクリックします。  
  
### <a name="the-remote-desktop-gateway-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>リモート デスクトップ ゲートウェイ サービスでは、ログオン アカウントとして NT AUTHORITY\Network Service アカウントを使用する必要がある  
 **問題:** リモートデスクトップゲートウェイサービスの既定のログオンアカウントが変更されます。  
  
 **影響:** サービスに、想定どおりに動作するための適切なアクセス許可がない可能性があります。 結果として、ユーザーは、リモート Web アクセスを使用してコンピューターにアクセスできない可能性があります。  
  
 **解決**  
  
##### <a name="to-change-the-remote-desktop-gateway-service-logon-account"></a>リモート デスクトップ ゲートウェイ サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[リモート デスクトップ ゲートウェイ]** を右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[このアカウント]** をクリックしてから、「**NT AUTHORITY\Network Service**」と入力します。  
  
### <a name="the-windows-time-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>Windows タイム サービスでは、ログオン アカウントとして NT AUTHORITY\Network Service アカウントを使用する必要がある  
 **問題:** Windows タイムサービスの既定のログオンアカウントが変更されます。  
  
 **影響:** サービスに、想定どおりに動作するための適切なアクセス許可がない可能性があります。 結果として、日付と時刻の同期が使用できない可能性があります。  
  
 **解決**  
  
##### <a name="to-change-the-windows-time-service-logon-account"></a>Windows タイム サービスのログオン アカウントを変更するには  
  
1.  サーバーで services.msc を開きます。  
  
2.  **[Windows タイム]** サービスを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[ログオン]** タブで **[このアカウント]** をクリックしてから、「**NT AUTHORITY\LocalService**」と入力します。  
  
### <a name="the-built-in-administrators-group-does-not-have-the-right-to-log-on-as-batch-job"></a>ビルトイン Administrators グループに、バッチ ジョブとしてログオンする権限がない  
 **問題:** 組み込みの Administrators グループには、batch ジョブとしてログオンする権限がありません。  
  
 **影響:** 管理者がアラートを作成し、管理者がログオンしていないときに実行するようにアラートを構成した場合、アラートはエラーコード2147943785で失敗します。  
  
 **解決策:** 組み込みの Administrators グループにバッチジョブとしてログオンする権限を付与する方法については、「[ビルトイン Administrator グループにバッチジョブとしてログオンする権利を付与](https://technet.microsoft.com/library/jj635076)する (https://technet.microsoft.com/library/jj635076)」を参照してください。  
  
### <a name="the-windows-firewall-is-turned-off"></a>Windows ファイアウォールが無効になっている  
 **問題:** Windows ファイアウォールがオフになっています。 既定値は有効です。  
  
 **影響:** ファイアウォールの設定によっては、Windows ファイアウォールは、一部の情報がサーバーを通過するのをブロックすることで、サーバーとネットワークを悪意のあるアクティビティから保護するのに役立ちます。  
  
 **解決**  
  
##### <a name="to-turn-on-windows-firewall-on-the-server"></a>サーバーで Windows ファイアウォールを有効にするには  
  
1.  サーバーの [コントロール パネル] を開きます。  
  
2.  [コントロール パネル] で、 **[システムとセキュリティ]** 、 **[Windows ファイアウォール]** の順にクリックします。  
  
3.  [Windows ファイアウォール] で、 **[Windows ファイアウォールを有効または無効にする]** をクリックします。 **[Windows ファイアウォールを有効にする]** オプションを選択してから、 **[OK]** をクリックします。  
  
### <a name="the-internal-network-adapter-is-not-configured-to-register-ip-address-in-dns"></a>内部ネットワーク アダプターが、IP アドレスを DNS に登録するように構成されていない  
 **問題:** 内部ネットワークアダプターが、IP アドレスを DNS に登録するように構成されていません。  
  
 **影響:** 内部ネットワークアダプターの IP アドレスが DNS に登録されていない場合、サーバーのコンピューター名を使用してサーバーにアクセスできない可能性があります。  
  
 **解決策:** 内部ネットワークアダプターが DNS に登録するように構成されていることを確認します。  
  
### <a name="dns-the-values-for-the-dns-forwardingtimeout-and-recursiontimeout-registry-key-are-identical"></a>DNS: DNS のレジストリ キー ForwardingTimeout および RecursionTimeout の値が同一である  
 **問題:** DNS ForwardingTimeout レジストリキーの値は、RecursionTimeout レジストリキーの値と同じにすることはできません。  
  
 **影響:** 名前でインターネットリソースにアクセスできない可能性があります。  
  
 **解決策:** RecursionTimeout レジストリキーの値を、レジストリの ForwardingTimeout キーの値よりも大きい値に設定します HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\DNS\Parameters.  
  
### <a name="the-forward-dns-zone-for-your-active-directory-domain-does-not-allow-secure-updates"></a>Active Directory ドメインの前方 DNS ゾーンで、セキュリティで保護された更新が許可されていない  
 **問題:** 前方参照ゾーンは、セキュリティで保護された動的更新のみを許可するように構成する必要があります。  
  
 **影響:** セキュリティで保護された動的更新を有効にすると、承認されたユーザーとホストのみがレコードに変更を加えることができます。  
  
 **解決**  
  
##### <a name="to-configure-the-forward-lookup-zone-for-your-active-directory-domain"></a>Active Directory ドメインの前方参照ゾーンを構成するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  Active Directory ドメインの前方参照ゾーンを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[動的更新]** ドロップダウン リストで、 **[セキュリティ保護のみ]** 、 **[OK]** の順にクリックします。  
  
### <a name="the-forward-dns-zone-does-not-allow-secure-updates"></a>セキュリティで保護された更新が、前方 DNS ゾーンで許可されない  
 **問題:** セキュリティで保護された動的更新のみを許可するように、_msdcs. * ゾーンの前方参照ゾーンを構成する必要があります。  
  
 **影響:** セキュリティで保護された動的更新を有効にすると、承認されたユーザーとホストのみが、msdcs. * ゾーンのレコードに変更を加えることができます。  
  
 **解決**  
  
##### <a name="to-allow-secure-updates-in-the-_msdcs-zone"></a>_msdcs ゾーンでセキュリティで保護された更新を許可するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  _msdcs ゾーンの [前方参照ゾーン] を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[動的更新]** ドロップダウン リストで、 **[セキュリティ保護のみ]** 、 **[OK]** の順にクリックします。  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Internet Explorer セキュリティ強化の構成が無効になっている  
 **問題:** Internet Explorer セキュリティ強化の構成 (IE ESC) は、現在、管理者グループに対して有効になっていません。  
  
 **影響:** Internet Explorer のセキュリティ強化の構成が管理者グループに対して有効になっていない場合、サーバーと Internet Explorer は Web コンテンツおよびアプリケーションスクリプトを介して発生する可能性がある悪意のある攻撃にさらされます。  
  
 **解決**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>Internet Explorer セキュリティ強化の構成を有効にするには  
  
1.  サーバーで **[サーバー マネージャー]** を開き、 **[ローカル サーバー]** をクリックします。  
  
2.  **[プロパティ]** ウィンドウで、 **[IE セキュリティ強化の構成]** の設定を **[有効]** にしてから、 **[OK]** をクリックします。  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Internet Explorer セキュリティ強化の構成が無効になっている  
 **問題:** Internet Explorer セキュリティ強化の構成 (IE ESC) は、現在、ユーザーグループに対して有効になっていません。  
  
 **影響:** Internet Explorer セキュリティ強化の構成が Users グループに対して有効になっていない場合、サーバーと Internet Explorer は Web コンテンツおよびアプリケーションスクリプトを介して発生する可能性がある悪意のある攻撃にさらされる可能性が高くなります。  
  
 **解決**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>Internet Explorer セキュリティ強化の構成を有効にするには  
  
1.  **[サーバー マネージャー]** を開いて、 **[ローカル サーバー]** をクリックします。  
  
2.  **[プロパティ]** ウィンドウで、 **[IE セキュリティ強化の構成]** の設定を **[有効]** にしてから、 **[OK]** をクリックします。  
  
### <a name="the-source-server-remains-in-active-directory-sites-and-services"></a>移行元サーバーが Active Directory サイトとサービスに残っている  
 **問題:** Windows Small Business Server を実行している移行元サーバーは、既定のファーストサイト名の Active Directory サイトとサービスにまだ存在しています。  
  
 **影響:** 移行元サーバーが Active Director サイトおよびサービスに残っている場合、クライアントコンピューターで接続の問題が発生する可能性があります。  
  
 **解決策:** 移行元サーバーを降格して、ドメインから削除した後、Active Directory のサイトとサービスおよび Active Directory ユーザーとコンピューター から移行元サーバーを削除する必要があります。  
  
### <a name="source-server-remains-in-sbscomputer-ou"></a>移行元サーバーが SBSComputer OU に残っている  
 **問題:** Windows Small Business Server を実行している移行元サーバーは、Active Directory ユーザーとコンピューターにまだ存在しています。  
  
 **影響:** 移行元サーバーが Active Director ユーザーとコンピューターに残っている場合、クライアントコンピューターで接続の問題が発生する可能性があります。  
  
 **解決策:** 移行元サーバーを降格して、ドメインから削除した後、Active Directory のサイトとサービスおよび Active Directory ユーザーとコンピューター から移行元サーバーを削除する必要があります。  
  
### <a name="a-group-policy-is-missing"></a>グループ ポリシーが見つからない  
 **問題:** 既定のドメインポリシーグループポリシーがありません。  
  
 **影響:** ドメインの適切な機能を使用するには、既定のドメインポリシーが必要です。  
  
 **解決**  
  
##### <a name="to-restore-a-missing-group-policy"></a>不足しているグループ ポリシーを復元するには  
  
1.  サーバーで gpmc.msc を開きます。  
  
2.  [グループ ポリシー マネージャー] で、ドメイン フォレストを展開し、**既定のドメイン ポリシー**のグループ ポリシー オブジェクトのコンソール ツリーを検索します。  
  
3.  ツリーにポリシーが表示されない場合は、システム状態のバックアップから復元します。  
  
### <a name="no-dns-name-server-resource-records"></a>DNS ネーム サーバー リソース レコードがない  
 **問題:** サーバーの前方参照ゾーンに DNS ネームサーバー (NS) リソースレコードがありません。  
  
 **影響:** Active Directory ドメインの前方参照ゾーンに DNS ネームサーバー (NS) リソースレコードが存在しない場合、ユーザーはネットワークまたはインターネット上のリソースにアクセスできない可能性があります。  
  
 **解決**  
  
##### <a name="to-restore-missing-dns-name-server-resource-records"></a>DNS ネーム サーバー リソース レコードを復元するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  DNS マネージャーで、Active Directory ドメインの前方参照ゾーンを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[ネーム サーバー]** タブで、設定が正しいことを確認します。  
  
4.  必要な変更を行ってから、 **[OK]** をクリックして設定を保存します。  
  
### <a name="no-dns-name-server-records"></a>DNS ネーム サーバー レコードがない  
 **問題:** サーバーの _msdcs ゾーンに DNS ネームサーバー (NS) リソースレコードがありません (例: _msdcs. contoso. local)。  
  
 **影響:** Active Directory ドメインの _msdcs ゾーンに DNS ネームサーバー (NS) リソースレコードが存在しない場合、ユーザーはネットワークまたはインターネット上のリソースにアクセスできない可能性があります。  
  
 **解決**  
  
##### <a name="to-restore-missing-dns-name-server-records"></a>DNS ネーム サーバー レコードを復元するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  [DNS マネージャー] で、_msdcs ゾーンの [前方参照ゾーン] を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[ネーム サーバー]** タブで、設定が正しいことを確認します。  
  
4.  必要な変更を行ってから、 **[OK]** をクリックして設定を保存します。  
  
### <a name="no-dns-name-server-records"></a>DNS ネーム サーバー レコードがない  
 **問題:** 委任された _msdcs 前方参照ゾーンに DNS ネームサーバー (NS) リソースレコードがありません。  
  
 **影響:** 委任された _msdcs 前方参照ゾーンに DNS ネームサーバー (NS) リソースレコードが存在しない場合、DNS サーバーサービスはドメインの DNS リソースレコードを解決できず、開始に失敗します。  
  
 **解決**  
  
##### <a name="to-reconfigure-missing-dns-name-server-records"></a>不足している DNS ネーム サーバー レコードを再構成するには  
  
1.  サーバーで dnsmgmt.msc を開きます。  
  
2.  [DNS マネージャー] で、サーバー名を展開し、 **[前方参照ゾーン]** を展開します。  
  
3.  Active Directory ドメインの前方参照ゾーン (例: contoso.local) をクリックします。  
  
4.  委任された _msdcs ゾーンが灰色のフォルダーとして表示されます。 _msdcs ゾーンを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[ネーム サーバー]** タブで、設定が正しいことを確認します。  
  
6.  必要な変更を行ってから、 **[OK]** をクリックして設定を保存します。  
  
### <a name="authenticated-users-not-a-member-of-the-pre-windows-2000-compatible-access-group"></a>認証されたユーザーは、Pre-Windows 2000 Compatible Access グループのメンバーではない  
 **問題:** Authenticated Users グループは、Windows 2000 以前の互換性のあるアクセスグループのメンバーではありません。  
  
 **影響:** 組み込みの Authenticated Users グループが Windows 2000 より前の互換性のあるアクセスグループのメンバーでない場合、ネットワークユーザーに "アクセスが拒否されました" というエラーが発生する可能性があります。  
  
 **解決**  
  
##### <a name="to-add-authenticated-users-to-the-pre-windows-2000-compatible-access-group"></a>認証されたユーザーを Pre-Windows 2000 Compatible Access グループのメンバーに追加するには  
  
1.  サーバーで dsa.msc を開きます。  
  
2.  **Builtin** フォルダーで、 **[Pre-Windows 2000 Compatible Access]** を右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  **[追加]** をクリックし、「**Authenticated Users**」と入力してから、 **[OK]** を 2 回クリックします。  
  
### <a name="dns-client-not-configured"></a>DNS クライアントが構成されていない  
 **問題:** DNS クライアントが、サーバーの内部 IP アドレスのみを指すように構成されていません。  
  
 **影響:** DNS クライアントが、サーバーの内部 IP アドレスのみを指すように構成されていない場合、DNS 名前解決が失敗する可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-dns-to-point-only-to-the-server-s-internal-ip-address"></a>サーバーの内部 IP アドレスのみを指すように DNS を構成するには  
  
1.  クライアント コンピューターから、ネットワーク接続の **[プロパティ]** ページを開きます。  
  
2.  DNS がサーバーの内部 IP アドレスのみを指定するように構成されていることを確認します。  
  
### <a name="default-application-pool-value-changed"></a>既定のアプリケーション プールの値が変更されている  
 **問題:** DefaultAppPool アプリケーションプールのワーカープロセスの最大数が、既定値の1に設定されていません。  
  
 **影響:** ユーザーは、Windows Small Business Server web ベースのサービスに接続できない可能性があります。  
  
 **解決**  
  
##### <a name="to-reset-maximum-worker-processes-for-the-default-application-pool"></a>既定のアプリケーション プールのワーカー プロセスの最大数をリセットするには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、 **[アプリケーション プール]** をクリックします。  
  
3.  **[アプリケーション プール]** で、 **[DefaultAppPool]** を右クリックし、 **[詳細設定]** をクリックします。  
  
4.  **[詳細設定]** で、 **[ワーカー プロセスの最大数]** の値を 1 に変更してから、 **[OK]** をクリックします。  
  
5.  **[詳細設定]** を閉じ、 **[DefaultAppPool]** を右クリックしてから、アプリケーション プールを停止して再開します。  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-account"></a>リモート Web アクセス用のアプリケーション プールが既定のアカウントを使用していない  
 **問題:** RemoteAppPool アプリケーションプールが既定のアカウントで実行されていません。  
  
 **影響:** ネットワークユーザーがリモート Web アクセス web サイトにアクセスできない可能性があります。  
  
 **解決**  
  
##### <a name="to-reset-the-remote-application-pool-to-use-the-default-account"></a>既定のアカウントを使用するためにリモート アプリケーション プールをリセットするには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、 **[アプリケーション プール]** をクリックします。  
  
3.  **[アプリケーション プール]** で、 **[RemoteAppPool]** を右クリックしてから、 **[詳細設定]** をクリックします。  
  
4.  **[詳細設定]** で、 **[ID]** を**NetworkService** に変更してから、 **[OK]** をクリックします。  
  
5.  **[詳細設定]** を閉じ、 **[RemoteAppPool]** を右クリックしてから、アプリケーション プールを停止して再開します。  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-net-framework-version"></a>リモート Web アクセス用のアプリケーション プールが既定の .NET Framework バージョンを使用していない  
 **問題:** RemoteAppPool アプリケーションプールが、既定のバージョンの Microsoft .NET Framework で実行されていません。  
  
 **影響:** ネットワークユーザーがリモート Web アクセス web サイトにアクセスできない可能性があります。  
  
 **解決**  
  
##### <a name="to-change-the-net-framework-version-used-by-the-remoteapppool"></a>RemoteAppPool で使用される .NET Framework のバージョンを変更するには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  IIS マネージャーで、サーバー名を展開し、 **[アプリケーション プール]** をクリックします。  
  
3.  **[アプリケーション プール]** で、 **[RemoteAppPool]** を右クリックしてから、 **[詳細設定]** をクリックします。  
  
4.  **[詳細設定]** で、 **[.NET Framework バージョン]** を v4.0 に変更してから、 **[OK]** をクリックします。  
  
5.  **[詳細設定]** を閉じ、 **[RemoteAppPool]** を右クリックしてから、アプリケーション プールを停止して再開します。  
  
### <a name="the-remoteaccesslog-file-is-larger-than-1-gb-in-size"></a>RemoteAccess.log ファイルのサイズが 1 GB より大きい  
 **問題:** Remoteaccess .log ファイルのサイズが 1 GB を超えると、システムドライブ上のディスク領域不足のエラーが発生する可能性があります。  
  
 **影響:** Remoteaccess .log ファイルが大きすぎると、ドライブ c: ドライブの空き領域に問題が発生する可能性があります。  
  
 **解決策:** サーバーをバックアップした後は、%ProgramData%\Microsoft\Windows Server\Logs\WebApps フォルダーにある Remoteaccess .log ファイルを削除できます。  
  
### <a name="default-web-sites-log-directory-is-over-1-gb-in-size"></a>既定の Web サイトのログ ディレクトリのサイズが 1 GB を超える  
 **問題:** 既定の web サイトのログフォルダーのサイズが 1 GB を超えると、システムドライブのディスク領域の不足エラーが発生する可能性があります。  
  
 **影響:** 既定の web サイトのログフォルダーが大きすぎる場合は、空き領域の問題が発生する可能性があります。 s ドライブ C:  
  
 **解決策:** サーバーをバックアップした後、既定の web サイトが停止している間は、C:\inetpub\logs\LogFiles\W3SVC1 フォルダー内のログファイルを削除できます。 その後、既定の Web サイトを開始します。  
  
### <a name="no-binding-for-ssl-on-all-ip-addresses"></a>すべての IP アドレスに SSL のバインドがない  
 **問題:** サーバー上のすべての IP アドレスに Secure Sockets Layer (SSL) のバインドがありません。  
  
 **影響:** SSL がサーバー上のすべての IP アドレスにバインドされていない場合、一部の web サイトはユーザーに提供されません。  
  
 **解決**  
  
##### <a name="to-bind-ssl-to-all-ip-addresses-on-the-server"></a>サーバー上のすべての IP アドレスに SSL をバインドするには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] の **[接続]** ウィンドウで、サーバー、 **[サイト]** の順に展開し、 **[既定の Web サイト]** を右クリックしてから、 **[バインドの編集]** をクリックします。  
  
3.  **[サイトのバインド]** で、 **[追加]** をクリックしてから、次の設定を選択します。  
  
    -   **Https** = **入力**  
  
    -   **IP アドレス** = **未割り当て**  
  
    -   **[ポート]** = 443  
  
4.  SSL 証明書を選択し、 **[OK]** をクリックして変更を保存します。  
  
### <a name="no-binding-for-ssl-on-the-default-web-site"></a>既定の Web サイトに SSL のバインドがない  
 **問題:** 既定の web サイトに SSL のバインドがありません。  
  
 **影響:** SSL が既定の web サイトにバインドされていない場合は、一部の web サイトがユーザーに提供されない可能性があります。  
  
 **解決**  
  
##### <a name="to-bind-ssl-to-the-default-website"></a>既定の Web サイトに SSL をバインドするには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] の **[接続]** ウィンドウで、サーバー、 **[サイト]** の順に展開し、 **[既定の Web サイト]** を右クリックしてから、 **[バインドの編集]** をクリックします。  
  
3.  **[サイトのバインド]** で、 **[追加]** をクリックしてから、次のオプションを選択します。  
  
    -   **Https** = **入力**  
  
    -   **IP アドレス** = **未割り当て**  
  
    -   **[ポート]** = 443  
  
    > [!NOTE]
    >  特定の IP アドレスにポート 443 の HTTPS バインドが存在する場合は、そのバインドの **[IP アドレス]** 属性を**未使用の IP アドレスすべて**に変更します。 この場合の例外は IP アドレス 127.0.0.1 です。 127.0.0.1 のバインドは変更しないでください。  
  
4.  SSL 証明書を選択し、 **[OK]** をクリックして変更を保存します。  
  
### <a name="a-certificate-expires-within-30-days"></a>証明書の有効期限が 30 日以内に切れる  
 **問題:** サーバー証明書の有効期限は30日以内に切れます。  
  
 **影響:** サーバーは、有効期限が切れた証明書を使用できません。 証明書の有効期限が切れると、ユーザーは Anywhere Access 機能を使用できない可能性があります。  
  
 **解決策:** 証明書の有効期限が切れないようにするには、信頼された証明機関で証明書を更新します。  
  
### <a name="certificate-subject-does-not-match-the-name-configured-by-domain-name-wizard"></a>証明書のサブジェクトが [ドメイン名] ウィザードで設定した名前と一致しない  
 **問題:** 証明書のサブジェクトが、ドメイン名ウィザードで構成された名前と一致しません。  
  
 **影響:** 証明書のサブジェクトがドメイン名ウィザードで構成された名前と一致しない場合、一部の web サイトは初期化されません。 他のサイトでは、"この web サイトのセキュリティ証明書に問題があります。" というエラーが表示されます。  
  
 **解決策:** この問題を解決するには、[Anywhere Access のセットアップ] ウィザードをもう一度実行し、証明書の正しいドメイン名を指定するか、使用するドメイン名と一致する新しい証明書を購入します。  
  
### <a name="one-or-more-user-accounts-have-duplicate-cn-names"></a>1 つ以上のユーザー アカウントに重複した CN 名がある  
 **問題:** 1つ以上のユーザーアカウントに重複する CN 名があります: {0}。  
  
 **影響:** ユーザーアカウントに重複する CN 名がある場合、ユーザーはネットワークにログオンできない可能性があります。 さらに、Active Directory でユーザーを検索すると、正しくない値が返される可能性があります。  
  
 **解決策:** この問題を解決するには、ネットワークユーザーアカウントの名前が重複していないことを確認します。 より簡単に行うため、確認用に Active Directory の内容をテキスト ファイルにエクスポートすることを検討してください。 この方法の詳細については、「 [LDIFDE を使用してディレクトリオブジェクトを Active Directory にインポートおよびエクスポートする (サポート技術情報の記事 237677)](https://support.microsoft.com/kb/237677) 」 (https://support.microsoft.com/kb/237677)を参照してください。  
  
### <a name="nt-backup-is-installed"></a>NT のバックアップがインストールされている  
 **問題:** Windows NT バックアッププログラムがサーバーにインストールされていること。  
  
 **影響:**  Windows Server Essentials では、Windows Server バックアップを使用します。 Windows NT バックアップ プログラムもインストールされている場合、2 つのバックアップ プログラムの間に競合が存在する可能性があります。 これにより、Windows Server バックアップのプロセスが失敗することがあります。 また、競合により、バックアップを使用してサーバーを復元できなくなる場合があります。  
  
 **解決策:** この問題を解決するには、サーバーから NT バックアッププログラムをアンインストールします。  
  
### <a name="iis-does-not-own-port-80-000080-or-port-443-0000443"></a>IIS がポート 80 (0.0.0.0:80) またはポート 443 (0.0.0.0:443) を保有していない  
 **問題:** インターネットインフォメーションサービス (IIS) は、ポート 80 (0.0.0.0:80) またはポート443を所有していません。 これらのポートは、現在他のアプリケーションによってバインドされています。  
  
 **影響:**  Windows Server Essentials web アプリケーションでは、ユーザーがサービスを利用できるようにするために、ポート80とポート443を使用する必要があります。 別のプロセスまたはアプリケーションが既にポート80またはポート443を使用している場合、Windows Server Essentials web アプリケーションを実行することはできません。 このような場合は、ユーザーはリモート Web アクセスおよびその他のアプリケーションを使用できません。  
  
 **解決策:** この問題を解決するには、既にポート80またはポート443を使用しているアプリケーションをアンインストールするか、別のポートにそのアプリケーションを割り当てます。  
  
### <a name="the-default-website-is-not-running"></a>既定の Web サイトが実行されていない  
 **問題:** 既定の web サイトが Windows Server Essentials 環境で実行されていません。  
  
 **影響:**  Windows Server Essentials web アプリケーションでは、既定の web サイトを使用する必要があります。 既定の Web サイトが実行されていない場合、ユーザーはリモート Web アクセスおよびその他のアプリケーションを使用できません。  
  
 **解決**  
  
##### <a name="to-start-the-default-website"></a>既定の Web サイトを開始するには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] で、サーバー名を展開し、 **[サイト]** をクリックします。  
  
3.  **[既定の Web サイト]** を右クリックし、 **[Web サイトの管理]** をポイントしてから、 **[開始]** をクリックします。  
  
### <a name="read-and-script-permissions-for-the-remote-virtual-directory-are-incorrect"></a>/Remote 仮想ディレクトリに対する読み取りとスクリプトのアクセス許可が正しくない  
 **問題:** 読み取りとスクリプトのアクセス許可が、この仮想ディレクトリに割り当てられていません。  
  
 **影響:** 仮想ディレクトリに対する読み取りとスクリプトのアクセス許可が正しくない場合、ユーザーはリモート Web アクセスを使用できません。 リモート Web アクセスを使用してインターネットを参照しようとすると、"HTTP エラー403.1 は許可されていません" というエラーが発生することがあります。  
  
 **解決**  
  
##### <a name="to-assign-read-and-script-permissions-to-the-remote-directory"></a>/Remote ディレクトリに対して読み取りとスクリプトのアクセス許可を割り当てるには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] で、サーバー名を展開し、 **[サイト]** をクリックします。  
  
3.  **[既定の Web サイト]** 、 **[リモート]** の順に展開します。  
  
4.  **[機能ビュー]** で、 **[ハンドラー マッピング]** をダブルクリックします。  
  
5.  **[操作]** ウィンドウで、 **[機能のアクセス許可の編集]** をクリックします。  
  
6.  **[読み取り]** と **[スクリプト]** チェック ボックスをオンにし、 **[OK]** をクリックします。  
  
### <a name="http-redirect-is-either-set-or-inherited-on-the-remote-virtual-directory"></a>HTTP リダイレクトが、/Remote 仮想ディレクトリに設定または継承されている  
 **問題:** HTTP リダイレクト属性が、複数の仮想ディレクトリに対して予期せず設定または継承されています。  
  
 **影響:** オフラインの仮想ディレクトリに対して HTTP リダイレクト属性が設定されている場合、リモート Web ワークプレースは正常に機能しません。  
  
 **解決**  
  
##### <a name="to-remove-the-http-redirect-attribute"></a>HTTP リダイレクト属性を削除するには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] で、サーバー名を展開し、 **[サイト]** をクリックします。  
  
3.  **[既定の Web サイト]** 、 **[リモート]** の順に展開します。  
  
4.  **[機能ビュー]** で **[HTTP リダイレクト]** をダブルクリックします。  
  
5.  **[この宛先に要求をリダイレクト]** チェック ボックスをオフにしてから、 **[操作]** ウィンドウで **[適用]** をクリックします。  
  
### <a name="a-host-name-exists-for-port-80-on-the-default-website"></a>既定の Web サイトのポート 80 にホスト名が存在する  
 **問題:** 既定の web サイトでは、ポート80にホスト名が割り当てられます。  
  
 **影響:** 既定の web サイトのポート80にホスト名が割り当てられている場合は、一部の Windows Server Essentials web アプリケーションに接続できないことがあります。 ホスト名は不要であり、このような状況ではお勧めしません。  
  
 **解決**  
  
##### <a name="to-clear-the-host-name-entry-for-port-80-on-the-default-website"></a>既定の Web サイトのポート 80 にあるホスト名のエントリを消去するには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] で、サーバー名を展開し、 **[サイト]** をクリックします。  
  
3.  **[機能] ビュー**で、 **[既定の Web サイト]** を右クリックしてから、 **[バインド]** をクリックします。  
  
4.  **[サイト バインド]** で、 **[ポート 80 の http]** の設定を選択してから、 **[編集]** をクリックします。  
  
5.  **[サイト バインドの編集]** で、 **[ホスト名]** エントリを消去してから、 **[OK]** をクリックします。  
  
### <a name="backup-does-not-succeed-because-of-a-hidden-partition"></a>隠れたパーティションのため、バックアップが成功しない  
 **問題:** 非 NTFS パーティションは、Windows Server バックアップによってバックアップのスケジュールが設定されます。  
  
 **影響:** Windows Server バックアップは、NTFS としてフォーマットされたパーティションのみをバックアップできます。  
  
 **解決策:** 非 NTFS パーティションをバックアップするように Windows Server バックアップを構成しないでください。 詳細については、「 [Windows Server 2008 ベースのコンピューターでシステム状態のバックアップが失敗したときにイベント id 12290 および16387がログに記録される (サポート技術情報の記事 968128)](https://support.microsoft.com/kb/968128) 」 (https://support.microsoft.com/kb/968128)を参照してください。  
  
### <a name="the-most-recent-backup-did-not-succeed"></a>直近のバックアップが成功しなかった  
 **問題:** 最新のバックアップ試行は正常に完了しませんでした。  
  
 **影響:** システムのバックアップの状態が正しくありません。  
  
 **解決策:** イベントログとバックアップログで、最新のバックアップ中に発生したエラーを確認します。  
  
### <a name="the-startup-type-for-the-file-replication-service-is-not-set-to-automatic"></a>ファイル レプリケーション サービスのスタートアップの種類が ”自動" に設定されていない  
 **問題:** スタートアップの種類が既定値の [自動] に設定されていない場合、ファイルレプリケーションサービス (FRS) が開始しないことがあります。  
  
 **影響:** ファイルレプリケーションサービスが実行されていない場合、ドメインコントローラーはそのサービスのアドバタイズを停止する可能性があります。 これにより、ログオン エラーやグループ ポリシー エラーなど、その他の問題につながる可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-the-file-replication-service-for-automatic-startup"></a>ファイル レプリケーション サービスが自動的に開始するように構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、 **[ファイル レプリケーション]** をダブルクリックします。  
  
3.  **[スタートアップの種類]** で **[自動]** を選択し、 **[適用]** をクリックします。  
  
### <a name="the-file-replication-service-is-not-running"></a>ファイル レプリケーション サービスが実行されていない  
 **問題:** ファイルレプリケーションサービスが実行されていません。  
  
 **影響:** ファイルレプリケーションサービスが実行されていない場合、ドメインコントローラーはそのサービスのアドバタイズを停止する可能性があります。 この動作は、ログオン エラーやグループ ポリシー エラーなど、その他の問題につながる可能性があります。  
  
 **解決**  
  
##### <a name="to-start-the-file-replication-service"></a>ファイル レプリケーション サービスを開始するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、 **[ファイル レプリケーション サービス]** をダブルクリックします。  
  
3.  **[スタート]** をクリックします。  
  
### <a name="the-logon-account-for-the-file-replication-service-is-not-set-to-use-the-local-system-account"></a>ファイル レプリケーション サービスのログオン アカウントが、ローカル システム アカウントを使用するように設定されていない  
 **問題:** ファイルレプリケーションサービスは、既定のログオンアカウントとしてローカルシステムアカウントを使用するように構成されていません。  
  
 **影響:** ファイルレプリケーションサービスが既定のログオンアカウントとしてローカルシステムを使用していない場合は、アクセス許可に関連するエラーが発生する可能性があります。 これらのエラーは、他のエラーのトリガーとなり、最終的にドメイン コント ローラーがそのサービスのアドバタイズを停止する可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-local-system-as-the-default-logon-account-for-file-replication"></a>ファイル レプリケーションの既定のログオン アカウントとしてローカル システムを構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、 **[ファイル レプリケーション]** をダブルクリックします。  
  
3.  **[サービスのプロパティ]** ページで、 **[ログオン]** タブをクリックします。  
  
4.  **[ローカル システム アカウント]** オプションをクリックしてから、 **[適用]** をクリックします。  
  
5.  サービスを再起動します。  
  
### <a name="the-startup-type-for-the-dfs-replication-service-is-not-set-to-automatic"></a>DFS レプリケーション サービスのスタートアップの種類が ”自動" に設定されていない  
 **問題:** スタートアップの種類が既定値の "自動" に設定されていない場合、DFS レプリケーションサービスが開始しないことがあります。  
  
 **影響:** DFS レプリケーションサービスが実行されていない場合、ドメインコントローラーはそのサービスのアドバタイズを停止する可能性があります。 これにより、ログオン エラーやグループ ポリシー エラーなど、その他の問題につながる可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-the-dfs-replication-service-for-automatic-startup"></a>DFS レプリケーション サービスが自動的に開始するように構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、 **[DFS レプリケーション]** をダブルクリックします。  
  
3.  **[スタートアップの種類]** で **[自動]** を選択し、 **[適用]** をクリックします。  
  
### <a name="the-dfs-replication-service-is-not-running"></a>DFS レプリケーション サービスが実行されていない  
 **問題:** DFS レプリケーションサービスは現在実行されていません。  
  
 **影響:** DFS レプリケーションサービスが実行されていない場合、ドメインコントローラーはそのサービスのアドバタイズを停止する可能性があります。 この動作は、ログオン エラーやグループ ポリシー エラーなど、その他の問題につながる可能性があります。  
  
 **解決**  
  
##### <a name="to-start-the-dfs-replication-service"></a>DFS レプリケーション サービスを開始するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、 **[DFS レプリケーション]** をダブルクリックします。  
  
3.  **[スタート]** をクリックします。  
  
### <a name="the-dfs-replication-service-is-not-is-not-set-to-use-the-local-system-account"></a>DFS レプリケーション サービスがローカル システム アカウントを使用するように設定されていない  
 **問題:** DFS レプリケーションサービスが、既定のログオンアカウントとしてローカルシステムアカウントを使用するように設定されていません。  
  
 **影響:** DFS レプリケーションサービスが既定のログオンアカウントとしてローカルシステムを使用していない場合は、アクセス許可に関連するエラーが発生する可能性があります。 これらのエラーは、他のエラーのトリガーとなり、最終的にドメイン コント ローラーがそのサービスのアドバタイズを停止する可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-dfs-replication-to-use-local-system-as-the-default-logon-account"></a>DFS レプリケーションが既定のログオン アカウントとしてローカル システムを使用するように構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、 **[DFS レプリケーション]** をダブルクリックします。  
  
3.  **[サービスのプロパティ]** ページで、 **[ログオン]** タブをクリックします。  
  
4.  **[ローカル システム アカウント]** オプションをクリックしてから、 **[適用]** をクリックします。  
  
5.  サービスを再起動します。  
  
### <a name="the-windows-server-office-365-integration-service-is-not-set-to-use-the-local-system-account"></a>Windows Server Office 365 統合サービスがローカル システム アカウントを使用するように設定されていない  
 **問題:** Windows Server Office 365 統合サービスが、既定のログオンアカウントとしてローカルシステムアカウントを使用するように設定されていません。  
  
 **影響:** Windows Server Office 365 統合サービスが既定のログオンアカウントとしてローカルシステムを使用していない場合、Office 365 の一部の機能が正常に機能しない可能性があります。 また、アクセス許可に関連するエラーが発生する可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-the-office-365-integration-service-to-use-local-system-as-the-default-logon-account"></a>Office 365 統合サービスが既定のログオン アカウントとしてローカル システムを使用するように構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、 **[Windows Server Office 365 統合サービス]** をダブルクリックします。  
  
3.  **[サービスのプロパティ]** ページで、 **[ログオン]** タブをクリックします。  
  
4.  **[ローカル システム アカウント]** オプションをクリックしてから、 **[適用]** をクリックします。  
  
5.  サービスを再起動します。  
  
### <a name="the-windows-server-office-365-integration-service-is-not-running"></a>Windows Server Office 365 統合サービスが実行されていない  
 **問題:** Windows Server Office 365 統合サービスは現在実行されていません。  
  
 **影響:** Windows Server Office 365 統合サービスが実行されていない場合、Office 365 のクラウドベースの機能は使用できません。  
  
 **解決**  
  
##### <a name="to-start-the-windows-server-office-365-integration-service"></a>Windows Server Office 365 統合サービスを開始するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、 **[Windows Server Office 365 統合サービス]** をダブルクリックします。  
  
3.  **[スタート]** をクリックします。  
  
### <a name="the-startup-type-for-the-windows-server-office-365-integration-service-is-not-set-to-automatic"></a>Windows Server Office 365 統合サービスのスタートアップの種類が ”自動” に設定されていない  
 **問題:** スタートアップの種類が既定値の自動に設定されていない場合、Windows Server Office 365 統合サービスが開始しないことがあります。  
  
 **影響:** Windows Server Office 365 統合サービスが実行されていない場合、Office 365 のクラウドベースの機能は使用できません。  
  
 **解決**  
  
##### <a name="to-configure-the-office-365-integration-service-for-automatic-startup"></a>Windows Server Office 365 統合サービスが自動的に開始するように構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、 **[Windows Server Office 365 統合サービス]** をダブルクリックします。  
  
3.  **[スタートアップの種類]** で **[自動]** を選択し、 **[適用]** をクリックします。  
  
### <a name="a-registry-value-is-missing-or-set-incorrectly"></a>レジストリの値が不足しているか、正しく設定されていない  
 **問題:** HKEY_LOCAL_MACHINE \Software\Microsoft\Rpc\RpcProxy の下のレジストリキーに正しくない値が含まれているか、存在しません。  
  
 **影響:** RPCProxy レジストリキーが正しく設定されていない場合、次のようなエラーメッセージが表示されることがあります。 "リモートデスクトップゲートウェイサーバーが一時的に使用できないため、このコンピューターはリモートコンピューターに接続できません。 後で再接続するか、ネットワーク管理者にお問い合わせください。"  
  
 **解決**  
  
##### <a name="to-correct-the-registry-setting"></a>レジストリの設定を修正するには  
  
1.  レジストリ エディタを開きます。  
  
2.  次のレジストリ キーに移動します。  
  
     HKEY_LOCAL_MACHINE\Software\Microsoft\Rpc\RpcProxy  
  
3.  "Website" という名前の文字列に、[既定の Web サイト] のデータ値が設定されていることを確認します。  
  
    -   データ値が正しくない場合は、適切な値を使用するように文字列を変更します。  
  
    -   文字列が存在しない場合は、"Website" という名前の新しい文字列を作成し、データ値を "Default Web Site" に設定します。  
  
### <a name="the-startup-type-for-the-block-level-backup-engine-service-is-not-set-to-manual"></a>ブロック レベルのバックアップ エンジン サービスのスタートアップの種類が ”手動" に設定されていない  
 **問題:** ブロックレベルのバックアップエンジンサービスでは、既定のスタートアップの種類として "手動" が使用されていません。  
  
 **影響:** スタートアップの種類が手動に設定されていない場合、ブロックレベルのバックアップエンジンサービスは開始されない可能性があります。 この問題は、Windows Server バックアップジョブが失敗する原因となる可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-for-manual-startup"></a>ブロック レベルのバックアップ エンジン サービスで手動スタートアップを構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、 **[ブロック レベルのバックアップ エンジン サービス]** をダブルクリックします。  
  
3.  **[スタートアップの種類]** で **[手動]** を選択し、 **[適用]** をクリックします。  
  
### <a name="the-logon-account-for-the-block-level-backup-engine-service-is-not-set-to-use-the-local-system-account"></a>ブロック レベルのバックアップ エンジン サービスのログオン アカウントが、ローカル システム アカウントを使用するように設定されていない  
 **問題:** ブロックレベルのバックアップエンジンサービスが、既定のログオンアカウントとしてローカルシステムアカウントを使用するように設定されていません。  
  
 **影響:** ブロックレベルのバックアップエンジンサービスが、既定のログオンアカウントとしてローカルシステムを使用していない場合は、アクセス許可に関連するエラーが発生する可能性があります。 これらのエラーにより、Windows Server バックアップのジョブが正常に完了しない可能性があります。  
  
 **解決**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-to-use-local-system-as-the-default-logon-account"></a>ブロック レベルのバックアップ エンジン サービスが、既定のログオン アカウントとしてローカル システムを使用するように構成するには  
  
1.  サービス コンソールを開きます。  
  
2.  サービスの一覧で、 **[ブロック レベルのバックアップ エンジン サービス]** をダブルクリックします。  
  
3.  **[サービスのプロパティ]** ページで、 **[ログオン]** タブをクリックします。  
  
4.  **[ローカル システム アカウント]** オプションをクリックしてから、 **[適用]** をクリックします。  
  
5.  サービスを再起動します。  
  
### <a name="the-common-name-on-the-certificate-that-is-bound-to-the-wss-certificate-web-service-website-does-not-match-the-server-name"></a>WSS Certificate Web Service Web サイトにバインドしている証明書の共通名がサーバー名と一致しない  
 **問題:** 有効ではない証明書は、IIS の WSS Certificate Web Service web サイトにバインドされています。 この証明書の共通名がサーバー名と一致しません。  
  
 **影響:** WSS Certificate Web Service web サイトに有効でない証明書をバインドすると、接続ウィザードが正常に機能しない場合があります。  
  
 **解決**  
  
##### <a name="to-configure-a-valid-certificate-for-the-wss-certificate-web-service"></a>WSS Certificate Web Service に有効な証明書を構成するには  
  
1.  サーバーで、インターネット インフォメーション サービス (IIS) マネージャーを開きます。  
  
2.  [IIS マネージャー] で、サーバー名を展開し、 **[サイト]** をクリックします。  
  
3.  **[WSS Certificate Web Service]** を右クリックしてから、 **[バインドの編集]** をクリックします。  
  
4.  **[サイト バインド]** で、 **[HTTPS]** 、 **[編集]** の順にクリックします。  
  
5.  **[サイト バインドの編集]** の **[SSL 証明書]** で、サーバーと同じ名前を持つ証明書を選択します。  
  
6.  サーバーと同じ名前を持つ証明書のエントリが複数ある場合は、 **[表示]** をクリックして、どの証明書が有効かを判断し、適切な証明書を選択します。  
  
### <a name="there-appears-to-be-a-problem-with-the-certificate-binding-for-the-remote-desktop-gateway-service"></a>リモート デスクトップ ゲートウェイ サービスにバインドされている証明書に問題があるように見える  
 **問題:** リモートデスクトップゲートウェイサービスの証明書が正しくバインドされていない可能性があります。  
  
 **影響:** リモートデスクトップゲートウェイサービスの証明書が正しく構成されていない場合、ユーザーはリモート Web アクセスに接続できません。  
  
 **解決**  
  
##### <a name="to-fix-the-binding-for-the-remote-desktop-gateway-service"></a>リモート デスクトップ ゲートウェイ サービスのバインドを修復するには  
  
-   管理者としてコマンド プロンプトを開き、次のコマンドを入力します。  
  
    ```  
    REG ADD HKLM\SYSTEM\CurrentControlSet\services\HTTP\Parameters\SslBindingInfo\0.0.0.0:443  /v DefaultFlags /t REG_DWORD /d 1 /f  
    net stop tsgateway  
    net start tsgateway  
    ```  
  
     詳細については、「 [Windows Server Essentials でリモートデスクトップゲートウェイサービスを管理する方法 (サポート技術情報の記事 2472211)](https://support.microsoft.com/kb/2472211) 」 (https://support.microsoft.com/kb/2472211)を参照してください。
