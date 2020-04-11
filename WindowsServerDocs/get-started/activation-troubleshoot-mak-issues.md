---
title: MAK ライセンス認証の既知の問題
description: MAK ライセンス認証プロセス中に発生する可能性のある一般的な問題について説明し、解決策とガイダンスを示します。
ms.topic: article
ms.date: 10/3/2019
ms.technology: server-general
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: 0f4153387d740379e66eca9e8069b7a446a1ec71
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80826235"
---
# <a name="mak-activation-known-issues"></a>MAK ライセンス認証: 既知の問題

この記事では、マルチ ライセンス認証キー (MAK) のライセンス認証中に発生する可能性のある一般的な問題について説明し、それらの問題に対処するためのガイダンスを示します。

## <a name="how-can-i-tell-whether-my-computer-is-activated"></a>コンピューターがライセンス認証済みかどうかを確認する方法はありますか?

コンピューターで、 **[システム]** コントロール パネルを開き、"**Windows はライセンス認証されています**" を探します。 または、Slmgr.vbs を実行し、 **/dli** コマンド ライン オプションを使用します。

## <a name="the-computer-does-not-activate-over-the-internet"></a>コンピューターがインターネット経由でライセンス認証されない

必要なポートがファイアウォールで開かれていることを確認します。 ポートの一覧については、「[ボリューム ライセンス認証の展開ガイド](https://go.microsoft.com/fwlink/?linkid=150083)」を参照してください。

## <a name="internet-and-telephone-activation-fail"></a>インターネットと電話によるライセンス認証が失敗する

最寄りのマイクロソフト ライセンス認証専用窓口にお問い合わせください。 世界中のマイクロソフト ライセンス認証専用窓口の電話番号については、「[マイクロソフト ライセンス認証専用窓口の電話番号](https://www.microsoft.com/Licensing/existing-customer/activation-centers)」を参照してください。 お電話いただくときは、ボリューム ライセンス契約の情報と購入の証明をお知らせください。

## <a name="slmgrvbs-ato-returns-an-error-code"></a>Slmgr.vbs /ato でエラー コードが返される

Slmgr.vbs から 16 進数のエラー コードが返された場合は、次のスクリプトを実行して対応するエラー メッセージを確認します。

```cmd
slui.exe 0x2a 0x <ErrorCode>
```

具体的なエラー コードとその対処方法の詳細については、[一般的なライセンス認証エラー コードの解決](activation-error-codes.md)に関するページを参照してください。
