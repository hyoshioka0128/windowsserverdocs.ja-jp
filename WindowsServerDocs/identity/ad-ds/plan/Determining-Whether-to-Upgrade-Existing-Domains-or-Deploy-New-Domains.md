---
ms.assetid: c20231dd-2b83-4494-9385-1172272e00d6
title: 既存のドメインをアップグレードするか新しいドメインを展開するかを決定する
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 7064a3ef4735d88051a91390089549d4a3eba613
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87943086"
---
# <a name="determining-whether-to-upgrade-existing-domains-or-deploy-new-domains"></a>既存のドメインをアップグレードするか新しいドメインを展開するかを決定する

> 適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

設計内の各ドメインは、新しいドメインか、または既存のアップグレードされたドメインになります。 アップグレードしていない既存のドメインのユーザーは、新しいドメインに移動する必要があります。

ドメイン間でアカウントを移動すると、エンドユーザーに影響が及ぶ可能性があります。 ユーザーを新しいドメインに移動するか、既存のドメインをアップグレードするかを決定する前に、新しい AD DS ドメインの長期的な管理上の利点を、ユーザーをドメインに移動するコストと比較して評価してください。

Active Directory ドメインを Windows Server 2008 にアップグレードする方法の詳細については、「 [Active Directory ドメインを Windows server 2008 および Windows server 2008 R2 AD DS ドメインにアップグレードする](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731188(v=ws.10))」を参照してください。

フォレスト内およびフォレスト間の AD DS ドメインの再構築の詳細については、「 [ADMT Guide: Active Directory ドメインの移行と再構築](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc974332(v=ws.10))」を参照してください。

新規およびアップグレードされたドメインの計画を文書化するためのワークシートについては、「 [Windows Server 2003 Deployment Kit のジョブエイド](https://microsoft.com/download/details.aspx?id=9608)」から Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip をダウンロードし、「ドメイン計画」 (DSSLOGI_5.doc) を開いてください。
