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
# <a name="checklist-setting-up-a-federation-server"></a>チェックリスト:フェデレーション サーバーのセットアップ

このチェックリストには、Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 のフェデレーションサーバーの役割用に、Windows Server®2012を実行しているサーバーを準備するために必要な展開タスクが含まれています。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)** フェデレーションサーバーのセットアップ @ no__t-1Checklist リスト:フェデレーションサーバーのセットアップ @ no__t-0  
  
||タスク|参照|  
|-|--------|-------------|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|AD FS フェデレーションサーバーのデプロイを開始する前に、「」を確認してください。1. \) AD FS 構成データベースを格納するための Windows Internal Database \(WID @ no__t-2 または SQL Server を選択した場合の長所と短所。 \)AD FS 展開トポロジの種類と、それに関連付けられているサーバーの配置とネットワークレイアウトに関する推奨事項。|つのフェデレーションサーバーをセットアップする](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS の展開トポロジを決定](https://technet.microsoft.com/library/gg982491.aspx)する<br /><br />つのフェデレーションサーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジに関する考慮事項](https://technet.microsoft.com/library/gg982489.aspx)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|AD FS 容量計画のガイダンスを確認して、運用環境で使用する必要があるフェデレーションサーバーの適切な数を決定します。|つのフェデレーションサーバーをセットアップする](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバーの容量を計画](https://technet.microsoft.com/library/gg749917.aspx)する|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|組織内のフェデレーションサーバーを配置する場所について AD FS 設計ガイドの情報を確認する|つのフェデレーションサーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバーの配置の計画](https://technet.microsoft.com/library/dd807069.aspx)<br /><br />@no__t: フェデレーションサーバーを](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[配置する](https://technet.microsoft.com/library/dd807127.aspx)フェデレーションサーバーをセットアップする|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|スタンドアロンのフェデレーションサーバーまたはフェデレーションサーバーファームが展開に適しているかどうかを判断します。|@no__t: フェデレーションサーバーを](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[作成するとき](https://technet.microsoft.com/library/dd807101.aspx)にフェデレーションサーバーをセットアップする<br /><br />@no__t:](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバーファームを作成する場合](https://technet.microsoft.com/library/dd807062.aspx)のフェデレーションサーバーのセットアップ|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|この新しいフェデレーションサーバーが、アカウントパートナー組織とリソースパートナー組織のどちらに作成されるかを決定します。|つのフェデレーションサーバーをセットアップする](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[アカウントパートナー内のフェデレーションサーバーの役割を確認する](https://technet.microsoft.com/library/dd807117.aspx)<br /><br />つのフェデレーションサーバー](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[のセットアップリソースパートナー内のフェデレーションサーバーの役割を確認](https://technet.microsoft.com/library/dd807065.aspx)する|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーションサーバーがサービス通信証明書とトークン @ no__t-0signing 証明書を使用して、クライアントとフェデレーションサーバーのプロキシ要求を安全に認証する方法に関する情報を確認します。 **注:** たとえば、https: \/ @ no__t-1myserver のような非修飾ホスト名を持つ証明書を使用するのは一般的な方法ですが、これらの証明書にはセキュリティ値がないため、攻撃者は、AD FS のフェデレーションサービスをエンタープライズクライアントになりすますことができます. このため、https: \/\/myserver.contoso.com などの完全修飾ドメイン名 @no__t 0FQDN @ no__t-1 を使用し、フェデレーションサービスの FQDN に発行された SSL 証明書のみを使用することをお勧めします。|![setting server のフェデレーションサーバー](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)を設定する|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|企業ネットワークのドメインネームシステム \(DNS @ no__t-1 を更新して、フェデレーションサーバーへの名前解決が正常に行われるようにする方法に関する情報を確認します。|![setting server のフェデレーションサーバー](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の名前解決要件](https://technet.microsoft.com/library/dd807041.aspx)を設定する|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーションサーバーにするコンピューターを、アカウントパートナーフォレストまたはリソースパートナーフォレスト内のドメインに参加させます。このドメインは、そのフォレストのユーザーの認証に使用されるか、または信頼する側のフォレストによって認証されます。 **注:** アカウントパートナー組織でフェデレーションサーバーをセットアップする場合は、まず、そのコンピューターをフォレスト内の任意のドメインに参加させる必要があります。この場合、フェデレーションサーバーを使用して、そのフォレストのユーザーや信頼する側のフォレストからユーザーを認証します。|つのフェデレーションサーバーをセットアップして](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[コンピューターをドメインに参加させる](Join-a-Computer-to-a-Domain.md)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーションサーバーの DNS ホスト名をフェデレーションサーバーの IP アドレスに指す、企業ネットワークの DNS に新しいリソースレコードを作成します。|@no__t: フェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[ホスト&#40;a&#41;リソースレコードをフェデレーションサーバーの企業 DNS に追加する](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|\(Optional @ no__t-1 フェデレーションサーバーをフェデレーションサーバーファームに追加する場合は、最初に、ファームの最初のフェデレーションサーバー上の既存のトークン @ no__t-2signing 証明 @no__t 書の秘密キーをエクスポートする必要があります @ no__t-4他のフェデレーションサーバーが同じ証明書をインポートする必要がある場合は、証明書のファイル形式を準備します。<br /><br />発行されたサーバー認証証明書を複数の @no__t コンピューターで再利用する場合は、no__t-1 をエクスポートする必要がないか、またはそれぞれに対して一意のサーバー認証証明書を取得するときに、秘密キーをエクスポートする必要はありません。ファーム内のフェデレーションサーバー。 **注:** AD FS Management snap @ no__t-0in は、サービス通信証明書としてフェデレーションサーバーのサーバー認証証明書を参照します。|@no__t](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[サーバー認証証明書の秘密キーの部分をエクスポート](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)するフェデレーションサーバーのセットアップ|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|証明機関 \(CA @ no__t からサーバー認証証明書 \(or は秘密キー @ no__t-1 を取得した後、各フェデレーションサーバーの既定の Web サイトに証明書ファイルをインポートする必要があります。 **注:** AD FS フェデレーションサーバー構成ウィザードを使用するには、この証明書を既定の Web サイトにインストールする必要があります。|@no__t、フェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[サーバー認証証明書を既定の Web サイトにインポートする](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|\(Optional @ no__t-1 CA からサーバー認証証明書を取得する代わりに、インターネットインフォメーションサービス \(IIS @ no__t-3 を使用して、フェデレーションサーバーのサンプル証明書を作成できます。 **注:** セキュリティのベストプラクティスとして、自己 @ no__t-0signed 付きサーバー認証証明書を使用して、運用環境にフェデレーションサーバーを展開することは推奨されません。|](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[ フェデレーションサーバーをセットアップする @ no__t-1IIS:自己 @ no__t-0Signed サーバー証明書 @ no__t を作成し、 [「サーバー認証証明書を既定の Web サイトにインポートする](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)」の手順を完了します。|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|アカウントパートナー組織でフェデレーションサーバーファーム環境を構成する場合は、Active Directory Domain Services @no__t 0AD DS @ no__t で専用のサービスアカウントを作成して構成し、ファームが存在し、それぞれを構成する必要があります。このアカウントを使用するファーム内のフェデレーションサーバー。 この手順を実行すると、企業ネットワーク上のクライアントは、Windows 統合認証を使用して、ファーム内の任意のフェデレーションサーバーに対して認証を行うことができます。|つのフェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバーファームのサービスアカウントを手動で構成する](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーションサーバーとなるコンピューターにフェデレーションサービスの役割サービスをインストールします。|![setting サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサービスの役割サービスのインストール](Install-the-Federation-Service-Role-Service.md)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|AD FS フェデレーションサーバー構成ウィザードを使用して、フェデレーションサーバーの役割で動作するようにコンピューターの AD FS ソフトウェアを構成します。<br /><br />スタンドアロンフェデレーションサーバーをセットアップする場合、新しいファームに最初のフェデレーションサーバーを作成する場合、または既存のフェデレーションサーバーファームにコンピューターを参加させる場合は、次の手順に従います。 **注:** @No__t-1SSO @ no__t のフェデレーション Web シングルサインオンの場合は、アカウントパートナー組織に少なくとも1つのフェデレーションサーバーがあり、リソースパートナー組織に少なくとも1つのフェデレーションサーバーが必要です。|台のフェデレーションサーバーをセットアップする](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[スタンドアロンフェデレーションサーバーを作成](Create-a-Stand-Alone-Federation-Server.md)する<br /><br />台のフェデレーションサーバーのセットアップフェデレーションサーバー](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[ファームに最初のフェデレーションサーバーを作成](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)する<br /><br />つのフェデレーションサーバーのセットアップフェデレーションサーバー](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[ファームへのフェデレーションサーバーの追加](Add-a-Federation-Server-to-a-Federation-Server-Farm.md)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|\(Optional @ no__t を使用して、設計のデプロイに必要な AD FS 証明書を追加して構成するには、AD FS 管理スナップインを使用します。 でスナップ @ no__t を使用して証明書を追加または変更する場合の詳細については、「[フェデレーションサーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)」を参照してください。|つのフェデレーションサーバーのセットアップ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[トークン署名証明書の追加](Add-a-Token-Signing-Certificate.md)<br /><br />つのフェデレーションサーバーのセットアップ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[トークン暗号化解除証明書の追加](Add-a-Token-Decrypting-Certificate.md)<br /><br />![ フェデレーションサーバーのセットアップ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[サービス通信証明書の設定](Set-a-Service-Communications-Certificate.md)|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|これが組織内の最初のフェデレーションサーバーである場合は、AD FS の設計に準拠するようにフェデレーションサービスを構成します。|](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[ フェデレーションサーバーのセットアップ @ no__t-1Checklist リスト:アカウントパートナー組織の構成 @ no__t-0<br /><br />](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[ フェデレーションサーバーのセットアップ @ no__t-1Checklist リスト:リソースパートナー組織の構成 @ no__t-0|  
|![フェデレーションサーバーのセットアップ](media/icon_checkboxo.gif)|クライアントコンピューターから、フェデレーションサーバーが動作可能であることを確認します。|つのフェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバーが動作していることを確認する](Verify-That-a-Federation-Server-Is-Operational.md)| 
