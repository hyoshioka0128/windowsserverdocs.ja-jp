---
title: ソフトウェアの制限のポリシーを使用した電子メール ウイルスからのコンピューターの保護
description: Windows Server のセキュリティ
ms.prod: windows-server
ms.technology: security-software-restriction-policies
ms.topic: article
ms.assetid: 02f23979-f832-4e46-bdea-21fd77db35b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 680d0435d77164e101f045b439be6ccb6601dfef
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855735"
---
# <a name="use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus"></a>ソフトウェアの制限のポリシーを使用した電子メール ウイルスからのコンピューターの保護

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、ソフトウェアの制限のポリシー (SRP) を使用してアプリケーション制御ポリシーを設定する方法について説明します。これは、Windows Server 2008 および Windows Vista 以降では、電子メールのウイルスからコンピューターを保護するのに役立ちます。

## <a name="introduction"></a>はじめに
ソフトウェアの制限のポリシー (SRP) はグループ ポリシー ベースの機能で、ドメイン内のコンピューターで実行されているソフトウェア プログラムを識別し、これらのプログラムを実行する機能を制御します。 ソフトウェアの制限のポリシーを使えば、コンピューターの構成に厳格な制限を加え、指定したアプリケーションに限って実行を許可することができます。 これらは Microsoft Active Directory Domain Services およびグループポリシーと統合されていますが、スタンドアロンコンピューターで構成することもできます。 SRP の開始点については、「[ソフトウェアの制限のポリシー](software-restriction-policies.md)」を参照してください。

Windows Server 2008 R2 および Windows 7 以降では、アプリケーション制御戦略の一部として、または SRP と連携して Windows AppLocker を使用できます。 

#### <a name="configure-srp-to-help-protect-against-an-e-mail-virus"></a>電子メールのウイルスから保護するために SRP を構成する

1.  「ソフトウェアの制限のポリシーに関するベストプラクティス」を参照して、SRP の動作を理解します。

    -   [ベスト プラクティス](software-restriction-policies-technical-overview.md#BKMK_Best_Practices)

    -   [ソフトウェアの制限のポリシーのしくみ](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx)

2.  [ソフトウェアの制限のポリシー] を開きます。

    -   [ローカルコンピューターの場合](administer-software-restriction-policies.md#BKMK_1)

    -   [ドメイン、サイト、または組織単位の場合、メンバーサーバーまたはドメインに参加しているワークステーション上にある](administer-software-restriction-policies.md#BKMK_2)

3.  以前にソフトウェアの制限のポリシーを定義していない場合は、新しいソフトウェアの制限のポリシーを作成します。

    -   [ソフトウェアの制限のポリシーを新規作成するには](administer-software-restriction-policies.md#BKMK_Create_SRP)

4.  電子メールプログラムが電子メールの添付ファイルを実行するために使用するフォルダーのパスの規則を作成し、セキュリティレベルを [**許可**しない] に設定します。

    -   [パスの規則の操作](work-with-software-restriction-policies-rules.md#BKMK_Path_Rules)

5.  規則を適用するファイルの種類を指定します。

    -   [指定されたファイルの種類を追加または削除するには](administer-software-restriction-policies.md#BKMK_Add_Del)

6.  ポリシー設定を変更して、目的のユーザーとグループに適用されるようにします。

    -   グループポリシーオブジェクトの (GPO) ポリシー設定を適用しないユーザーまたはグループを指定します。

    -   グループポリシーの特定のポリシー設定のソフトウェア制限ポリシーからローカル管理者を除外し、残りのグループポリシーを管理者に適用します。

        -   [ソフトウェアの制限のポリシーがローカルの管理者に適用されないようにするには](administer-software-restriction-policies.md#BKMK_Prevent_Admin)

7.  ポリシーをテストします。


