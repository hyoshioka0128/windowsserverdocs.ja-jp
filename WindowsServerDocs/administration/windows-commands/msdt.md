---
title: msdt
description: Msdt コマンドの参照記事。コマンドラインでトラブルシューティングパックを起動するか、自動スクリプトの一部として、ユーザー入力なしで追加のオプションを有効にします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ead1b672-a120-4e16-94aa-a8e13602c1d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b5f00f34da20e9e151f093b919244fe3b49a85d6
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956894"
---
# <a name="msdt"></a>msdt

コマンドラインまたは自動化されたスクリプトの一部としてトラブルシューティングパックを起動し、ユーザー入力なしで追加のオプションを有効にします。

## <a name="syntax"></a>構文

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

### <a name="parameters"></a>パラメーター

| パラメーター | Description |
| --------- | ----------- |
| /id`<packagename>` | 実行する診断パッケージを指定します。 利用可能なパッケージの一覧については、「[使用可能なトラブルシューティングパック](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/ee424379(v=ws.11)#available-troubleshooting-packs)」を参照してください。 |
| /path`<directory|.diagpkg file|.diagcfg file>` | 診断パッケージへの完全パスを指定します。 ディレクトリを指定する場合は、ディレクトリに診断パッケージが含まれている必要があります。 * */Id * *、 **/dci**、/ **cab**の各パラメーターと共に、 **/path**パラメーターを使用することはできません。 |                                                                                   |
| /dci`<passkey>` | パスキーフィールドをプリセットします。 このパラメーターは、サポートプロバイダーがパスキーを指定した場合にのみ使用されます。 |
| /dt`<directory>` | 指定されたディレクトリのトラブルシューティングの履歴を表示します。 診断結果は、ユーザーの **%LOCALAPPDATA%\Diagnostics**または **%LOCALAPPDATA%\ElevatedDiagnostics**ディレクトリに格納されます。 |
| /af`<answerfile>` | 1つ以上の診断対話に対する応答を含む応答ファイルを XML 形式で指定します。 |
| /モーダル`<ownerHWND>` | 親コンソールウィンドウハンドル (HWND) によって指定された、10進数のウィンドウにトラブルシューティングパックをモーダルにします。 このパラメーターは、通常、トラブルシューティングパックを起動するアプリケーションによって使用されます。 コンソールウィンドウハンドルの取得の詳細については、「[コンソールウィンドウハンドルを取得する方法 (HWND)](https://support.microsoft.com/help/124103/how-to-obtain-a-console-window-handle-hwnd)」を参照してください。 |
| その他のオプション`<true|false>` | ユーザーが追加のオプションを調査するかどうかを確認する最後のトラブルシューティング画面を有効 (true) または抑制 (false) します。 通常、このパラメーターは、オペレーティングシステムに含まれていないトラブルシューティングツールによってトラブルシューティングパックが起動されるときに使用されます。 |
| /param returns`<parameters>` | 応答ファイルと同様に、コマンドラインでの相互作用応答のセットを指定します。 通常、このパラメーターは、TSP デザイナーで作成されたトラブルシューティングパックのコンテキスト内では使用されません。 カスタムパラメーターの開発の詳細については、「 [Windows トラブルシューティングプラットフォーム](/previous-versions/windows/desktop/wintt/windows-troubleshooting-toolkit-portal)」を参照してください。 |
| /advanced | トラブルシューティングパックが開始されたときに、既定で [ようこそ] ページの [詳細設定] リンクを展開します。 |
| /カスタム | ユーザーに対して、適用される可能性のある解決策を確認するように求めるメッセージを表示します。 |

### <a name="return-codes"></a>リターン コード

トラブルシューティングパックは、一連の根本原因を構成し、それぞれが特定の技術的な問題について説明します。 トラブルシューティングパックのタスクが完了すると、各根本原因が、fixed、not fixed、検出された (修正されていない) 状態に戻ります。または、見つかりません。 トラブルシューティングツールのユーザーインターフェイスで報告される具体的な結果に加えて、トラブルシューティングエンジンは、トラブルシューティング担当が元の問題を修正したかどうかについて、一般的な用語で説明する結果のコードを返します。 コードは次のとおりです。

| コード | 説明 |
| ---- | ----------- |
| -1 | **中断:** トラブルシューティングタスクが完了する前に、トラブルシューティングツールが閉じられました。 |
| 0 | **修正済み:** このトラブルシューティングツールでは、少なくとも1つの根本原因を特定し、修正しました。根本的な原因はありません。 |
| 1 | **存在しますが、修正されていません。** トラブルシューティングツールによって、固定されていない状態の1つ以上の根本原因が特定されました。 このコードは、別の根本原因が修正された場合でも返されます。 |
| 2 | **見つかりませんでした:** トラブルシューティングツールは、根本的な原因を特定できませんでした。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [利用可能なトラブルシューティングパック](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/ee424379(v=ws.11)#available-troubleshooting-packs)

- [トラブルシューティングパック Powershell リファレンス](/powershell/module/troubleshootingpack/?view=win10-ps)
