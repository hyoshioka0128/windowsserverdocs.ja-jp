---
ms.assetid: c20231dd-2b83-4494-9385-1172272e00d6
title: 既存のドメインをアップグレードするか新しいドメインを展開するかを決定する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e07965b079a953d062f5bdaaca8f9f9f32500610
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851793"
---
# <a name="determining-whether-to-upgrade-existing-domains-or-deploy-new-domains"></a>既存のドメインをアップグレードするか新しいドメインを展開するかを決定する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

設計上の各ドメインは、新しいドメインになります。 または既存のドメインをアップグレードします。 アップグレードしない既存のドメインのユーザーは、新しいドメインに移動する必要があります。  
  
ドメイン間でアカウントを移動するとエンドユーザーに影響を与えることができます。 新しいドメインへのユーザーの移動や、既存のドメインをアップグレードするかどうかを決定するには、前に、ドメインにユーザーの移動のコストと新しい AD DS ドメインの長期的な管理上の利点を評価します。  
  
Active Directory ドメインを Windows Server 2008 にアップグレードする方法の詳細については、次を参照してください。[を Windows Server 2008 および Windows Server 2008 R2 の AD DS ドメインの Active Directory ドメインのアップグレード](https://technet.microsoft.com/library/cc731188.aspx)します。  
  
AD DS ドメイン内およびフォレスト間での再構築の詳細については、Active Directory 移行ツール バージョン 3.1 を参照してください。 移行ガイド ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678))。  
  
新規とアップグレード ドメインの計画を文書化するために、ワークシートでは、ジョブ エイドの Windows Server 2003 展開キットから Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip をダウンロードして ([ https://go.microsoft.com/fwlink/?LinkID=102558 ](https://go.microsoft.com/fwlink/?LinkID=102558))「ドメイン計画」(DSSLOGI_5.doc) を開きます。  
  


