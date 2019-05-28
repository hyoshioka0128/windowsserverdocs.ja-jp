---
title: msdt
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ead1b672-a120-4e16-94aa-a8e13602c1d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 09f3f738d5a7ba7f7c40cb4eb2ce043856b378cc
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "63718266"
---
# <a name="msdt"></a>msdt



コマンドラインまたは自動化されたスクリプトの一部として、トラブルシューティング パックを呼び出し、ユーザー入力がないその他のオプションを使用します。

## <a name="syntax"></a>構文

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

## <a name="parameters"></a>パラメーター

次の表には、パラメーターと msdt.exe でサポートされるオプションが含まれています。

|パラメーター|説明|
|---------|-----------|
|/id\<パッケージ名 >|実行すると、診断パッケージを指定します。 利用可能なパッケージの一覧は、"利用可能なトラブルシューティング パックでしょうか。 でのトラブルシューティング パック ID を参照してください。 このトピックで後述する「します。|
|/path\<ディレクトリ | .diagpkg ファイル | .diagcfg ファイル >|診断パッケージへの完全パスを指定します。 ディレクトリを指定する場合、ディレクトリは、診断パッケージを含める必要があります。 組み合わせて/path パラメーターを使用することはできません、 */id*、 */dci*、または*cab/* パラメーター。|
|/dci \<passkey>|Msdt のパスキーのフィールドに設定します。 このパラメーターは、サポート プロバイダーにパスキーが提供されている場合にのみ使用します。|
|/dt \<directory>|指定したディレクトリ内には、トラブルシューティングの履歴を表示します。 ユーザーの診断結果が格納されている **%LOCALAPPDATA%\Diagnostics**または **%LOCALAPPDATA%\ElevatedDiagnostics**ディレクトリ。|
|/af\<応答ファイル >|1 つまたは複数の診断操作に応答が含まれている XML 形式で応答ファイルを指定します。|
