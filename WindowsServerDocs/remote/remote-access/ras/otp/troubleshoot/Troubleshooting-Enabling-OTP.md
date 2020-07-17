---
title: OTP の有効化のトラブルシューティング
description: このトピックは、「Windows Server 2016 で OTP 認証を使用してリモートアクセスを展開する」の一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: b58252ca-4c1d-4664-a3c4-7301e2121517
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9be7ef4c4d07b522f683a403e46a11e109dbd226
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853645"
---
# <a name="troubleshooting-enabling-otp"></a>OTP の有効化のトラブルシューティング

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、 **DAOtpAuthentication** PowerShell コマンドレットまたはリモートアクセス管理コンソールを使用した DirectAccess OTP 認証の有効化に関連する問題のトラブルシューティング情報について説明します。
  
## <a name="failed-to-enroll-the-otp-signing-certificate"></a>OTP 署名証明書を登録できませんでした  
**エラーを受信しました**(サーバーイベントログ)。 OTP 署名証明書は、証明書テンプレート < OTP_signing_template_name を使用して登録することはできません >  
  
**原因**  
  
このエラーには、次の3つの原因が考えられます。  
  
-   テンプレートが存在しません。  
  
-   テンプレートに設定されているアクセス許可では、DirectAccess サーバーを登録することはできません。  
  
-   発行元の証明機関 (CA) へのネットワーク接続がありません。  
  
**ソリューション**  
  
1.  指定された名前を持つ OTP 署名証明書テンプレートがあることを確認します。  
  
    1.  が存在し、適切なアクセス許可を持っている。  
  
    2.  は、DirectAccess サーバーに証明書を発行できる1つ以上の CA によって発行されるように設定されます。  
  
2.  テンプレートが存在しない場合は、3.3 の説明に従って作成し、登録機関の証明書を計画します。または、別の一致するテンプレートが存在する場合は、新しいテンプレート名を使用して DirectAccess OTP を再構成します。  
  
## <a name="failed-to-enable-directaccess-otp-when-webdav-is-installed"></a>WebDAV がインストールされているときに DirectAccess OTP を有効にできませんでした  
**シナリオ**。 リモートアクセス管理コンソールまたは `Enable-DAOtpAuthentication` PowerShell コマンドレットを使用して DirectAccess OTP 構成を適用しようとすると、操作は失敗します。  
  
**エラーを受信しました**(サーバーイベントログ)。 サーバーで WebDAV IIS 拡張機能が実行されているため、DirectAccess OTP 設定を適用できません。 WebDAV を削除して、もう一度設定を適用してください。  
  
**原因**  
  
DirectAccess OTP サービスは、WebDAV 発行機能と互換性がないため、WebDAV のインストール中に有効にすることはできません。  
  
**ソリューション**  
  
WebDAV ロールをアンインストールします。  
  
1.  サーバーマネージャーコンソールの左側のウィンドウで、 **[IIS]** をクリックします。  
  
2.  メインウィンドウで、 **[役割と機能]** までスクロールします。  
  
3.  **[WebDAV 発行]** を右クリックし、 **[役割または機能の削除]** をクリックします。  
  
4.  役割と機能の削除ウィザードを完了します。  
  
5.  DirectAccess OTP 構成を再適用します。  
  
## <a name="no-templates-available-in-the-remote-access-management-console"></a>リモートアクセス管理コンソールで使用できるテンプレートがありません  
**シナリオ**。 リモートアクセス管理コンソールを使用して OTP または登録機関の証明書テンプレートを構成するときに、選択ウィンドウに一部またはすべてのテンプレートが表示されません。  
  
**原因**  
  
このエラーには、次の2つの原因が考えられます。  
  
-   このテンプレートは、DirectAccess OTP の要件に従って構成されていないため、選択できません。  
  
-   **OTP CA サーバー**で選択されている ca は、必要なテンプレートを発行するように構成されていません。  
  
**ソリューション**  
  
1.  「3.2」の説明に従って otp ログオンテンプレートと OTP 署名証明書テンプレートが正しく構成されていることを確認します。「」を参照して、OTP 証明書テンプレートと3.3 を計画します。  
  
2.  **OTP CA サーバー**の一覧に構成されている ca が、関連するテンプレートを発行するように構成されていることを確認します。  
  
    1.  CA サーバーで、証明機関コンソールを開きます。  
  
    2.  左側のウィンドウで、選択した CA サーバーを展開します。  
  
    3.  **[証明書テンプレート]** をクリックし、必要なテンプレートが有効になっていることを確認します。 そうでない場合は、 **[証明書テンプレート]** を右クリックし、 **[新規]** をクリックして、 **[発行する証明書テンプレート]** をクリックし、有効にするテンプレートを選択します。  
  
## <a name="cannot-set-renewal-period-of-otp-template-to-1-hour"></a>OTP テンプレートの更新期間を1時間に設定できません  
**シナリオ**。 Windows 2003 CA を使用して DirectAccess OTP ログオンテンプレートを構成する場合、テンプレートの更新期間を1時間に設定することはできません。  
  
**原因**  
  
Windows Server 2003 の証明書テンプレート MMC スナップインでは、テンプレートの更新期間を1時間に設定することはできません。  
  
**ソリューション**  
  
Windows Server 2003 サーバーに証明書テンプレートスナップインをインストールし、それを使用して OTP ログオンテンプレートを構成する方法については、[証明書テンプレートスナップインのインストール](https://technet.microsoft.com/library/cc732445.aspx)に関する記事をご覧ください。  
  


