---
title: Active Directory サーバーのパフォーマンス チューニング
description: Active Directory サーバーのパフォーマンス チューニング
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: TimWi; ChrisRob; HerbertM; KenBrumf;  MLeary; ShawnRab
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 04c9683c3d14291d5dc2682c6836657313865866
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891943"
---
# <a name="performance-tuning-active-directory-servers"></a>Active Directory サーバーのパフォーマンス チューニング

Active Directory のパフォーマンス チューニングでは、次の 2 つの目標に焦点を当てます。
- Active Directory が、可能な限り最も効率的な方法で負荷を処理するように最適に構成されている
- Active Directory に送信されるワークロードをできるだけ効率的にする

そのためには、次の 3 つの独立した領域に適切な注意を払う必要があります。
- 適切なキャパシティ プランニング - 既存の負荷をサポートするために十分なハードウェアが配置されていることの確認
- サーバー側チューニング - 負荷をできるだけ効率よく処理するためのドメイン コントローラーの構成
- Active Directory クライアント/アプリケーション チューニング - クライアントとアプリケーションによって Active Directory が最適な方法で使用されていることの確認

## <a name="start-with-capacity-planning"></a>キャパシティ プランニングから開始する
十分な数のドメイン コントローラーを適切なロケールの適切なドメインに適切に展開し、冗長性に対処することは、適切なタイミングでクライアント要求を処理するために重要です。 これは詳細なトピックであり、このガイドのスコープ外となります。 読者には、「[Capacity Planning for Active Directory Domain Services (Active Directory Domain Services のキャパシティ プランニング](https://go.microsoft.com/fwlink/?LinkId=324566)」に記載されている推奨事項とガイダンスを読んで理解することにより、Active Directory のパフォーマンス チューニングを開始することをお勧めします。

>[!Important]
> Active Directory の適切な構成とサイズ設定は、全体的なシステムとワークロードのパフォーマンスに大きく影響する可能性があります。 読者には、最初に「[Capacity Planning for Active Directory Domain Services (Active Directory Domain Services のキャパシティ プランニング)](https://go.microsoft.com/fwlink/?LinkId=324566)」を読むことを強くお勧めします。

## <a name="updates-and-evolving-recommendations"></a>更新と進化する推奨事項

過去数世代のオペレーティング システムでは Active Directory とクライアントの両方のパフォーマンス最適化に大規模な改善が行われ、こうした努力が続いています。 以下のようなメリットを得るために、最新バージョンのプラットフォームを展開することをお勧めします。

- 信頼性の向上
- パフォーマンスの向上
- ログ記録とトラブルシューティングを行うツールの向上

ただし、これには時間がかかり、最新のプラットフォームを 100% 採用することはできないシナリオで実行されている環境が多いことを私たちは認識しています。 以前のバージョンのプラットフォームにはいくつかの改善が追加されており、さらに追加を続けていく予定です。

「[Ask the Directory Services Team (ディレクトリ サービス チームに質問)](https://blogs.technet.microsoft.com/askds)」のチーム ブログに従って、ADDS の管理に関する最新ニュース、ガイダンスおよびベスト プラクティスの最新情報を常に把握しておくことをお勧めします。

## <a name="see-also"></a>関連項目
- [ハードウェアに関する考慮事項](hardware-considerations.md)
- [LDAP に関する考慮事項](ldap-considerations.md)
- [ドメイン コントローラーとサイトの適切な配置に関する考慮事項](site-definition-considerations.md)
- [ADDS パフォーマンスのトラブルシューティング](troubleshoot.md) 
- [Active Directory Domain Services のキャパシティ プランニング](https://go.microsoft.com/fwlink/?LinkId=324566)
