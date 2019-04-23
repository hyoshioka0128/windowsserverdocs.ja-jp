---
title: ソフトウェア制限ポリシー
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c0befad-07c3-4262-b418-372d01850305
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: ab44013b947d33adc12c54b527415bf16c46a4c6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875823"
---
# <a name="software-restriction-policies"></a>ソフトウェア制限ポリシー

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

IT プロフェッショナルは、このトピックでは、Windows Server 2012 および Windows 8 では、ソフトウェア制限ポリシー (SRP) について説明し、と共に Windows Server 2003 以降の SRP に関する技術情報へのリンクを提供します。

手順とトラブルシューティングのヒントについては、次を参照してください。[ソフトウェア制限ポリシーの管理](administer-software-restriction-policies.md)と[ソフトウェア制限ポリシーのトラブルシューティングを行う](troubleshoot-software-restriction-policies.md)します。

## <a name="BKMK_OVER"></a>ソフトウェアの制限のポリシーの説明
ソフトウェアの制限のポリシー (SRP) はグループ ポリシー ベースの機能で、ドメイン内のコンピューターで実行されているソフトウェア プログラムを識別し、これらのプログラムを実行する機能を制御します。 ソフトウェアの制限のポリシーは、マイクロソフトのセキュリティと管理に関する戦略の一環として、企業のコンピューターの信頼性、整合性、および管理容易性の向上に寄与します。

ソフトウェアの制限のポリシーを使えば、コンピューターの構成に厳格な制限を加え、指定したアプリケーションに限って実行を許可することもできます。 ソフトウェアの制限のポリシーは、Microsoft Active Directory とグループ ポリシーに統合されています。 スタンドアロン コンピューター上でソフトウェアの制限のポリシーを作成することも可能です。 ソフトウェアの制限のポリシーは信頼ポリシーであり、スクリプトなどの必ずしも信頼できないコードの実行を制限するために管理者が設定する規則です。

このポリシーを定義するには、Microsoft 管理コンソール (MMC) のローカル グループ ポリシー エディター スナップインまたはローカル セキュリティ ポリシー スナップインの "ソフトウェアの制限のポリシー" 拡張機能を使います。

SRP の詳細については、「 [Software Restriction Policies Technical Overview](software-restriction-policies-technical-overview.md)」を参照してください。

## <a name="BKMK_APP"></a>実際の適用
管理者は次のタスクにソフトウェアの制限のポリシーを使用できます。

-   信頼できるコードの定義

-   スクリプト、実行可能ファイル、および ActiveX コントロールの制御用の柔軟なグループ ポリシーの設計

ソフトウェアの制限のポリシーは、ソフトウェアの制限のポリシーに準拠しているオペレーティング システムとアプリケーション (スクリプト アプリケーションなど) によって適用されます。

具体的には、管理者は次の用途にソフトウェアの制限のポリシーを使用できます。

-   クライアントで実行できるソフトウェア (実行可能ファイル) を指定する

-   共有のコンピューター上でユーザーによって特定のプログラムが実行されるのを防ぐ

-   信頼できる発行元をクライアントに追加できるユーザーを指定する

-   ソフトウェアの制限のポリシーの範囲を設定する (ポリシーがクライアントの全ユーザーに適用となるのか、一部ユーザーのみに適用となるのかを指定する)

-   実行可能ファイルがローカル コンピューター、組織単位 (OU)、サイト、ドメインで実行されるのを防ぐ。 悪意のあるユーザーによって引き起こされる問題の予防にソフトウェアの制限のポリシーを使っていない場合には、これが適しています。

## <a name="BKMK_NEW"></a>新規または変更された機能
ソフトウェアの制限のポリシーの機能については変更はありません。

## <a name="BKMK_DEP"></a>削除または非推奨の機能
ソフトウェアの制限のポリシーの機能については削除された機能や推奨されなくなった機能はありません。

## <a name="BKMK_SOFT"></a>ソフトウェアの要件
ローカル グループ ポリシー エディターの "ソフトウェアの制限のポリシー" 拡張機能は、MMC からアクセスできます。

ローカル コンピューターでソフトウェアの制限のポリシーを作成して管理するには、次の機能が必要です。

-   ローカル グループ ポリシー エディター

-   Windows インストーラー

-   Authenticode および WinVerifyTrust

このポリシーをドメインに展開する必要がある場合には、上に挙げた機能のほか、次の機能が必要です。

-   Active Directory Domain Services

-   グループ ポリシー

## <a name="BKMK_INSTALL"></a>サーバー マネージャーの情報
ソフトウェアの制限のポリシーは、ローカル グループ ポリシー エディターの拡張機能の 1 つであり、サーバー マネージャーや [役割と機能の追加] からインストールするものではありません。

## <a name="BKMK_LINKS"></a>参照してください。
SRP に関する情報と使用方法についてのリソースへのリンクを次の表に示します。

|コンテンツの種類|参考資料|
|--------|-------|
|**製品評価**|[ソフトウェア制限ポリシーによるアプリケーションのロックダウン](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|
|**計画**|[ソフトウェア制限ポリシーの技術概要](software-restriction-policies-technical-overview.md)(Windows Server 2012)<br /><br />[ソフトウェアの制限のポリシーのテクニカル リファレンス](https://technet.microsoft.com/library/cc728085(v=WS.10).aspx) (Windows Server 2003)|
|**展開**|リソースはありません。|
|**運用**|[ソフトウェア制限ポリシーの管理](administer-software-restriction-policies.md)(Windows Server 2012)<br /><br />[ソフトウェアの制限のポリシーの製品ヘルプ](https://technet.microsoft.com/library/cc779607(v=WS.10).aspx) (Windows Server 2003)|
|**トラブルシューティング**|[ソフトウェア制限ポリシーのトラブルシューティングを行う](troubleshoot-software-restriction-policies.md)(Windows Server 2012)<br /><br />[ソフトウェアの制限のポリシーのトラブルシューティング](https://technet.microsoft.com/library/cc737011(v=WS.10).aspx) (Windows Server 2003)|
|**セキュリティ**|[ソフトウェアの制限のポリシーに関する脅威と対策](https://technet.microsoft.com/library/dd349795(v=WS.10).aspx) (Windows Server 2008)<br /><br />[ソフトウェアの制限のポリシーに関する脅威と対策](https://technet.microsoft.com/library/hh125926(v=WS.10).aspx) (Windows Server 2008 R2)|
|**ツールと設定**|[ソフトウェアの制限ポリシーのツールおよび設定](https://technet.microsoft.com/library/cc782454(v=WS.10).aspx) (Windows Server 2003)|
|**コミュニティ リソース**|[ソフトウェア制限ポリシーによるアプリケーションのロックダウン](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|



