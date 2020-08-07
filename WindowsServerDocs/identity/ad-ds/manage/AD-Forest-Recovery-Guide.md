---
ms.assetid: 680e05ac-f9be-4b07-a9f4-cd6da5835952
title: Active Directory フォレストの回復ガイド
description: このガイドでは、バックアップ、復元、および active directory ディザスターリカバリーに関するガイダンスを提供します。
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.openlocfilehash: bf8356f49ce505db053ec37c6a91e4f8bccb8ac1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969909"
---
# <a name="active-directory-forest-recovery-guide"></a>Active Directory フォレストの回復ガイド

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2、Windows Server 2003

このガイドでは、フォレスト全体で障害が発生した場合に、フォレスト内のすべてのドメインコントローラー (Dc) が正常に機能しなくなった場合に Active Directory®フォレストを回復するためのベストプラクティスについて説明します。 ここで説明する手順は、特定の環境に合わせてカスタマイズできる、フォレストの復旧計画のテンプレートとして機能します。 これらの手順は、Microsoft® Windows Server 2016、2012 R2、2012、2008 R2、2008、および2003オペレーティングシステムを実行する Dc に適用されます。

> [!NOTE]
> Windows Server 2003 を実行している Dc に固有の手順は、 [AD フォレストの回復 Windows server 2003](AD-Forest-Recovery-Windows-Server-2003.md)に統合されています。

## <a name="steps-outlined-in-this-guide"></a>このガイドで説明されている手順

- [AD フォレストの回復 - 前提条件](AD-Forest-Recovery-Prerequisties.md)
- [AD フォレストの回復-カスタムフォレストの復旧計画の作成](AD-Forest-Recovery-Devising-a-Plan.md)
- [AD フォレストの回復 - 回復の手順](AD-Forest-Recovery-Steps-For-Restoring.md)
- [AD フォレストの回復-問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD フォレストの回復-回復方法を決定する](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD フォレストの回復-最初の回復を実行する](AD-Forest-Recovery-Perform-initial-recovery.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
- [AD フォレストの回復-よく寄せられる質問](AD-Forest-Recovery-FAQ.md)
- [AD フォレストの回復-マルチドメインフォレスト内の単一ドメインの回復](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)
- [AD フォレストの回復 - 仮想化](AD-Forest-Recovery-Virtualization.md)
- [AD フォレストの回復-Windows Server 2003 ドメインコントローラーを使用したフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md)
