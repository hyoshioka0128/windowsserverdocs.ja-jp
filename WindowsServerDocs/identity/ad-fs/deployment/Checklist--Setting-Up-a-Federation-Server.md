---
ms.assetid: 8f954004-40d5-4c5e-8e0d-e8700c8ec7b1
title: チェックリストのフェデレーション サーバーを設定します。
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d46fc3246ed6ead54d58f44aaed0e8863ea189a6
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192338"
---
# <a name="checklist-setting-up-a-federation-server"></a>チェックリスト:フェデレーション サーバーのセットアップ

このチェックリストには、Active Directory フェデレーション サービスでフェデレーション サーバーの役割を Windows Server® 2012 を実行するサーバーを準備するために必要な展開タスクが含まれています。 \(AD FS\)します。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![フェデレーション サーバーを設定する](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト。フェデレーション サーバーを設定します。**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|AD FS フェデレーション サーバーを展開する前に、次のように確認してください。1.\)か Windows Internal Database を選択することの長所と短所\(WID\)や 2 AD FS 構成データベースを格納する SQL Server。\)AD FS 展開トポロジの種類と関連付けられているサーバーの配置とネットワーク レイアウトの推奨します。|![フェデレーション サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジの決定](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![フェデレーション サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジに関する考慮事項](https://technet.microsoft.com/library/gg982489.aspx)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|実稼働環境で使用する必要がありますのフェデレーション サーバーの適切な数を決定する AD FS キャパシティ プランニング ガイダンスを確認します。|![フェデレーション サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバーのキャパシティ プランニング](https://technet.microsoft.com/library/gg749917.aspx)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|AD FS の設計ガイドで、組織内のフェデレーション サーバーを配置する場所に関する情報を確認してください。|![フェデレーション サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバーの配置の計画](https://technet.microsoft.com/library/dd807069.aspx)<br /><br />![フェデレーション サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバーを配置する場所](https://technet.microsoft.com/library/dd807127.aspx)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|スタンドアロンかどうかを判断\-フェデレーション サーバーまたはフェデレーション サーバー ファームを単独では、展開に適しています。|![フェデレーション サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバーを作成する場合](https://technet.microsoft.com/library/dd807101.aspx)<br /><br />![フェデレーション サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバー ファームを作成する場合](https://technet.microsoft.com/library/dd807062.aspx)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|アカウント パートナー組織内、またはリソース パートナー組織でこの新しいフェデレーション サーバーが作成するかどうかを決定します。|![フェデレーション サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[アカウント パートナーのフェデレーション サーバーの役割を確認します。](https://technet.microsoft.com/library/dd807117.aspx)<br /><br />![フェデレーション サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[リソース パートナーのフェデレーション サーバーの役割を確認します。](https://technet.microsoft.com/library/dd807065.aspx)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|フェデレーション サーバーでのサービス通信証明書とトークンの使用方法に関する情報を確認\-署名証明書を安全にクライアントとフェデレーション サーバー プロキシの要求を認証します。 **注:** Https などの非修飾ホスト名で証明書を使用する一般的な方法は長いも:\/\/myserver、これらの証明書セキュリティの値がない場合や、攻撃者の権限を借用するには、AD FS フェデレーション サービスを有効にすることができますエンタープライズ クライアント。 完全修飾ドメイン名を使用することを推奨はそのため、 \(FQDN\) https など:\/\/myserver.contoso.com とのみ使用して SSL 証明書、フェデレーション サービスの FQDN に発行します。|![フェデレーション サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|企業ネットワークのドメイン ネーム システムを更新する方法についての情報を確認して\(DNS\)フェデレーション サーバーに正常な名前解決が行われるようにします。|![フェデレーション サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバーの名前解決の要件](https://technet.microsoft.com/library/dd807041.aspx)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|アカウント パートナー フォレストまたはフォレストを信頼するかそのフォレストのユーザーの認証に使用、リソース パートナー フォレスト内のドメインをフェデレーション サーバーとなるコンピューターを参加させます。 **注:** アカウント パートナー組織内のフェデレーション サーバーを設定する場合は、コンピューターをまたはフォレストを信頼する側のフォレストからユーザーを認証するフェデレーション サーバーを使用、フォレスト内のドメインに参加して最初にする必要があります。|![フェデレーション サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[コンピューターをドメインに参加させる](Join-a-Computer-to-a-Domain.md)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|企業ネットワークのフェデレーション サーバーの IP アドレスにフェデレーション サーバーの DNS ホスト名を指す DNS の新しいリソース レコードを作成します。|![フェデレーション サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[ホストを追加する&#40;A&#41;をフェデレーション サーバーの会社の DNS リソース レコード](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|\(省略可能な\)フェデレーション サーバー ファームにフェデレーション サーバーを追加する場合は、まず既存のトークンの秘密キーをエクスポートする必要があります\-署名証明書\(、ファーム内の最初のフェデレーションサーバー\)準備完了の証明書のファイル形式があるようにと他のフェデレーション サーバーする必要があります、同じ証明書をインポートします。<br /><br />秘密キーをエクスポートする場合は必要ありません、発行済みのサーバー認証証明書は、複数のコンピューターで再利用できる\(をエクスポートすることがなく\)の一意のサーバー認証証明書を取得するとき、またはファームの各フェデレーション サーバー。 **注:** AD FS 管理スナップイン\-サービス通信証明書としてフェデレーション サーバーのサーバー認証証明書を参照しています。|![フェデレーション サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[サーバー認証証明書の秘密キー部分のエクスポート](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|サーバー認証証明書を取得した後\(または秘密キー\)証明機関から\(CA\)、各フェデレーション サーバーの既定の Web サイトに証明書ファイルをインポートする必要があります。 **注:** AD FS フェデレーション サーバー構成ウィザードを使用する前に、既定の Web サイトにこの証明書をインストールするが必要です。|![フェデレーション サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[既定の Web サイトにサーバー認証証明書のインポート](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|\(省略可能な\)インターネット インフォメーション サービスを使用する CA からサーバー認証証明書を取得する代わりに、 \(IIS\)サンプルで、フェデレーション サーバーの証明書を作成します。 **注:** 自己を使用して、運用環境でのフェデレーション サーバーを展開するセキュリティのベスト プラクティスではない\-サーバー認証証明書に署名します。|![フェデレーション サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS:自動作成\-サーバー証明書の署名](https://go.microsoft.com/fwlink/?LinkID=108271)と手順を完了して[既定の Web サイトにサーバー認証証明書をインポート](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|アカウント パートナー組織でフェデレーション サーバー ファーム環境を構成して作成し、Active Directory Domain Services の専用のサービス アカウントを構成する必要があります\(AD DS\)ファームが存在し、このアカウントを使用して、ファーム内の各フェデレーション サーバーを構成します。 この手順を実行するには Windows 統合認証を使用して、ファーム内のフェデレーション サーバーのいずれかの認証に企業ネットワークでクライアントはできます。|![フェデレーション サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーション サーバー ファームのサービス アカウントを手動で構成](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|フェデレーション サーバーになるコンピューターには、フェデレーション サービスの役割サービスをインストールします。|![フェデレーション サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーション サービスの役割のインストール](Install-the-Federation-Service-Role-Service.md)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|AD FS フェデレーション サーバー構成ウィザードを使用して、フェデレーション サーバーの役割で動作するコンピューターの AD FS ソフトウェアを構成します。<br /><br />この手順で、スタンドアロンを設定する場合に\-単独でフェデレーション サーバーで、新しいファームに最初のフェデレーション サーバーを作成または既存のフェデレーション サーバー ファームにコンピューターを参加させます。 **注:** フェデレーション Web シングル サインオン\-で\(SSO\)デザイン、アカウント パートナー組織内の少なくとも 1 つのフェデレーション サーバーとリソース パートナー組織内の少なくとも 1 つのフェデレーション サーバーが必要です。|![フェデレーション サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[スタンドアロン フェデレーション サーバーの作成](Create-a-Stand-Alone-Federation-Server.md)<br /><br />![フェデレーション サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーション サーバー ファーム内の最初のフェデレーション サーバーの作成](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)<br /><br />![フェデレーション サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーション サーバー ファームにフェデレーション サーバーを追加](Add-a-Federation-Server-to-a-Federation-Server-Farm.md)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|\(省略可能な\)AD FS 管理スナップインを使用して、\-のロックを追加し、設計を展開するために必要なために必要な AD FS 証明書を構成します。 追加または変更する証明書、スナップインを使用するタイミングの詳細については\-で、次を参照してください。 [Certificate Requirements for Federation Servers](https://technet.microsoft.com/library/dd807040.aspx)します。|![フェデレーション サーバーを設定する](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[トークン署名証明書の追加](Add-a-Token-Signing-Certificate.md)<br /><br />![フェデレーション サーバーを設定する](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[トークン暗号化解除証明書の追加](Add-a-Token-Decrypting-Certificate.md)<br /><br />![フェデレーション サーバーを設定する](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[サービス通信証明書の設定](Set-a-Service-Communications-Certificate.md)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|組織内の最初のフェデレーション サーバーの場合は、AD FS 設計に準拠しているように、フェデレーション サービスを構成します。|![フェデレーション サーバーを設定する](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。アカウント パートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)<br /><br />![フェデレーション サーバーを設定する](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。リソース パートナー組織の構成](Checklist--Configuring-the-Resource-Partner-Organization.md)|  
|![フェデレーション サーバーを設定します。](media/icon_checkboxo.gif)|クライアント コンピューターから、フェデレーション サーバーの操作を確認します。|![フェデレーション サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[いることを確認、フェデレーション サーバーが正常に動作](Verify-That-a-Federation-Server-Is-Operational.md)| 
