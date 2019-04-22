---
title: OTP の有効化のトラブルシューティング
description: このトピックでは、ガイド Windows Server 2016 での OTP 認証を使用したリモート アクセスの展開の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b58252ca-4c1d-4664-a3c4-7301e2121517
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d789671a0425974e560e5f4a43ebcba4c1741c76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819463"
---
# <a name="troubleshooting-enabling-otp"></a>OTP の有効化のトラブルシューティング

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックには、いずれかを使用して DirectAccess OTP 認証を有効化に関連する問題のトラブルシューティング情報が含まれています、**有効にする DAOtpAuthentication** PowerShell コマンドレットまたはリモート アクセス管理コンソール。
  
## <a name="failed-to-enroll-the-otp-signing-certificate"></a>OTP の署名証明書の登録に失敗しました  
**表示されるエラー** (サーバーのイベント ログ)。 証明書テンプレート < OTP_signing_template_name > を使用して、OTP の署名証明書を登録することはできません。  
  
**原因**  
  
このエラーの考えられる原因を次の 3 つあります。  
  
-   テンプレートは存在しません。  
  
-   テンプレートで設定された権限では、DirectAccess サーバーを登録できません。  
  
-   発行元証明機関 (CA) へのネットワーク接続はありません。  
  
**ソリューション**  
  
1.  OTP の署名と指定した名前のテンプレートが証明書を確認します。  
  
    1.  存在し、適切なアクセス許可を持ちます。  
  
    2.  DirectAccess サーバーに証明書を発行することができますを少なくとも 1 つの CA によって発行される設定されます。  
  
2.  テンプレートは存在かどうか、登録機関の証明書の 3.3 のプランの説明に従って作成や別の一致するテンプレートが存在する場合は、新しいテンプレートの名前を持つ DirectAccess OTP を再構成します。  
  
## <a name="failed-to-enable-directaccess-otp-when-webdav-is-installed"></a>WebDAV がインストールされている場合は、DirectAccess の OTP を有効にできませんでした。  
**シナリオ**します。 リモート アクセス管理コンソールで、またはを使用して DirectAccess OTP 構成を適用しているときに、 `Enable-DAOtpAuthentication` PowerShell コマンドレットの操作は失敗します。  
  
**表示されるエラー** (サーバーのイベント ログ)。 WebDAV IIS 拡張機能が、サーバーで実行されているために、DirectAccess の OTP 設定を適用できません。 WebDAV を削除し、もう一度設定を適用します。  
  
**原因**  
  
DirectAccess OTP サービスでは、WebDAV 発行機能と互換性がないと、WebDAV がインストールされているときに有効にすることはできません。  
  
**ソリューション**  
  
WebDAV の役割をアンインストールします。  
  
1.  左側のウィンドウで、サーバー マネージャー コンソール をクリックして**IIS**します。  
  
2.  メイン ウィンドウで、スクロールする**役割と機能の**します。  
  
3.  右クリック**WebDAV 発行**、 をクリックし、**役割の削除または機能**します。  
  
4.  役割の削除と機能ウィザードを完了します。  
  
5.  DirectAccess OTP の構成を再適用します。  
  
## <a name="no-templates-available-in-the-remote-access-management-console"></a>リモート アクセス管理コンソールで使用できるテンプレートがありません。  
**シナリオ**します。 構成の一部をリモート アクセス管理コンソールを使用して OTP] または [登録機関証明書テンプレートまたはすべてのテンプレートは、選択ウィンドウから不足しています。  
  
**原因**  
  
このエラーの考えられる原因が 2 つあります。  
  
-   DirectAccess OTP の要件に従って、テンプレートが構成されていないと、ので選択することはできません。  
  
-   選択した Ca **OTP CA サーバー**必要なテンプレートの発行は構成されていません。  
  
**ソリューション**  
  
1.  OTP のログオンのテンプレートと OTP の署名証明書テンプレートが登録機関の証明書を計画、OTP 証明書テンプレートと 3.3、3.2 計画で説明されているように正しく構成されていることを確認します。  
  
2.  確認しますで構成されている Ca、 **OTP CA サーバー**一覧は、次の問題に関連するテンプレートを構成します。  
  
    1.  CA サーバーでは、証明機関 コンソールを開きます。  
  
    2.  左側のウィンドウでは、選択した CA サーバーを展開します。  
  
    3.  クリックして**証明書テンプレート**し、必要なテンプレートが有効になっているかどうかを確認します。 ない場合を右クリックして**証明書テンプレート**、 をクリックして**新規**、 をクリックして**を発行する証明書テンプレート**、しを有効にテンプレートを選択します。  
  
## <a name="cannot-set-renewal-period-of-otp-template-to-1-hour"></a>1 時間に OTP テンプレートの更新期間を設定することはできません。  
**シナリオ**します。 Windows 2003 の CA を使用して DirectAccess OTP ログオンのテンプレートを構成するときに、1 時間に、テンプレートの更新期間を設定することはできません。  
  
**原因**  
  
Windows Server 2003 での証明書テンプレート MMC スナップインは、しないと、1 時間に、テンプレートの更新期間を設定できます。  
  
**ソリューション**  
  
後の Windows Server 2003 のサーバーに証明書テンプレート スナップインをインストールし、これを使用して、OTP ログオンのテンプレートを構成するを参照してください[証明書テンプレート スナップインをインストール](https://technet.microsoft.com/library/cc732445.aspx)します。  
  


