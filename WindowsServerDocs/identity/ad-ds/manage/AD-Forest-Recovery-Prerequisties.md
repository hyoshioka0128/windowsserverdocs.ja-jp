---
title: Active Directory フォレストの回復を計画するための前提条件
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adds
ms.openlocfilehash: c8945dd5ccccb27826dd96413b56a070a7452789
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842173"
---
# <a name="active-directory-forest-recovery-prerequisites"></a>Active Directory フォレスト回復の前提条件

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

次のドキュメントでは、フォレスト回復の計画を立てるまたは復旧を試行する前に理解する必要がある前提条件について説明します。

## <a name="assumptions-for-using-this-guide"></a>このガイドを使用するための前提条件

1. マイクロソフトのサポート担当者で作業したとします。
   - フォレスト全体の障害の原因を特定します。 このガイド、エラーの原因を提案したりしない障害を防止するための手順をお勧めします。
   - 任意の考えられる解決策を評価します。  
   - 終了し、Microsoft のサポートと連絡を取り合って、その状態に復元するフォレスト全体の障害が発生する前に、障害から復旧する最適な方法です。 多くの場合、フォレストの回復は最後のオプションにする必要があります。

2. Active Directory に統合されたドメイン ネーム システム (DNS) の使用に関する Microsoft のベスト プラクティス推奨事項を従っていること。 具体的には、Active Directory ドメインごとに、Active Directory 統合 DNS ゾーンが必要があります。 
   - サポートしていない場合は場合、でも、フォレストの回復を実行するこのガイドの基本原則を使用することができます。 ただし、独自の環境に基づいて DNS 回復用の特定の対策を講じる必要があります。 詳細については、Active Directory 統合 DNS を使用して、次を参照してください。 [DNS インフラストラクチャの設計を作成する](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)します。

3. このガイドは、フォレストの回復のための汎用的なガイドとして対象としていますが、すべての可能なシナリオがについて説明します。 たとえば、完全な GUI ことがなく Windows Server の完全なバージョンである Server Core のバージョンは Windows Server 2008 以降。 確かに Server Core を実行している Dc だけで構成されるフォレストを回復することはできますが、このガイドの詳細な手順がありません。 ただし、ここで説明したガイダンスに基づくができる、必要なコマンドライン操作を自分で設計します。  

> ![!NOTE]
> このガイドの目的は、フォレストを回復し、維持または完全な DNS 機能を復元するが、DNS の構成、障害発生前に、構成から変更された、回復があります。 フォレストを回復すると後、は、元の DNS 構成に戻すことができます。 このガイドの推奨事項は、会社の名前空間の他の部分の名前解決を実行する DNS サーバーを構成する方法を記述しないが AD DS に格納されていない DNS ゾーンがある場合。  

## <a name="concepts-for-using-this-guide"></a>このガイドを使用するための概念

Active Directory フォレストの回復の計画を開始する前に、次のようにについて理解する必要があります。  
  
- Active Directory の基本的な概念  
- 操作マスターの役割 (フレキシブル シングル マスター操作または FSMO とも呼ばれます) の重要度。 これらのロールを以下に示します。  
   - スキーマ マスター
   - ドメイン名前付けマスタ
   - 相対 ID (RID) マスター
   - プライマリ ドメイン コント ローラー (PDC) エミュレータ マスタ
   - インフラストラクチャ マスタ

さらに、バックアップがある必要があり、定期的にラボ環境で AD DS と SYSVOL を復元します。 詳細については、次を参照してください。[システム状態データをバックアップする](AD-Forest-Recovery-Procedures.md)と[Active Directory Domain Services の権限のない状態の復元を実行する](AD-Forest-Recovery-Procedures.md)します。

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
