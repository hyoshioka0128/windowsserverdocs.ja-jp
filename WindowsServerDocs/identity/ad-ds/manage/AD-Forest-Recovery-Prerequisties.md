---
title: "Active Directory フォレストの回復を計画するための前提条件"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adfs
ms.openlocfilehash: 672e1f4d0de9bfb2cbe291c5ed715814c8acacd0
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2017
---
#<a name="active-directory-forest-recovery-prerequisites"></a>Active Directory フォレストの回復の前提条件

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

次のドキュメントでは、フォレストの回復計画を立てるまたは回復を試みる前に慣れておく必要のある前提条件について説明します。

## <a name="assumptions-for-using-this-guide"></a>このガイドを使用するための前提条件 

1.  マイクロソフトのサポート担当者に協力して。

    - フォレスト全体の障害の原因を特定します。 このガイドでは失敗の原因を提案しないや障害を防止するための手順をお勧めしません。  
    - 任意の考えられる救済策を評価します。  
    - 確認したうえで、Microsoft のサポートと相談、その状態に復元するフォレスト全体の障害発生前に、障害から回復する最適な方法です。 多くの場合、フォレストの回復は最後のオプションをする必要があります。  </br></br>

2. Active Directory 統合ドメイン ネーム システム (DNS) を使用するため、Microsoft のベスト プラクティス推奨事項を後があること。 具体的には、Active Directory ドメインごとに、Active Directory 統合 DNS ゾーンが必要があります。 サポートしていない場合は場合、でも、フォレストの回復を実行するこのガイドの基本原則を使用することができます。 ただし、ご使用の環境に基づく DNS 回復のための特定の対策を講じる必要があります。 詳細については、Active Directory 統合 DNS を使用して、次を参照してください。[DNS インフラストラクチャの設計を作成する](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)します。
3. このガイドは、フォレストの回復のための汎用的なガイドとして対象としていますが、すべての可能なシナリオがについて説明します。 たとえば、Windows Server 2008 以降では、バージョンがある Server Core、完全な GUI ことがなく Windows Server の完全なバージョンであります。 確実に Server Core を実行している Dc だけで成るフォレストを回復することはできますが、このガイドの詳細な手順についてはありません。 ただし、ここで説明するガイダンスに基づくことができますを自分で必要なコマンド ライン アクションを設計します。  
 
>![!NOTE]
> このガイドの目的は、フォレストを回復し、保守または DNS の全機能を復元するのには、回復 DNS 構成、障害発生前に、の構成から変更されていることがあります。 フォレストを修復した後は、元の DNS 構成に戻すことができます。 このガイドの推奨事項はの他の部分は、企業の名前空間の名前解決を実行する DNS サーバーを構成する方法を説明しませんが、AD DS に保存されていない DNS ゾーンが存在します。  

## <a name="concepts-for-using-this-guide"></a>このガイドを使用するための概念
 Active Directory フォレストの回復の計画を開始する前に、次を理解しておく必要があります。  
  
-   Active Directory の基本的な概念  
  
-   操作マスターの役割 (フレキシブル シングル マスター操作または FSMO とも呼ばれます) の重要性 これらの役割は、次のとおりです。  
  
    -   スキーマ マスタ  
  
    -   ドメイン名前付けマスタ  
  
    -   相対 ID (RID) マスタ  
  
    -   プライマリ ドメイン コントローラー (PDC) エミュレータ マスタ  
  
    -   インフラストラクチャ マスタ  
  
 さらに、バックアップがある必要があり、定期的に、ラボ環境で AD DS と SYSVOL を復元します。 詳細については、次を参照してください。[システム状態データをバックアップする](AD-Forest-Recovery-Procedures.md)と[権限のない Active Directory ドメイン サービスの復元を実行する](AD-Forest-Recovery-Procedures.md)します。

## <a name="next-steps"></a>次の手順
-   [AD フォレストの回復の前提条件](AD-Forest-Recovery-Prerequisties.md)  
-   [AD フォレストの回復 - カスタム フォレスト回復計画を立てる](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD フォレストの回復 - 問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
-   [AD フォレストの回復 - を回復する方法を決定します。](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [AD フォレストの回復 - 最初の回復を実行](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
-   [AD フォレストの回復のよく寄せられる質問](AD-Forest-Recovery-FAQ.md)  
-   [AD フォレストの回復であれば、マルチ ドメイン フォレスト内で 1 つのドメインの回復](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [AD フォレストの回復 - Windows Server 2003 ドメイン コントローラーとフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md)  
