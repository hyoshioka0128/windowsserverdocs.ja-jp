---
title: パスワードの概要
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f608960e-2039-4c91-9c8c-9b81053c675e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 6c1b8d56b5c0da738e7dae5c0072be81040f90d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869603"
---
# <a name="passwords-overview"></a>パスワードの概要

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

IT プロフェッショナルは、このトピックでは、Windows オペレーティング システム、およびドキュメントおよび資格情報の管理戦略でのパスワードの使用に関するディスカッションへのリンクで使用するためのパスワードについて説明します。

## <a name="BKMK_OVER"></a>機能の説明
オペレーティング システムとアプリケーションの現在のパスワードに関する構成とスマート カードまたは生体認証システムを使用する場合でも、すべてのアカウントにはまだパスワードといくつかの状況で引き続き使用します。 いくつかのアカウントでは、サービスを実行するために使用するアカウント顕著なスマート カードと生体認証トークンを使用することはできませんもと、認証にパスワードを使用する必要がありますので。 Windows では、暗号化ハッシュを使用してパスワードを保護します。

Windows パスワードの詳細については、次を参照してください。[パスワードの技術概要](https://technet.microsoft.com/library/hh994558(WS.10).aspx)します。

## <a name="BKMK_APP"></a>実際の適用
Windows およびその他の多くのオペレーティング システムでは、秘密のパスフレーズやパスワードを使用すること、ユーザーの id を認証するための最も一般的な方法です。 ネットワーク環境を保護するには、すべてのユーザーが強力なパスワードを使用することが必要です。 これは、手動のメソッドを使用するかどうか、または侵害されたユーザー アカウントの資格情報を取得するツールを使用して、脆弱なパスワードを推測する悪意のあるユーザーの脅威を回避できます。 これは、管理者アカウントに特に当てはまります。 複雑なパスワードを定期的に変更すると、そのアカウントを侵害すること、パスワード攻撃の可能性を減らします。

## <a name="BKMK_NEW"></a>新規または変更された機能
Windows Server 2012 および Windows 8 でピクチャ パスワードが初めてです。 ピクチャ パスワードは、一連のジェスチャと組み合わせると、ユーザーの選択したイメージの組み合わせです。 ドメインでピクチャ パスワード機能が無効になっている\-参加しているコンピューター。 ピクチャ パスワードに関する詳細情報へのリンクが記載されて[参照](#BKMK_LINKS)以下。

Windows Server 2012 と Windows 8 でのパスワードの機能への変更はありませんしました。 新しいグループ ポリシー設定が追加されていません。 ただし、機能強化と拡張機能に加えられた資格情報\(とパスワード\)管理、ピクチャ パスワード、資格情報保管ボックスおよび Microsoft アカウントで Windows 8 へのサインインと呼ばれていた Windows Live ID など.

## <a name="BKMK_DEP"></a>非推奨の機能
Windows Server 2012 と Windows 8 でないパスワード機能は廃止されました。

## <a name="BKMK_SOFT"></a>ソフトウェアの要件
エンタープライズ環境でのパスワードは通常、Active Directory Domain Services を管理します。 ローカルのセキュリティの設定]、[アカウント ポリシー、パスワード ポリシーの設定を使用して、ローカル コンピューター上のパスワードを管理することもできます。

## <a name="BKMK_LINKS"></a>参照してください。
この表に、パスワードの機能の他のリソース テクノロジと資格情報の管理。

|コンテンツの種類|参考資料|
|--------|-------|
|**シナリオ ドキュメント**|[デジタル id の保護](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)|
|**運用**|[Active Directory ユーザーとコンピューター](https://technet.microsoft.com/library/cc754217.aspx)|
|**トラブルシューティング**|[パスワードの有効期限が切れる特定\-Active Directory PowerShell ブログ](http://blogs.msdn.com/b/adpowershell/archive/2010/08/09/9970198.aspx)|
|**セキュリティ**| Windows Server 2008 R2 および Windows 7[脅威と対策ガイド。アカウント ポリシー](https://technet.microsoft.com/library/hh125920(v=ws.10).aspx)<br /><br />ガイダンスを[変更し、強力なパスワードの作成](https://www.microsoft.com/security/online-privacy/passwords-create.aspx)|
|**ツールと設定**|[Windows と Windows Server、Microsoft ダウンロード センターでのグループ ポリシー設定リファレンス](https://www.microsoft.com/download/en/details.aspx?amp;displaylang=en&displaylang=en&id=25250)|
|**コミュニティ リソース**|[デジタル id の保護](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)<br /><br />[Windows 8 と Windows Live ID へのをサインイン](http://blogs.msdn.com/b/b8/archive/2011/09/26/signing-in-to-windows-8-with-a-windows-live-id.aspx)<br /><br />[ピクチャ パスワードを使用してサインイン](http://blogs.msdn.com/b/b8/archive/2011/12/16/signing-in-with-a-picture-password.aspx)<br /><br />[ピクチャ パスワードのセキュリティの最適化](http://blogs.msdn.com/b/b8/archive/2011/12/19/optimizing-picture-password-security.aspx)|


