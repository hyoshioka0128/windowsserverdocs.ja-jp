---
title: AD フォレストの回復 - 手順
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 47a471fb-3b0b-4aa8-8525-1c92d0d51e93
ms.technology: identity-adds
ms.openlocfilehash: da45e3b20c370a2a37b0eab31a78216434dd60be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827723"
---
# <a name="ad-forest-recovery---procedures"></a>AD フォレストの回復 - 手順

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

このセクションでは、フォレスト回復のプロセスに関連する手順を説明します。 手続きが Windows Server 2016 では、該当する 2012 R2、2012 および Windows Server 2008 R2 および 2008 軽微な例外にも適用されます。

Windows Server 2003 の異なる手順が含まれる手順が記載[Windows Server 2003 ドメイン コント ローラーとフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md)します。  

次にバックアップと復元のドメイン コント ローラーと Active Directory で使用されるプロシージャの一覧を示します。

- [完全なサーバーをバックアップします。](AD-Forest-Recovery-Backing-up-a-Full-Server.md)  
- [システム状態データをバックアップします。](AD-Forest-Recovery-Backing-up-System-State.md)  
- [サーバーの完全回復を実行します。](AD-Forest-Recovery-Perform-a-Full-Recovery.md)  
- [DFSR でレプリケートされた SYSVOL の権限を持つの同期を実行します。](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)
- [Active Directory Domain Services の権限のない状態の復元を実行します。](AD-Forest-Recovery-Nonauthoritative-Restore.md)  

次の手順では、同時に SYSVOL の authoritative restore を実行する方法について説明します。  

- [DNS サーバー サービスを構成します。](AD-Forest-Recovery-Configure-DNS.md)  
- [グローバル カタログを削除します。](AD-Forest-Recovery-Remove-GC.md)  
- [使用可能な RID プールの値を上げる](AD-Forest-Recovery-Raise-RID-Pool.md)  
- [現在の RID プールを無効化](AD-Forest-Recovery-Invaildate-RID-Pool.md)  
- [操作マスターの役割の強制](AD-Forest-Recovery-Seizing-Operations-Master-Role.md)  
- [復元後のクリーンアップ](AD-Forest-Recovery-Cleanup.md)
- [削除された書き込み可能なドメイン コント ローラーのメタデータのクリーニング](AD-Forest-Recovery-Cleaning-Metadata.md)  
- [ドメイン コント ローラーのコンピューター アカウントのパスワードをリセットします。](AD-Forest-Recovery-Reset-Computer-Account-DC.md)  
- [Krbtgt パスワードをリセットします。](AD-Forest-Recovery-Resetting-the-krbtgt-password.md)  
- [信頼関係の 1 つの側での信頼のパスワードをリセットします。](AD-Forest-Recovery-Reset-Trust.md)  
- [グローバル カタログを追加します。](AD-Forest-Recovery-Add-GC.md)  
- [レプリケーションの動作を確認するリソース](AD-Forest-Recovery-Verify-Replication.md)  

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復 - 前提条件](AD-Forest-Recovery-Prerequisties.md)  
- [AD フォレストの回復 - カスタム フォレスト回復の計画を立てる](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD フォレストの回復の問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD フォレストの回復に回復する方法を決定](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD フォレストの回復 - 最初の回復を実行します。](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
- [AD フォレストの回復 - よく寄せられる質問](AD-Forest-Recovery-FAQ.md)  
- [AD フォレストの回復 - Multidomain フォレスト内の 1 つのドメインを回復します。](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [AD フォレストの回復 - Windows Server 2003 ドメイン コント ローラーとフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md) 
