---
title: ソフトウェアの制限のポリシーを使用した電子メール ウイルスからのコンピューターの保護
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02f23979-f832-4e46-bdea-21fd77db35b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 41b4c2399a86ef96d34b62295eda4a1ce9300609
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850673"
---
# <a name="use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus"></a>ソフトウェアの制限のポリシーを使用した電子メール ウイルスからのコンピューターの保護

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、アプリケーション制御を設定する方法のポリシーに対しても Windows Server 2008 および Windows Vista 電子メール ウイルスからコンピューターを保護するためにソフトウェア制限ポリシー (SRP) を使用して情報を提供します。

## <a name="introduction"></a>概要
ソフトウェアの制限のポリシー (SRP) はグループ ポリシー ベースの機能で、ドメイン内のコンピューターで実行されているソフトウェア プログラムを識別し、これらのプログラムを実行する機能を制御します。 ソフトウェアの制限のポリシーを使えば、コンピューターの構成に厳格な制限を加え、指定したアプリケーションに限って実行を許可することができます。 これらは、Microsoft Active Directory Domain Services とグループ ポリシーに統合されますが、スタンドアロン コンピューター上で構成することもできます。 SRP の開始点は、次を参照してください。、[ソフトウェア制限ポリシー](software-restriction-policies.md)します。

Windows Server 2008 R2 および Windows 7 以降、Windows AppLocker できますの代わりに、または SRP と連携してアプリケーション制御戦略の一部。 

#### <a name="configure-srp-to-help-protect-against-an-e-mail-virus"></a>電子メールのウイルスから保護するための SRP を構成します。

1.  ソフトウェアの制限のポリシー SRP のしくみを理解するためのベスト プラクティスを確認します。

    -   [ベスト プラクティス](software-restriction-policies-technical-overview.md#BKMK_Best_Practices)

    -   [ソフトウェア制限ポリシーのしくみ](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx)

2.  [ソフトウェアの制限のポリシー] を開きます。

    -   [ローカル コンピューターの](administer-software-restriction-policies.md#BKMK_1)

    -   [ドメインのサイト、または組織単位とする、メンバー サーバーまたはドメインに参加しているワークステーション](administer-software-restriction-policies.md#BKMK_2)

3.  ソフトウェア制限ポリシーをまだ定義していない場合は、新しいソフトウェアの制限のポリシーを作成します。

    -   [新しいソフトウェアの制限のポリシーを作成するには](administer-software-restriction-policies.md#BKMK_Create_SRP)

4.  電子メール プログラムを使用して電子メールの添付ファイルを実行するフォルダーのパスの規則を作成し、セキュリティ設定レベルを**許可しない**します。

    -   [パスの規則の操作](work-with-software-restriction-policies-rules.md#BKMK_Path_Rules)

5.  規則が適用されるファイルの種類を指定します。

    -   [指定されたファイルの種類を追加、削除します。](administer-software-restriction-policies.md#BKMK_Add_Del)

6.  ユーザーとグループに適用されるように、ポリシー設定を変更します。

    -   ユーザーまたはグループをたくないグループ ポリシー オブジェクト (GPO) を指定するポリシー設定を適用します。

    -   ローカルの administrators をグループ ポリシーで特定のポリシー設定のソフトウェア制限ポリシーから除外して、他のグループ ポリシー管理者に適用。

        -   [ソフトウェア制限ポリシーがローカルの管理者に適用するを防ぐために](administer-software-restriction-policies.md#BKMK_Prevent_Admin)

7.  ポリシーをテストします。


