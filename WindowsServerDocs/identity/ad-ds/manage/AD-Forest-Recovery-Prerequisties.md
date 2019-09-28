---
title: Active Directory フォレストの回復を計画するための前提条件
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adds
ms.openlocfilehash: 12c34afc497131bfe6abdc78c636e6d3b784877e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390370"
---
# <a name="active-directory-forest-recovery-prerequisites"></a>Active Directory フォレスト回復の前提条件

>適用先:Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

次のドキュメントでは、フォレストの復旧計画を策定する前、または回復を試みる前に理解しておく必要がある前提条件について説明します。

## <a name="assumptions-for-using-this-guide"></a>このガイドを使用する場合の前提条件

1. Microsoft サポート professional とを使用して作業しました。
   - フォレスト全体の障害の原因を特定します。 このガイドでは、エラーの原因については説明しません。また、エラーを回避するための手順を推奨しません。
   - 考えられる解決策を評価します。  
   - 最後に、Microsoft サポートを使用して、エラーが発生する前の状態にフォレスト全体を復元することが、障害から復旧するための最善の方法です。 多くの場合、フォレストの回復は最後のオプションである必要があります。

2. Active Directory 統合されたドメインネームシステム (DNS) を使用するための Microsoft のベストプラクティスの推奨事項に従っていること。 具体的には、Active Directory ドメインごとに Active Directory 統合 DNS ゾーンが必要です。 
   - そうでない場合でも、このガイドの基本原則を使用してフォレストの回復を実行できます。 ただし、独自の環境に基づいて DNS 回復を行うには、特定の対策を講じる必要があります。 Active Directory 統合 DNS の使用方法の詳細については、「 [Dns インフラストラクチャ設計の作成](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)」を参照してください。

3. このガイドはフォレストの回復に関する一般的なガイドとして使用されていますが、すべてのシナリオについては説明しません。 たとえば、Windows Server 2008 以降では、Windows Server の完全なバージョンである Server Core バージョンがありますが、完全な GUI はありません。 Server Core を実行する Dc だけで構成されるフォレストを回復することは確かですが、このガイドには詳細な手順がありません。 ただし、ここで説明されているガイダンスに基づき、必要なコマンドラインアクションを自分で設計できます。  

> ![!NOTE]
> このガイドの目的はフォレストを回復し、完全な DNS 機能を維持または復元することですが、回復によって、障害が発生する前に構成から変更された DNS 構成が復元される可能性があります。 フォレストが回復した後は、元の DNS 構成に戻すことができます。 このガイドの推奨事項では、AD DS に格納されていない DNS ゾーンがある企業名前空間の他の部分の名前解決を実行するように DNS サーバーを構成する方法については説明しません。  

## <a name="concepts-for-using-this-guide"></a>このガイドを使用するための概念

Active Directory フォレストの回復計画を開始する前に、次のことを理解しておく必要があります。  
  
- 基本的な Active Directory の概念  
- 操作マスターの役割 (フレキシブルシングルマスター操作または FSMO とも呼ばれます) の重要性。 これらのロールには、次のものがあります。  
   - スキーママスタ
   - ドメイン名前付けマスタ
   - 相対 ID (RID) マスター
   - プライマリドメインコントローラー (PDC) エミュレーターマスター
   - インフラストラクチャマスター

さらに、ラボ環境で AD DS と SYSVOL を定期的にバックアップして復元する必要があります。 詳細については、「[システム状態データをバックアップ](AD-Forest-Recovery-Procedures.md)し、 [Active Directory Domain Services の権限のない復元を実行する](AD-Forest-Recovery-Procedures.md)」を参照してください。

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
