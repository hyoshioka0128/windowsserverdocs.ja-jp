---
title: tpmtool
description: Tpmtool - の Windows コマンド」のトピックでは、トラステッド プラットフォーム モジュールに関する情報を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: ashleytqy
ms.author: ashleytqy
manager: ronaldai
ms.date: 05/07/2019
ms.openlocfilehash: d2939b693c3f9bd8d0d8c8e1fefdd5d8f892e4c9
ms.sourcegitcommit: 3582c38d87f23cc54467d63bf00c29ef07cdb7c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2019
ms.locfileid: "65517195"
---
>[!IMPORTANT]
>一部の情報はリリース前の製品に関することであり、正式版がリリースされるまでに大幅に変更される可能性があります。 本書に記載された情報について、Microsoft は明示または黙示を問わずいかなる保証をするものでもありません。

# <a name="tpmtool"></a>tpmtool

このユーティリティを使用して、情報を取得すること、[トラステッド プラットフォーム モジュール (TPM)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-overview)します。

このコマンドを使用する方法の例については、[例](#tpmtool_examples)を参照してください。

## <a name="syntax"></a>構文

```
tpmtool /parameter [<arguments>]
```
## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|getdeviceinformation|TPM の基本情報が表示されます。|
|gatherlogs [output directory path]|TPM のログを収集し、指定したディレクトリに配置します。 既定では、現在のディレクトリにそれらに配置されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="tpmtool_examples"></a>例

TPM の基本的な情報を表示するには、次のように入力します。
```
tpmtool getdeviceinformation
```
TPM ログを収集して、現在のディレクトリ タイプに配置。
```
tpmtool gatherlogs
```
TPM のログを収集してに配置`C:\Users\Public`種類。
```
tpmtool gatherlogs C:\Users\Public
```
