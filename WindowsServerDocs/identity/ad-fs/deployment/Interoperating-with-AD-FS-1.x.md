---
ms.assetid: 97999892-29c6-4076-be19-5e5259d8ada6
title: AD FS 1.x との相互運用
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 21f0ef0e3ad77d5ea58e5d3b82da66ce420e5d49
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972149"
---
# <a name="interoperating-with-ad-fs-1x"></a>AD FS 1.x との相互運用

\( \) Windows Server 2012 の Active Directory フェデレーションサービス (AD FS) AD FS &reg; と AD FS 1 の間の相互運用性については、「」をご使用ください。*x*では、組織のニーズに応じて、次の1つ以上のタスクを実行します。

-   Windows Server 2012 と以前のバージョンの AD FS の AD FS 間の相互運用性を計画し、Name ID 要求の種類の詳細について説明します。 詳細については、「 [AD FS 1.x との相互運用性の計画](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678040(v=ws.11))」を参照してください。

-   AD FS 1 で使用できる Windows Server 2012 の AD FS フェデレーションサービスから要求を送信する場合は。*x*フェデレーションサービス、「[チェックリスト: AD FS 1.X フェデレーションサービスに要求を送信するための AD FS の構成](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)」を参照してください。

-   AD FS 1 を実行している Web サーバーでホストされているアプリケーションで使用できる Windows Server 2012 の AD FS フェデレーションサービスから要求を送信する場合。*x*要求に \- 対応する web エージェント、「[チェックリスト: AD FS 1. x 要求に対応する web エージェントに要求を送信するための AD FS の構成](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)」を参照してください。

-   AD FS 1 から要求を送信する場合は。*x*フェデレーションサービス Windows Server 2012 の AD FS フェデレーションサービスによって使用される場合は、「[チェックリスト: AD FS 1.X からの要求を使用するように AD FS を構成](Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)する」を参照してください。

## <a name="differences-between-federation-service-settings"></a>フェデレーションサービス設定の相違点
ほとんどの AD FS 1 です。*x*フェデレーションサービス設定は、Windows Server 2012 設定の AD FS フェデレーションサービスと同様の方法で動作します。一部の設定名が変更されています。 次の表に、AD FS 1 の設定の名前を示します。Windows Server 2012 の AD FS フェデレーションサービスの*x*フェデレーションサービスとそれに相当する名前。

|AD FS 1.x フェデレーションサービス設定|Windows Server 2012 の設定で AD FS フェデレーションサービスと同じです。
|----------------------------------------|----------------------------------------------------------------------------------------------------------
|アカウントパートナー|要求プロバイダー信頼
|リソースパートナー|証明書利用者信頼
|Application|証明書利用者信頼
|Application Properties|証明書利用者信頼のプロパティ
|アプリケーションの URL|証明書利用者識別子と WS \- フェデレーションパッシブエンドポイント URL
|フェデレーションサービス URI|フェデレーション サービスの識別子
|フェデレーションサービスエンドポイント URL|WS \- フェデレーションパッシブエンドポイント URL

## <a name="see-also"></a>参照
[AD FS と AD FS 1. x 相互運用性](https://go.microsoft.com/fwlink/?LinkId=200776)

