---
title: tpmtool
description: Tpmtool の Windows コマンドトピックでは、トラステッドプラットフォームモジュールに関する情報を取得します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: ashleytqy
ms.author: ashleytqy
manager: ronaldai
ms.date: 05/07/2019
ms.openlocfilehash: 3967136bc64d1e06425a019466dea15ddce3a563
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385716"
---
# <a name="tpmtool"></a>tpmtool

このユーティリティは、[トラステッドプラットフォームモジュール (TPM)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-overview)に関する情報を取得するために使用できます。

>[!IMPORTANT]
>一部の情報はリリース前の製品に関することであり、正式版がリリースされるまでに大幅に変更される可能性があります。 本書に記載された情報について、Microsoft は明示または黙示を問わずいかなる保証をするものでもありません。

このコマンドを使用する方法の例については、[例](#tpmtool_examples)を参照してください。

## <a name="syntax"></a>構文

```
tpmtool /parameter [<arguments>]
```
## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|getdeviceinformation|TPM の基本情報が表示されます。 情報フラグの値の意味については、[こちら](https://docs.microsoft.com/windows/desktop/SecProv/win32-tpm-isreadyinformation#parameters)を参照してください。|
|gatherlogs [出力ディレクトリのパス]|TPM ログを収集し、指定したディレクトリに格納します。 このディレクトリが存在しない場合は、作成されます。 既定では、これらは現在のディレクトリに配置されます。 生成される可能性があるファイルは次のとおりです。 </br>-TpmEvents</br>-TpmInformation .txt</br>-SRTMBoot dat</br>-SRTMResume. dat</br>-DRTMBoot dat</br>-DRTMResume dat</br>|
|drivertracing [開始/停止]|TPM ドライバーのトレースの収集を開始または停止します。 トレースログ TPMTRACE が生成され、現在のディレクトリに配置されます。|
|parsetcglogs [-validate (-v)]|解析された TCG ログ (Windows ブート構成ログ (WBCL) とも呼ばれます) を表示します。 最新のイベントの説明については、「**イベントの説明**」の「 [TCG」 web サイト](https://trustedcomputinggroup.org/resource/pc-client-specific-platform-firmware-profile-specification/)を参照してください。 @No__t-0 フラグが設定されている場合、は、TPM のプラットフォーム構成レジスタ (PCR) の値がログ内の値と一致することを検証します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="tpmtool_examples"></a>例

TPM の基本情報を表示するには、次のように入力します。
```
tpmtool getdeviceinformation
```
TPM ログを収集して現在のディレクトリに配置するには、次のように入力します。
```
tpmtool gatherlogs
```
TPM ログを収集して `C:\Users\Public` に配置するには、次のように入力します。
```
tpmtool gatherlogs C:\Users\Public
```
TPM ドライバーのトレースを収集するには、次のように入力します。
```
tpmtool drivertracing start
# Run scenario
tpmtool drivertracing stop
```
TCG ログを解析するには、次のようにします。
```
tpmtool parsetcglogs
```
TCG ログを解析し、Pcr を検証するには、次のようにします。
```
tpmtool parsetcglogs -validate
```

## <a name="decoding-error-codes"></a>エラーコードのデコード

TPM 固有のエラーコードについては、[こちら](https://docs.microsoft.com/windows/desktop/com/com-error-codes-6)を参照してください。
