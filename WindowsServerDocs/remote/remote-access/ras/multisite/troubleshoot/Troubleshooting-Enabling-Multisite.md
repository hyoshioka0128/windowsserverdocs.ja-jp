---
title: マルチサイト有効化のトラブルシューティング
description: このトピックは、ガイドの一部複数リモート アクセス サーバーの展開で Windows Server 2016 の Multisite 展開します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 570c81d6-c4f4-464c-bee9-0acbd4993584
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7fafc2e95f30a3956a1e2fdfcdf2f368a1798d28
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280966"
---
# <a name="troubleshooting-enabling-multisite"></a>マルチサイト有効化のトラブルシューティング

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、`Enable-DAMultisite` コマンドに関連する問題のトラブルシューティング情報を示します。 表示されたエラーがマルチサイト有効化に関連するものであるか確認するには、Windows イベント ログでイベント ID 10051 があるか確認してください。  
  
## <a name="user-connectivity-issues"></a>ユーザー接続の問題  
正しくない構成方法でマルチサイトを有効にした場合、ユーザー接続の問題が発生する可能性があります。  
  
**原因**  
  
マルチサイト展開では、Windows 10 および Windows 8 クライアント コンピューターは異なるエントリ ポイント間をローミングできます。  Windows 7 クライアント コンピューターは、マルチサイト展開内の特定のエントリ ポイントに関連付けられたである必要があります。 クライアント コンピューターが適切なセキュリティ グループに属していない場合、誤ったグループ ポリシー設定を受け取る可能性があります。  
  
**ソリューション**  
  
DirectAccess では、すべての Windows 10 および Windows 8 クライアント コンピューターの少なくとも 1 つのセキュリティ グループが必要です。すべての Windows 10 および Windows 8 コンピューターのドメインごとに 1 つのセキュリティ グループを使用することをお勧めします。 DirectAccess には、各エントリ ポイントの Windows 7 クライアント コンピューターのセキュリティ グループも必要です。 各クライアント コンピューターは、1 つのセキュリティ グループにのみ属している必要があります。 そのため、セキュリティ グループを Windows 10 用 Windows 8 クライアントは、Windows 10 または Windows 8 を実行しているコンピューターのみを含めることがいることを確認する必要があり、各 Windows 7 クライアント コンピューターが関連するエントリ ポイント専用の 1 つのセキュリティ グループに属しているとWindows 10 または Windows 8 に属しているクライアントなし、Windows 7 のセキュリティ グループ。  
  
Windows 8 のセキュリティ グループを構成、**グループの選択**のページ、 **DirectAccess クライアントのセットアップ**ウィザード。 Windows 7 のセキュリティ グループを構成、**クライアント サポート**のページ、**マルチサイト展開を有効にする**ウィザード、または、**クライアント サポート**のページ、 **エントリ ポイントを追加**ウィザード。  
  
## <a name="kerberos-proxy-authentication"></a>Kerberos プロキシ認証  
**表示されるエラー**します。 マルチサイト展開では、Kerberos プロキシ認証がサポートされていません。 コンピューター証明書を IPsec ユーザー認証に使用できるようにする必要があります。  
  
**原因**  
  
マルチサイトを有効にする前に、コンピューター証明書認証を有効にする必要があります。  
  
**ソリューション**  
  
コンピューター証明書認証を有効にするには、次の手順を実行します。  
  
1.  リモート アクセス管理コンソールの詳細ウィンドウの **[手順 2 リモート アクセス サーバー]** で、 **[編集]** をクリックします。  
  
2.  **リモート アクセス サーバーのセットアップ** ウィザードの **[認証]** ページで、 **[コンピューターの証明書を使用する]** チェック ボックスをオンにし、展開内で証明書を発行するルート証明機関または中間証明機関を選択します。  
  
Windows PowerShell を使用してコンピューター証明書認証を有効にするには使用、`Set-DAServer`コマンドレットを指定し、 *IPsecRootCertificate*パラメーター。  
  
## <a name="ip-https-certificates"></a>IP-HTTPS 証明書  
**表示されるエラー**します。 DirectAccess サーバーは IP-HTTPS 自己署名証明書を使用します。 既知の CA から発行された署名入りの証明書を使用するように IP-HTTPS を構成してください。  
  
**原因**  
  
IP-HTTPS 証明書が自己署名されています。 マルチサイト展開で自己署名証明書を使用することはできません。  
  
**ソリューション**  
  
IP-HTTPS 証明書を選択するには、次の手順を実行します。  
  
1.  リモート アクセス管理コンソールの詳細ウィンドウの **[手順 2 リモート アクセス サーバー]** で、 **[編集]** をクリックします。  
  
2.  **リモート アクセス サーバーのセットアップ** ウィザードの **[ネットワーク アダプター]** ページの **[IP-HTTPS 接続の認証に使用する証明書を選択してください]** で、 **[DirectAccess で自動的に作成される自己署名証明書を使用する]** チェック ボックスがオフになっていることを確認し、 **[参照]** をクリックして、信頼できる CA によって発行された証明書を選択します。  
  
## <a name="network-location-server"></a>ネットワーク ロケーション サーバー  
  
-   **問題 1**  
  
    **表示されるエラー**します。 DirectAccess を構成して、ネットワーク ロケーション サーバーの自己署名証明書を使用します。 CA から発行された署名入りの証明書を使用するようにネットワーク ロケーション サーバーを構成してください。  
  
    **原因**  
  
    ネットワーク ロケーション サーバーがリモート アクセス サーバー上に展開されていて、自己署名証明書を使用しています。 マルチサイト展開で自己署名証明書を使用することはできません。  
  
    **ソリューション**  
  
    ネットワーク ロケーション サーバーの証明書を選択するには、次の手順を実行します。  
  
    1.  リモート アクセス管理コンソールの詳細ウィンドウの **[手順 3 インフラストラクチャ サーバー]** で、 **[編集]** をクリックします。  
  
    2.  **インフラストラクチャ サーバーのセットアップ** ウィザードの **[ネットワーク ロケーション サーバー]** ページの **[ネットワーク ロケーション サーバーをリモート アクセス サーバー上に展開する]** で、 **[自己署名証明書を使用する]** チェック ボックスがオフになっていることを確認し、 **[参照]** をクリックして、エンタープライズ CA によって発行された証明書を選択します。  
  
-   **問題 2**  
  
    **表示されるエラー**します。 展開ネットワーク負荷分散クラスターまたはマルチサイト展開、リモート アクセス サーバーの内部名とは異なるサブジェクト名を持つネットワーク ロケーション サーバー証明書を取得します。  
  
    **原因**  
  
    ネットワーク ロケーション サーバーの Web サイト用証明書のサブジェクト名がリモート アクセス サーバーの内部名と同じです。 これは名前解決の問題を引き起こします。  
  
    **ソリューション**  
  
    リモート アクセス サーバーの内部名とは異なるサブジェクト名を持つ証明書を取得します。  
  
    ネットワーク ロケーション サーバーを構成するには、次の手順を実行します。  
  
    1.  リモート アクセス管理コンソールの詳細ウィンドウの **[手順 3 インフラストラクチャ サーバー]** で、 **[編集]** をクリックします。  
  
    2.  **インフラストラクチャ サーバーのセットアップ** ウィザードの **[ネットワーク ロケーション サーバー]** ページの **[ネットワーク ロケーション サーバーをリモート アクセス サーバー上に展開する]** で、 **[参照]** をクリックして、以前に取得した証明書を選択します。 この証明書は、リモート アクセス サーバーの内部名とは異なるサブジェクト名を持っている必要があります。  
  
## <a name="windows-7-client-computers"></a>Windows 7 クライアント コンピューター  
**表示される警告**します。 マルチサイトを有効にするときに、DirectAccess クライアント用に構成されたセキュリティ グループは Windows 7 コンピューターを含めないでください。 マルチサイト展開で Windows 7 クライアント コンピューターをサポートするには、それらのクライアントを含むセキュリティ グループを各エントリ ポイントに対して選択します。  
  
**原因**  
  
既存の DirectAccess 展開では、Windows 7 クライアントのサポートが有効にされました。  
  
**ソリューション**  
  
DirectAccess には、各エントリ ポイントの Windows 7 クライアント コンピューターのすべての Windows 8 クライアント コンピューターの少なくとも 1 つのセキュリティ グループとセキュリティ グループが必要です。 各クライアント コンピューターは、1 つのセキュリティ グループにのみ属している必要があります。 そのため、する Windows 8 クライアントのセキュリティ グループに、Windows 8 を実行しているコンピューターのみが含まれていると、各 Windows 7 クライアント コンピューターが関連するエントリ ポイント用の専用の 1 つのセキュリティ グループに属していることを確認してください Windows 8 クライアントなしWindows 7 のセキュリティ グループに属しています。  
  
## <a name="active-directory-site"></a>Active Directory サイト  
**表示されるエラー**します。 サーバー < server_name > は、Active Directory サイトに関連付けられていません。  
  
**原因**  
  
DirectAccess は、Active Directory サイトを特定できませんでした。 Active Directory サイトとサービス コンソールでは、ネットワークのさまざまなサブネットを構成し、各サブネットを関連する Active Directory サイトに関連付けることができます。 このエラーは、リモート アクセス サーバーの IP アドレスがどのサブネットにも属していない場合、または IP アドレスが属しているサブネットが Active Directory サイトで定義されていない場合に発生する可能性があります。  
  
**ソリューション**  
  
リモート アクセス サーバーで `nltest /dsgetsite` コマンドを実行して、この問題が生じているかどうかを確認します。 この問題が生じている場合は、このコマンドから ERROR_NO_SITENAME が返されます。 この問題を解決するには、内部サーバーの IP アドレスを含むサブネットが存在すること、およびそのサブネットが Active Directory サイトで定義されていることを確認します。  
  
## <a name="SaveGPOSettings"></a>サーバー GPO 設定の保存  
**表示されるエラー**します。 リモート アクセスの設定を GPO < gpo 名 > に保存中にエラーが発生しました。  
  
**原因**  
  
接続の問題がいずれかのサーバー GPO への変更を保存できませんでしたまたは registry.pol ファイルに対する共有違反がある場合など、別のユーザーがファイルをロックします。  
  
**ソリューション**  
  
リモート アクセス サーバーとドメイン コントローラー間に接続が存在することを確認します。 接続が存在する場合は、ドメイン コントローラーを調べて registry.pol ファイルが別のユーザーに対してロックされているかどうかを確認し、必要な場合はそのユーザー セッションを終了してファイルのロックを解除します。  
  
## <a name="InternalServerError"></a>内部エラーが発生しました  
**表示されるエラー**します。 内部エラーが発生しました。  
  
**原因**  
  
これはクライアント GPO に予期しないエントリ ポイント テーブルが構成されていることが原因で発生する可能性があります。 管理者が DirectAccess クライアント コマンドレットを使用してクライアント GPO のエントリ ポイント テーブルを編集した場合に発生する可能性があります。  
  
**ソリューション**  
  
すべてのクライアント GPO のエントリ ポイント テーブル構成を確認し、クライアント GPO のさまざまなインスタンスと DirectAccess 構成の間のマルチサイト構成の不整合をすべて解決します。 クライアント GPO の名前を指定して `Get-DaEntryPointTableItem` コマンドレットを実行し、クライアントのエントリ ポイント テーブルを取得します。 `Get-NetIPHttpsConfiguration` コマンドレットを使用して、すべてのエントリ ポイントの IP-HTTPS プロファイルをすべて取得します。  
  
詳細については、次を参照してください。 [Windows PowerShell の DirectAccess クライアント コマンドレット](https://technet.microsoft.com/library/hh848426)します。  
  


