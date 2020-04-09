---
title: パスワードの概要
description: Windows Server のセキュリティ
ms.prod: windows-server
ms.technology: security-kerberos
ms.topic: article
ms.assetid: f608960e-2039-4c91-9c8c-9b81053c675e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 19003d5dcfdaa0f9d6dafcc31bab31a5cb50efa0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858835"
---
# <a name="passwords-overview"></a>パスワードの概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT 担当者向けのこのトピックでは、Windows オペレーティングシステムで使用されるパスワードについて説明し、資格情報管理戦略でのパスワードの使用に関するドキュメントとディスカッションへのリンクを示します。

## <a name="feature-description"></a><a name="BKMK_OVER"></a>機能の説明
現在、オペレーティングシステムとアプリケーションはパスワードを中心に設計されており、スマートカードや生体認証システムを使用している場合でも、すべてのアカウントにパスワードがあり、状況によっては引き続き使用できます。 一部のアカウント (特にサービスの実行に使用されるアカウント) では、スマートカードと生体認証トークンを使用できないため、認証にパスワードを使用する必要があります。 Windows は、暗号化ハッシュを使用してパスワードを保護します。

Windows パスワードの詳細については、「[パスワードの技術概要](https://technet.microsoft.com/library/hh994558(WS.10).aspx)」を参照してください。

## <a name="practical-applications"></a><a name="BKMK_APP"></a>実用的なアプリケーション
Windows およびその他の多くのオペレーティングシステムでは、ユーザーの id を認証する最も一般的な方法は、シークレットパスフレーズまたはパスワードを使用することです。 ネットワーク環境をセキュリティで保護するには、すべてのユーザーが強力なパスワードを使用する必要があります。 これにより、悪意のあるユーザーが悪意のあるユーザーによる脆弱なパスワードの推測を防ぐことができます。これには、手動の方法を使用するか、ツールを使用して、侵害されたユーザーアカウントの資格情報を取得します。 これは、特に管理者アカウントに当てはまります。 複雑なパスワードを定期的に変更すると、パスワード攻撃によってそのアカウントが侵害される可能性が低くなります。

## <a name="new-and-changed-functionality"></a><a name="BKMK_NEW"></a>新機能と変更された機能
Windows Server 2012 と Windows 8 では、ピクチャパスワードが新しくなっています。 ピクチャパスワードは、ユーザーが選択したイメージと一連のジェスチャを組み合わせたものです。 ドメイン\-参加しているコンピューターでは、ピクチャパスワード機能が無効になっています。 ピクチャパスワードに関する詳細情報へのリンクについては、以下を[参照してください](#BKMK_LINKS)。

Windows Server 2012 および Windows 8 では、パスワード機能が変更されていません。 新しいグループポリシー設定は追加されていません。 ただし、資格情報 \(とパスワード\) の管理 (ピクチャパスワードを使用する場合など)、資格情報の保管、Microsoft アカウントで Windows 8 にサインインする (旧称 Windows Live ID) などの機能強化と機能強化が行われました。

## <a name="deprecated-functionality"></a><a name="BKMK_DEP"></a>非推奨の機能
Windows Server 2012 および Windows 8 では、パスワード機能が非推奨とされます。

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>ソフトウェア要件
エンタープライズ環境では、通常、パスワードは Active Directory Domain Services で管理されます。 ローカルコンピューターで、[ローカルセキュリティ設定]、[アカウントポリシー]、[パスワードポリシー] の設定を使用して、パスワードを管理することもできます。

## <a name="see-also"></a><a name="BKMK_LINKS"></a>関連項目
次の表に、パスワード機能、テクノロジ、および資格情報の管理に関するその他のリソースを示します。

|コンテンツの種類|参照|
|--------|-------|
|**シナリオのドキュメント**|[デジタル id の保護](https://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)|
|**運用**|[Active Directory ユーザーとコンピューター](https://technet.microsoft.com/library/cc754217.aspx)|
|**トラブルシューティング**|[パスワードの有効期限が切れたことを確認する \- Active Directory PowerShell ブログ](https://blogs.msdn.com/b/adpowershell/archive/2010/08/09/9970198.aspx)|
|**セキュリティ**| Windows Server 2008 R2 および Windows 7 の[脅威と対策ガイド: アカウントポリシー](https://technet.microsoft.com/library/hh125920(v=ws.10).aspx)<p>[強力なパスワードを変更および作成](https://www.microsoft.com/security/online-privacy/passwords-create.aspx)するためのガイダンス|
|**ツールと設定**|[Microsoft ダウンロードセンターの「Windows および Windows Server 用のグループポリシー設定のリファレンス」](https://www.microsoft.com/download/en/details.aspx?amp;displaylang=en&displaylang=en&id=25250)|
|**コミュニティ リソース**|[デジタル id の保護](https://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)<p>[Windows Live ID を使用した Windows 8 へのサインイン](https://blogs.msdn.com/b/b8/archive/2011/09/26/signing-in-to-windows-8-with-a-windows-live-id.aspx)<p>[ピクチャパスワードを使用したサインイン](https://blogs.msdn.com/b/b8/archive/2011/12/16/signing-in-with-a-picture-password.aspx)<p>[ピクチャパスワードのセキュリティの最適化](https://blogs.msdn.com/b/b8/archive/2011/12/19/optimizing-picture-password-security.aspx)|


