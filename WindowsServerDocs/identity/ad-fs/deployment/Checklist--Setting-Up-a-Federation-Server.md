---
ms.assetid: 8f954004-40d5-4c5e-8e0d-e8700c8ec7b1
title: "フェデレーション サーバーのセットアップのチェックリスト-"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 44448088184d86874e91855d8a51ef40d8cea049
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="checklist-setting-up-a-federation-server"></a>チェックリスト: フェデレーション サーバーのセットアップ

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このチェックリストには、Active Directory フェデレーション サービス \(AD FS\) でフェデレーション サーバーの役割を Windows Server® 2012 を実行しているサーバーを準備するために必要な展開タスクが含まれます。  
  
> [!NOTE]  
> 順序でこのチェックリストのタスクを完了します。 参照リンクでは、手順には、このトピックに戻りできるように、このチェックリストの残りのタスクを続行することができます、その手順の手順を完了します。  
  
![フェデレーション サーバーのセットアップ](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: フェデレーション サーバーのセットアップ**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|AD FS フェデレーション サーバーを展開する作業を開始する前に確認します。1。\) データベース 2 の長所と短所の AD FS 構成を保存する Windows Internal Database \(WID\) または SQL Server を選択します。\) AD FS 展開トポロジの種類とその関連するサーバーの配置とネットワーク レイアウトの推奨事項です。|![フェデレーション サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジの決定](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![フェデレーション サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジに関する考慮事項](https://technet.microsoft.com/library/gg982489.aspx)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|実稼働環境で使用する必要がありますフェデレーション サーバーの適切な数を特定する AD FS 容量計画のガイダンスを確認します。|![フェデレーション サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバーの容量計画](https://technet.microsoft.com/library/gg749917.aspx)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|AD FS 設計ガイドで、組織内のフェデレーション サーバーを配置する場所に関する情報を確認します。|![フェデレーション サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバーの配置の計画](https://technet.microsoft.com/library/dd807069.aspx)<br /><br />![フェデレーション サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバーを配置する場所](https://technet.microsoft.com/library/dd807127.aspx)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|スタンドアロンのフェデレーション サーバーまたはフェデレーション サーバー ファームは、展開に適しているかどうかを決定します。|![フェデレーション サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[をフェデレーション サーバーを作成する場合](https://technet.microsoft.com/library/dd807101.aspx)<br /><br />![フェデレーション サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバー ファームを作成します。](https://technet.microsoft.com/library/dd807062.aspx)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|アカウント パートナー組織内、またはリソース パートナー組織内に、この新しいフェデレーション サーバーを作成するかどうかを決定します。|![フェデレーション サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[アカウント パートナーのフェデレーション サーバーの役割を確認します。](https://technet.microsoft.com/library/dd807117.aspx)<br /><br />![フェデレーション サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[リソース パートナーのフェデレーション サーバーの役割を確認します。](https://technet.microsoft.com/library/dd807065.aspx)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|クライアントとフェデレーション サーバー プロキシの要求を安全に認証する、フェデレーション サーバーがサービス通信証明書と token\ 署名証明書を使用する方法に関する情報を確認します。 **注意:**が時間経過している https:\/\/myserver などの非修飾ホスト名を持つ証明書を使用する一般的な方法で、これらの証明書なしセキュリティの値があり、社内のクライアントへの AD FS フェデレーション サービスの偽装が攻撃者が有効にすることができます。 このため、お勧め完全修飾ドメインを使用することなど https:\/\/myserver.contoso.com \(FQDN\) の名前を指定し、のみ、フェデレーション サービスの FQDN に発行された SSL 証明書を使用します。|![フェデレーション サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーション サーバーに正常な名前解決が発生することができるように、企業ネットワークのドメイン ネーム システム \(DNS\) を更新する方法に関する情報を確認します。|![フェデレーション サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバーの名前解決の要件](https://technet.microsoft.com/library/dd807041.aspx)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|アカウント パートナー フォレストまたはまたはそのフォレストの信頼する側のフォレストからユーザーの認証に使用がリソース パートナー フォレスト内のドメインにフェデレーション サーバーとなるコンピューターを参加させます。 **注:**アカウント パートナー組織内のフェデレーション サーバーを設定する場合は、コンピューターをそのフォレストとは信頼する側のフォレストからユーザーを認証する、フェデレーション サーバーを使用するフォレスト内の任意のドメインに参加するまず必要があります。|![フェデレーション サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[コンピューターをドメインに参加させる](Join-a-Computer-to-a-Domain.md)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|企業ネットワークのフェデレーション サーバーの DNS ホスト名をフェデレーション サーバーの IP アドレスを指す DNS で新しいリソース レコードを作成します。|![フェデレーション サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[ホスト (&) #40; を追加A & #41 です。リソース レコードを会社の DNS にフェデレーション サーバーに](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|\(Optional\) フェデレーション サーバー、フェデレーション サーバー ファームに追加する場合、まず既存 token\ 署名証明書の秘密キーをエクスポートする必要があります \ (、最初のフェデレーション サーバーで、farm\) ファイル形式の証明書の準備ができるようにと他のフェデレーション サーバー必要があります、同じ証明書をインポートします。<br /><br />秘密キーをエクスポートする場合は必要ありません、発行されたサーバー認証証明書は、複数のコンピューターで再利用できます \ (なしする必要がある) 場合したは取得して、ファーム内の各フェデレーション サーバーの一意のサーバー認証証明書またはします。 **注:**の AD FS 管理スナップインは、サービス通信証明書としてフェデレーション サーバーのサーバー認証証明書を指します。|![フェデレーション サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[サーバー認証証明書の秘密キー部分のエクスポート](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|サーバー認証証明書を取得した後 \(or private key\) 証明機関から \(CA\)、する必要がありますし、ファイルをインポートする証明書の各フェデレーション サーバーの既定の Web サイトにします。 **注:** AD FS フェデレーション サーバー構成ウィザードを使用する前に、要件は、既定の Web サイトにこの証明書をインストールします。|![フェデレーション サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[サーバー認証証明書を既定の Web サイトにインポートします。](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|\(Optional\) CA からサーバー認証証明書を取得するのに代わりに、フェデレーション サーバーの証明書のサンプルを作成するのにインターネット インフォメーション サービス \(IIS\) を使用することができます。 **注意:**自己署名のサーバー認証証明書を使用して実稼働環境でフェデレーション サーバーを展開するセキュリティのベスト プラクティスではありません。|![フェデレーション サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS: Self\-Signed サーバー証明書を作成する](https://go.microsoft.com/fwlink/?LinkID=108271)し、手順を完了[サーバー認証証明書を既定の Web サイトにインポートします。](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|アカウント パートナー組織のフェデレーション サーバー ファーム環境を構成する場合は、作成して、Active Directory Domain Services \(AD DS\) ファームがあるし、このアカウントを使用して、ファーム内の各フェデレーション サーバーを構成する場所で専用のサービス アカウントを構成する必要があります。 この手順を実行して、Windows 統合認証を使用して、ファーム内のフェデレーション サーバーのいずれかへの認証に企業ネットワークでクライアントを許可します。|![フェデレーション サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーション サーバー ファームのサービス アカウントを手動で構成します。](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーション サーバーとなるコンピューターにフェデレーション サービス役割サービスをインストールします。|![フェデレーション サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーション サービス役割サービスのインストール](Install-the-Federation-Service-Role-Service.md)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|AD FS フェデレーション サーバー構成ウィザードを使用してフェデレーション サーバーの役割で動作するコンピューターで AD FS ソフトウェアを構成します。<br /><br />スタンドアロンのフェデレーション サーバーのセットアップ、新しいファームに最初のフェデレーション サーバーを作成またはコンピューターを既存のフェデレーション サーバー ファームに参加するときに、この手順に従います。 **注:**フェデレーション Web の単一 Sign\-On \(SSO\) 設計では、アカウント パートナー組織内の少なくとも 1 つのフェデレーション サーバーと、リソース パートナー組織内の少なくとも 1 つのフェデレーション サーバーをいる必要があります。|![フェデレーション サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[スタンドアロン フェデレーション サーバーを作成します。](Create-a-Stand-Alone-Federation-Server.md)<br /><br />![フェデレーション サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーション サーバー ファームに最初のフェデレーション サーバーを作成します。](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)<br /><br />![フェデレーション サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーション サーバー ファームにフェデレーション サーバーを追加](Add-a-Federation-Server-to-a-Federation-Server-Farm.md)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|\(Optional\)、AD FS 管理スナップインを追加し、必要な AD FS 証明書を構成するために必要な設計を展開します。 詳細については、スナップインを使用して証明書の変更を追加するときに、次を参照してください。[フェデレーション サーバーの証明書要件](https://technet.microsoft.com/library/dd807040.aspx)します。|![フェデレーション サーバーのセットアップ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[トークン署名証明書の追加](Add-a-Token-Signing-Certificate.md)<br /><br />![フェデレーション サーバーのセットアップ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[トークン暗号化解除証明書の追加](Add-a-Token-Decrypting-Certificate.md)<br /><br />![フェデレーション サーバーのセットアップ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[サービス通信証明書の設定](Set-a-Service-Communications-Certificate.md)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|これは、組織内の最初のフェデレーション サーバーである場合、AD FS の設計に適合するよう、フェデレーション サービスを構成します。|![フェデレーション サーバーのセットアップ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: アカウント パートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)<br /><br />![フェデレーション サーバーのセットアップ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: リソース パートナー組織の構成](Checklist--Configuring-the-Resource-Partner-Organization.md)|  
|![フェデレーション サーバーのセットアップ](media/icon_checkboxo.gif)|クライアント コンピューターからフェデレーション サーバーが動作可能であることを確認します。|![フェデレーション サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[いることを確認、フェデレーション サーバーが正常に動作](Verify-That-a-Federation-Server-Is-Operational.md)| 
