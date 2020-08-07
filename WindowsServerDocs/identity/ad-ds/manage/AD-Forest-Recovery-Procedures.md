---
title: AD フォレストの回復 - 手順
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 47a471fb-3b0b-4aa8-8525-1c92d0d51e93
ms.openlocfilehash: c59990486da26847884aec3052818bce1ebe450d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969859"
---
# <a name="ad-forest-recovery---procedures"></a>AD フォレストの回復 - 手順

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

このセクションでは、フォレストの回復プロセスに関連する手順について説明します。 これらの手順は、Windows Server 2016、2012 R2、2012に適用されます。また、Windows Server 2008 R2 および2008にも適用できますが、いくつかの小さな例外があります。

Windows server 2003 で異なる手順を含む手順については、「 [Windows server 2003 を使用](AD-Forest-Recovery-Windows-Server-2003.md)したフォレストの回復」を参照してください。

次に、ドメインコントローラーと Active Directory のバックアップと復元に使用される手順の一覧を示します。

- [フルサーバーのバックアップ](AD-Forest-Recovery-Backing-up-a-Full-Server.md)
- [システム状態データのバックアップ](AD-Forest-Recovery-Backing-up-System-State.md)
- [サーバーの完全復旧を実行する](AD-Forest-Recovery-Perform-a-Full-Recovery.md)
- [DFSR によってレプリケートされた SYSVOL の権限のある同期を実行する](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)
- [Active Directory Domain Services の権限のない復元を実行する](AD-Forest-Recovery-Nonauthoritative-Restore.md)

次の手順では、SYSVOL の authoritative restore を同時に実行する方法について説明します。

- [DNS サーバーサービスの構成](AD-Forest-Recovery-Configure-DNS.md)
- [グローバルカタログを削除しています](AD-Forest-Recovery-Remove-GC.md)
- [使用可能な RID プールの値を上げる](AD-Forest-Recovery-Raise-RID-Pool.md)
- [現在の RID プールを無効にします](AD-Forest-Recovery-Invaildate-RID-Pool.md)
- [操作マスタの役割を強制する](AD-Forest-Recovery-Seizing-Operations-Master-Role.md)
- [復元後のクリーンアップ](AD-Forest-Recovery-Cleanup.md)
- [削除された書き込み可能ドメインコントローラーのメタデータをクリーニングしています](AD-Forest-Recovery-Cleaning-Metadata.md)
- [ドメインコントローラーのコンピューターアカウントのパスワードをリセットしています](AD-Forest-Recovery-Reset-Computer-Account-DC.md)
- [Krbtgt パスワードをリセットしています](AD-Forest-Recovery-Resetting-the-krbtgt-password.md)
- [信頼の1側での信頼されたパスワードのリセット](AD-Forest-Recovery-Reset-Trust.md)
- [グローバルカタログを追加しています](AD-Forest-Recovery-Add-GC.md)
- [レプリケーションが機能していることを確認するためのリソース](AD-Forest-Recovery-Verify-Replication.md)

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復 - 前提条件](AD-Forest-Recovery-Prerequisties.md)
- [AD フォレストの回復-カスタムフォレストの復旧計画の作成](AD-Forest-Recovery-Devising-a-Plan.md)
- [AD フォレストの回復-問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD フォレストの回復-回復方法を決定する](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD フォレストの回復-最初の回復を実行する](AD-Forest-Recovery-Perform-initial-recovery.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
- [AD フォレストの回復-よく寄せられる質問](AD-Forest-Recovery-FAQ.md)
- [AD フォレストの回復-マルチドメインフォレスト内の単一ドメインの回復](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)
- [AD フォレストの回復-Windows Server 2003 ドメインコントローラーを使用したフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md)
