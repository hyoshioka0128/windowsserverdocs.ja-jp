---
title: AD FS 2.0 WID ファームの移行の準備
description: AD FS 2.0 server WID ファームを Windows Server 2012 に移行するための準備について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: 2393e289e6a20d30db2d5523810437b6c5049fe5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940601"
---
# <a name="prepare-to-migrate-an-ad-fs-20-wid-farm"></a>AD FS 2.0 WID ファームの移行の準備
 Windows Internal Database (WID) ファームに属している AD FS 2.0 フェデレーションサーバーを Windows Server 2012 に移行する準備を行うには、これらのサーバーから AD FS 構成データをエクスポートしてバックアップする必要があります。

 AD FS の構成データをエクスポートするには、次の作業を実行します。

-   [手順 1: サービスの設定をエクスポートする](#step-1-export-service-settings)

-   [手順 2:カスタム属性ストアをバックアップする](#step-2-back-up-custom-attribute-stores)

-   [手順 3:Web ページのカスタマイズをバックアップする](#step-3-back-up-webpage-customizations)

## <a name="step-1-export-service-settings"></a>手順 1:サービスの設定をエクスポートする
 サービスの設定をエクスポートするには、次の手順を実行します。

### <a name="to-export-service-settings"></a>サービスの設定をエクスポートするには

1.  フェデレーション サービスによって使用される SSL 証明書の証明書サブジェクト名と拇印の値を記録します。 SSL 証明書を検索するには、インターネットインフォメーションサービス (IIS) 管理コンソールを開き、左側のウィンドウで [**既定の Web サイト**] を選択し、[**バインド...** ] をクリックします。 [**操作**] ウィンドウで、https バインドを検索して選択し、[**編集**] をクリックして、[**表示**] をクリックします。

> [!NOTE]
>  オプションで、SSL 証明書とその秘密キーを .pfx ファイルにエクスポートすることもできます。 詳細については、[サーバー認証証明書の秘密キー部分のエクスポートに関するページ](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)を参照してください。
>
>  SSL 証明書は、ローカル コンピューターの [個人] 証明書ストアに格納されており、オペレーティング システムをアップグレードしても保持されます。したがって、この手順は省略可能です。

2. 内部生成されない任意のトークン署名証明書/キー、トークン暗号化証明書/キー、サービス通信証明書/キーのほか、すべての自己署名証明書をエクスポートします。

サーバーで使用中のすべての証明書を表示するには、Windows PowerShell を使用します。 Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して、AD FS cmdlets を Windows PowerShell セッションに追加します。 次に、コマンド `PSH:>Get-ADFSCertificate` を実行し、サーバーで使用中のすべての証明書を表示します。 このコマンドの出力には、各証明書の格納場所を指定する StoreLocation および StoreName の値が含まれます。  その後、[サーバー認証証明書の秘密キー部分のエクスポートに関するページ](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)のガイダンスを使用して、各証明書およびその秘密キーを .pfx ファイルにエクスポートできます。

> [!NOTE]
>  オペレーティング システムをアップグレードしても、外部証明書はすべて保持されます。したがって、この手順は省略可能です。

3. AD FS 2.0 フェデレーション サービス アカウントの ID とこのアカウントのパスワードを記録します。

ID 値を検索するには、**[サービス]** コンソールで **[AD FS 2.0 Windows サービス]** の **[ログオン方法]** 列を調べ、値を手動で記録します。

## <a name="step-2-back-up-custom-attribute-stores"></a>手順 2:カスタム属性ストアをバックアップする
 AD FS によって使用中のカスタム属性ストアに関する情報を検索するには、Windows PowerShell を使用します。 Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して、AD FS cmdlets を Windows PowerShell セッションに追加します。 次に、コマンド `PSH:>Get-ADFSAttributeStore` を実行してカスタム属性ストアに関する情報を検索します。 カスタム属性ストアのアップグレードまたは移行手順はさまざまです。

## <a name="step-3-back-up-webpage-customizations"></a>手順 3:Web ページのカスタマイズをバックアップする
 任意の Web ページのカスタマイズをバックアップするには、IIS で仮想パス **“/adfs/ls”** にマップされたディレクトリから AD FS Web ページと **web.config** ファイルをコピーします。 既定では、そのファイルは **%systemdrive%\inetpub\adfs\ls** ディレクトリにあります。

## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーションサーバーの移行の準備](prepare-to-migrate-ad-fs-fed-server.md) [AD FS 2.0 フェデレーションサーバープロキシ](prepare-to-migrate-ad-fs-fed-proxy.md)の移行の準備[AD FS 2.0 フェデレーションサーバー](migrate-the-ad-fs-fed-server.md) [AD FS 2.0 フェデレーションサーバープロキシの](migrate-the-ad-fs-2-fed-server-proxy.md)移行[AD FS 1.1 Web エージェントの](migrate-the-ad-fs-web-agent.md)移行