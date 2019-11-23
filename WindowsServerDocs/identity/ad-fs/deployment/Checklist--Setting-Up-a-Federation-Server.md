---
ms.assetid: 8f954004-40d5-4c5e-8e0d-e8700c8ec7b1
title: チェックリスト-フェデレーションサーバーのセットアップ
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8fed51679ecabd883cfdcdf01523e123a1ca5243
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408513"
---
# <a name="checklist-setting-up-a-federation-server"></a>チェックリスト: フェデレーション サーバーのセットアップ

このチェックリストには、Active Directory フェデレーションサービス (AD FS) \(AD FS\)のフェデレーションサーバーの役割用に、Windows Server®2012を実行しているサーバーを準備するために必要な展開タスクが含まれています。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
フェデレーションサーバーのセットアップの ![](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: フェデレーションサーバーの**セットアップ  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|AD FS フェデレーションサーバーのデプロイを開始する前に、「」を確認してください。1. Windows Internal Database \(WID\) または SQL Server を選択して、AD FS 構成データベース2を格納するという\) の長所と短所があります。\) AD FS 展開トポロジの種類と、それに関連付けられているサーバーの配置とネットワークレイアウトに関する推奨事項を紹介します。|フェデレーションサーバーのセットアップ ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS の展開トポロジを決定](https://technet.microsoft.com/library/gg982491.aspx)する<br /><br />フェデレーションサーバーのセットアップ ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジに関する考慮事項](https://technet.microsoft.com/library/gg982489.aspx)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|AD FS 容量計画のガイダンスを確認して、運用環境で使用する必要があるフェデレーションサーバーの適切な数を決定します。|フェデレーションサーバーをセットアップする ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバーの容量を計画](https://technet.microsoft.com/library/gg749917.aspx)する|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|組織内のフェデレーションサーバーを配置する場所について AD FS 設計ガイドの情報を確認する|フェデレーションサーバーをセットアップする ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバーの配置を計画](https://technet.microsoft.com/library/dd807069.aspx)する<br /><br />フェデレーションサーバーを](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[配置する](https://technet.microsoft.com/library/dd807127.aspx)フェデレーションサーバーのセットアップ ![|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|\-スタンドアロンのフェデレーションサーバーまたはフェデレーションサーバーファームが展開に適しているかどうかを判断します。|フェデレーションサーバーを](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[作成するとき](https://technet.microsoft.com/library/dd807101.aspx)にフェデレーションサーバーをセットアップ ![には<br /><br />](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバーファームを作成する場合](https://technet.microsoft.com/library/dd807062.aspx)のフェデレーションサーバーのセットアップ ![|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|この新しいフェデレーションサーバーが、アカウントパートナー組織とリソースパートナー組織のどちらに作成されるかを決定します。|フェデレーションサーバーのセットアップ ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[アカウントパートナー内のフェデレーションサーバーの役割を確認する](https://technet.microsoft.com/library/dd807117.aspx)<br /><br />フェデレーションサーバーのセットアップ ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[リソースパートナー内のフェデレーションサーバーの役割を確認する](https://technet.microsoft.com/library/dd807065.aspx)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーションサーバーがサービス通信証明書とトークン\-署名証明書を使用して、クライアントとフェデレーションサーバーのプロキシ要求を安全に認証する方法に関する情報を確認します。 **注意:** Https:\/\/myserver など、修飾されていないホスト名を持つ証明書を使用するのはかなりの時間ですが、これらの証明書にはセキュリティ値がないため、攻撃者はエンタープライズクライアントに AD FS フェデレーションサービスを偽装することができます。 そのため、完全修飾ドメイン名を使用することをお勧めします。 \(FQDN\) (https:\/\/myserver.contoso.com など)、フェデレーションサービスの FQDN に発行された SSL 証明書のみを使用することをお勧めします。|フェデレーションサーバーのフェデレーションサーバー](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)を設定 ![には|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーションサーバーへの名前解決が正常に行われるように、企業ネットワークのドメインネームシステム \(DNS\) を更新する方法についての情報を確認します。|フェデレーションサーバーのフェデレーションサーバー](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の名前解決要件](https://technet.microsoft.com/library/dd807041.aspx)を設定 ![には|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーションサーバーにするコンピューターを、アカウントパートナーフォレストまたはリソースパートナーフォレスト内のドメインに参加させます。このドメインは、そのフォレストのユーザーの認証に使用されるか、または信頼する側のフォレストによって認証されます。 **注:** アカウントパートナー組織でフェデレーションサーバーをセットアップする場合は、まず、そのコンピューターをフォレスト内の任意のドメインに参加させる必要があります。この場合、フェデレーションサーバーを使用して、そのフォレストのユーザーや信頼する側のフォレストからユーザーを認証します。|フェデレーションサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[コンピューターのドメインへの参加](Join-a-Computer-to-a-Domain.md)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーションサーバーの DNS ホスト名をフェデレーションサーバーの IP アドレスに指す、企業ネットワークの DNS に新しいリソースレコードを作成します。|フェデレーションサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバーの企業&#40;DNS&#41;にリソースレコードを追加](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)する|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|\(オプション\) フェデレーションサーバーをフェデレーションサーバーファームに追加する場合は、最初に既存のトークンの秘密キー\-署名証明書\) \(をエクスポートする必要があります。これにより、他のフェデレーションサーバーが同じ証明書をインポートする必要がある場合に証明書のファイル形式を使用できるようになります。<br /><br />発行されたサーバー認証証明書が複数の \(コンピューターで再利用される場合は、\) をエクスポートする必要がなく、ファーム内の各フェデレーションサーバーに対して一意のサーバー認証証明書を取得するときに、秘密キーをエクスポートする必要はありません。 **注:** の AD FS 管理スナップ\-は、サービス通信証明書としてのフェデレーションサーバーのサーバー認証証明書を参照します。|フェデレーションサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[サーバー認証証明書の秘密キーの部分をエクスポート](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)する|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|証明機関 \(CA\)からサーバー認証証明書 \(または秘密キー\) を取得した後、各フェデレーションサーバーの既定の Web サイトに証明書ファイルをインポートする必要があります。 **注:** AD FS フェデレーションサーバー構成ウィザードを使用するには、この証明書を既定の Web サイトにインストールする必要があります。|フェデレーションサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[サーバー認証証明書を既定の Web サイトにインポートする](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|\(オプションの\) CA からサーバー認証証明書を取得する代わりに、インターネットインフォメーションサービス \(IIS\) を使用して、フェデレーションサーバーのサンプル証明書を作成することができます。 **注意:** 自己\-署名付きサーバー認証証明書を使用して運用環境にフェデレーションサーバーを展開することは、セキュリティのベストプラクティスではありません。|フェデレーションサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS: 自己\-署名されたサーバー証明書を作成](https://go.microsoft.com/fwlink/?LinkID=108271)し、「[サーバー認証証明書を既定の Web サイトにインポートする](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)」の手順を完了します。|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|アカウントパートナー組織でフェデレーションサーバーファーム環境を構成する場合は、ファームが存在する Active Directory Domain Services \(\) AD DS で専用のサービスアカウントを作成して構成し、このアカウントを使用するようにファーム内の各フェデレーションサーバーを構成する必要があります。 この手順を実行すると、企業ネットワーク上のクライアントは、Windows 統合認証を使用して、ファーム内の任意のフェデレーションサーバーに対して認証を行うことができます。|フェデレーションサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバーファームのサービスアカウントを手動で構成する](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーションサーバーとなるコンピューターにフェデレーションサービスの役割サービスをインストールします。|フェデレーションサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサービスの役割サービスをインストール](Install-the-Federation-Service-Role-Service.md)する|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|AD FS フェデレーションサーバー構成ウィザードを使用して、フェデレーションサーバーの役割で動作するようにコンピューターの AD FS ソフトウェアを構成します。<br /><br />スタンド\-アロンのフェデレーションサーバーをセットアップする場合、新しいファームに最初のフェデレーションサーバーを作成する場合、または既存のフェデレーションサーバーファームにコンピューターを参加させる場合は、次の手順に従います。 **注:** \(SSO\) 設計でフェデレーション Web シングルサイン\-を使用するには、アカウントパートナー組織に少なくとも1つのフェデレーションサーバーがあり、リソースパートナー組織に少なくとも1つのフェデレーションサーバーが必要です。|フェデレーションサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[スタンドアロンフェデレーションサーバーを作成](Create-a-Stand-Alone-Federation-Server.md)する<br /><br />フェデレーションサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバーファームに最初のフェデレーションサーバーを作成](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)する<br /><br />フェデレーションサーバーのセットアップ ![フェデレーションサーバーを](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバーファームに追加する](Add-a-Federation-Server-to-a-Federation-Server-Farm.md)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|オプション\) \(は、の AD FS 管理スナップ\-を使用して、設計を展開するために必要な AD FS 証明書を追加して構成します。 のスナップ\-を使用して証明書を追加または変更する場合の詳細については、「[フェデレーションサーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)」を参照してください。|フェデレーションサーバーのセットアップ ![](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[トークン署名証明書の追加](Add-a-Token-Signing-Certificate.md)<br /><br />フェデレーションサーバーのセットアップ ![](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[トークン暗号化解除証明書の追加](Add-a-Token-Decrypting-Certificate.md)<br /><br />フェデレーションサーバーのセットアップ ![](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[サービス通信証明書の設定](Set-a-Service-Communications-Certificate.md)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|これが組織内の最初のフェデレーションサーバーである場合は、AD FS の設計に準拠するようにフェデレーションサービスを構成します。|フェデレーションサーバーのセットアップの ![](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: アカウントパートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)<br /><br />フェデレーションサーバーのセットアップの ![](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: リソースパートナー組織の構成](Checklist--Configuring-the-Resource-Partner-Organization.md)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|クライアントコンピューターから、フェデレーションサーバーが動作可能であることを確認します。|フェデレーションサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバーが動作していることを確認する](Verify-That-a-Federation-Server-Is-Operational.md)| 
