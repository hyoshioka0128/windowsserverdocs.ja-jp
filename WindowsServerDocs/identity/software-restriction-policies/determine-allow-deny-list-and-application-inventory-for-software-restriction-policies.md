---
title: ソフトウェアの制限のポリシーの許可/拒否リストおよびアプリケーション インベントリの決定
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0abb73b6-b5d8-4505-8ab1-2f29e4bf0411
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 60e78912284715649938567d66ffb90b9890b1b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847293"
---
# <a name="determine-allow-deny-list-and-application-inventory-for-software-restriction-policies"></a>ソフトウェアの制限のポリシーの許可/拒否リストおよびアプリケーション インベントリの決定

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

IT プロフェッショナル向けのこのトピックでは、許可を作成し、Windows Server 2008 および Windows Vista 以降のソフトウェア制限ポリシー (SRP) によって管理されるアプリケーションの一覧を拒否する方法にガイダンスを提供します。

## <a name="introduction"></a>概要
ソフトウェアの制限のポリシー (SRP) はグループ ポリシー ベースの機能で、ドメイン内のコンピューターで実行されているソフトウェア プログラムを識別し、これらのプログラムを実行する機能を制御します。 ソフトウェアの制限のポリシーを使えば、コンピューターの構成に厳格な制限を加え、指定したアプリケーションに限って実行を許可することができます。 これらは、Microsoft Active Directory Domain Services とグループ ポリシーに統合されますが、スタンドアロン コンピューター上で構成することもできます。 SRP の開始点は、次を参照してください。、[ソフトウェア制限ポリシー](software-restriction-policies.md)します。

Windows Server 2008 R2 および Windows 7 以降、Windows AppLocker できますの代わりに、または SRP と連携してアプリケーション制御戦略の一部。

SRP を使用して特定のタスクを実行する方法については、次を参照してください。

-   [ソフトウェア制限ポリシー ルールを操作します。](work-with-software-restriction-policies-rules.md)

-   [ソフトウェア制限ポリシーを使用した電子メール ウイルスからコンピューターを保護するには](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

### <a name="what-default-rule-to-choose-allow-or-deny"></a>選択するどのような既定の規則:許可または拒否
ソフトウェア制限ポリシーは、既定のルールの基礎である 2 つのモードのいずれかで展開できます。許可リストまたはリストを拒否します。 環境内で実行が許可されているすべてのアプリケーションを識別するポリシーを作成することができます。ポリシー内で既定の規則が制限され実行を明示的に許可しないすべてのアプリケーションをブロックします。 またはを実行できません。 すべてのアプリケーションを識別するポリシーを作成することができます。既定のルールは [制限しない] が明示的に一覧表示するアプリケーションのみが制限されます。

> [!IMPORTANT]
> 拒否リスト モードには、アプリケーションの制御に関する組織の高メンテナンス戦略可能性があります。 作成して、すべてのマルウェアやその他の問題のあるアプリケーションを禁止する進化のリストを保持するは、時間がかかり、間違いやすいになります。

### <a name="create-an-inventory-of-your-applications-for-the-allow-list"></a>許可一覧については、アプリケーションのインベントリを作成します。
許可する既定のルールを効果的に使用するには、組織でどのアプリケーションが必要な正確に判断する必要があります。 インベントリ コレクターは、Microsoft Application Compatibility Toolkit などのアプリケーション インベントリを生成するためのツールがあります。 SRP が正確に実行されるアプリケーションを環境内の理解に役立つ、詳細ログ機能。

##### <a name="to-discover-which-applications-to-allow"></a>許可するには、どのアプリケーションを検出するには

1.  テスト環境では、ソフトウェア制限ポリシーを制限しない に既定の規則セットをデプロイし、追加の規則を削除します。 すべてのアプリケーションを制限することを強制せず SRP を有効にした場合 SPR は同じアプリケーションされるはどのように実行を監視することができます。

2.  詳細ログ機能を有効にして、ログ ファイルの書き込み先となるパスを設定するには、次のレジストリ値を作成します。

    **"HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Safer\ CodeIdentifiers"**

    文字列値。*NameLogFile NameLogFile パス*

    ログ ファイルにエントリが書き込まれるため、SRP では、実行時に、すべてのアプリケーションを評価するが、 *NameLogFile*アプリケーションを実行するたびにします。

3.  ログ ファイルを評価します。

    各ログ エントリを状態します。

    -   ソフトウェア制限ポリシーとプロセス ID (PID) 呼び出し元のプロセスの呼び出し元

    -   評価されているターゲット

    -   そのアプリケーションの実行時に発生した SRP の規則

    -   SRP の規則の識別子です。

    ログ ファイルに書き込まれた出力の例:

**explorer.exe (PID = 4728) identifiedC:\Windows\system32\onenote.exe 無制限 usingpath 規則として、Guid = {320bd852-aa7c-4674-82c5-9a80321670a3}** すべてのアプリケーションと関連付けられているコードを SRP チェックし、ブロックする設定には、ログに記録されますファイルは、し、使用する実行可能ファイルを許可されている一覧考慮すべきかを判断することができます。


