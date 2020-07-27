---
title: Windows ボリューム ライセンス認証のトラブルシューティング
description: ボリューム ライセンス認証のベスト プラクティスに関する情報と、ライセンス認証の問題のトラブルシューティングに関する情報を提供するリソースの一覧を示します
ms.topic: troubleshooting
ms.date: 09/24/2019
ms.technology: server-general
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: cdd597e77d35b154385cf9de35f3d51a3d9c4e8b
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961343"
---
# <a name="troubleshooting-windows-volume-activation"></a>Windows ボリューム ライセンス認証のトラブルシューティング

製品のライセンス認証は、ソフトウェアを特定のコンピューターにインストールした後に認証するプロセスです。 ライセンス認証により、製品が (不正コピーではなく) 正規品であることが確認されます。また、プロダクト キーまたはシリアル番号が有効であることと、改ざんされておらず、失効していないことも確認されます。 ライセンス認証では、プロダクト キーとインストールの間のリンクまたは関係も確立されます。

ボリューム ライセンス認証は、ボリュームライセンス製品をライセンス認証するプロセスです。 組織でボリューム ライセンスを使用するには、Microsoft との間でボリューム ライセンス契約を結ぶ必要があります。 Microsoft では、組織の規模および購入方法に対応した、カスタマイズされたボリューム ライセンス プログラムを提供しています。 詳しくは、[Microsoft ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/default.aspx)をご覧ください。

[Windows Server 2016 のライセンス認証ガイド](server-2016-activation.md)では、キー管理サービス (KMS) ライセンス認証テクノロジに焦点が当てられています。 このセクションでは、一般的な問題について説明し、KMS とその他のいくつかのボリューム ライセンス認証テクノロジに関するトラブルシューティングのガイドラインを示します。

## <a name="best-practices-for-volume-activation"></a>ボリューム ライセンス認証のベスト プラクティス

次の記事では、Microsoft のボリューム ライセンス認証テクノロジの技術情報とベスト プラクティスについて説明しています。

### <a name="key-management-service-kms"></a>キー管理サービス (KMS)

- [ボリューム ライセンス認証の計画](/windows/deployment/volume-activation/plan-for-volume-activation-client)
- [KMS について](/previous-versions/tn-archive/ff793434(v=technet.10))
- [KMS ライセンス認証の展開](/previous-versions/tn-archive/ff793409%28v=technet.10%29)
- [KMS ホストの構成](/previous-versions/tn-archive/ff793407%28v%3dtechnet.10%29)
- [DNS の構成](/previous-versions/tn-archive/ff793405%28v%3dtechnet.10%29)
- [キー管理サービスによるライセンス認証](/windows/deployment/volume-activation/activate-using-key-management-service-vamt)

### <a name="active-directory-based-activation-adba"></a>Active Directory によるライセンス認証 (ADBA)

- [Active Directory によるライセンス認証の展開](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn502534%28v%3dws.11%29)
- [Active Directory によるライセンス認証を使用したライセンス認証](/windows/deployment/volume-activation/activate-using-active-directory-based-activation-client)
- [Active Directory ベースのライセンス認証の概要](/windows/deployment/volume-activation/active-directory-based-activation-overview)

### <a name="multiple-activation-key-mak-activation"></a>マルチ ライセンス認証キー (MAK) ライセンス認証

- [MAK ライセンス認証の使用](/previous-versions/tn-archive/ff793438%28v=technet.10%29)
- [MAK ライセンス認証について](/previous-versions/tn-archive/ff793435%28v%3dtechnet.10%29)
- [MAK クライアントのライセンス認証](/previous-versions/tn-archive/ff793398%28v%3dtechnet.10%29)

### <a name="subscription-activation"></a>サブスクリプションのライセンス認証

- [Windows 10 サブスクリプションのライセンス認証](/windows/deployment/windows-10-subscription-activation)
- [Windows 10 Enterprise のライセンスの展開](/windows/deployment/deploy-enterprise-licenses)
- [Windows 10 Enterprise E3 in CSP](/windows/deployment/windows-10-enterprise-e3-overview)

## <a name="resources-for-troubleshooting-activation-issues"></a>ライセンス認証の問題のトラブルシューティングに関するリソース

次の記事では、ボリューム ライセンス認証の問題をトラブルシューティングするためのガイドラインとツールに関する情報を提供しています。

- [キー管理サービス (KMS) のトラブルシューティングのガイドライン](activation-troubleshoot-kms-general.md)
- [ボリューム ライセンス認証情報を取得するための Slmgr.vbs オプション](activation-slmgr-vbs-options.md)
- [例:ライセンス認証が行われない ADBA クライアントのトラブルシューティング](activation-troubleshoot-adba-clients.md)

次の記事では、より具体的なライセンス認証の問題に対処するためのガイダンスを提供します。

- [一般的なライセンス認証のエラー コードの解決](activation-error-codes.md)
- [KMS ライセンス認証: 既知の問題](activation-troubleshoot-KMS-issues.md)
- [MAK ライセンス認証: 既知の問題](activation-troubleshoot-MAK-issues.md)
- [DNS に関連するライセンス認証の問題のトラブルシューティングに関するガイドライン](common-troubleshooting-procedures-kms-dns.md)
- [Tokens.dat ファイルの再構築方法](activation-rebuild-tokens-dat-file.md)
