---
title: ダンプの暗号化について
description: ダンプファイルを暗号化し、暗号化をトラブルシューティングする方法について説明します。
ms.prod: windows-server
manager: dongill
ms.topic: article
author: larsiwer
ms.asset: b78ab493-e7c3-41f5-ab36-29397f086f32
ms.author: kathydav
ms.date: 11/03/2016
ms.openlocfilehash: a7df8de5a828b68a341191eaa1a400f80dd9127b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852905"
---
# <a name="about-dump-encryption"></a>ダンプの暗号化について
ダンプ暗号化を使用して、システムに対して生成されたクラッシュダンプとライブダンプを暗号化できます。 ダンプは、ダンプごとに生成される対称暗号化キーを使用して暗号化されます。 このキー自体は、ホストの信頼された管理者 (クラッシュダンプ暗号化キープロテクター) によって指定された公開キーを使用して暗号化されます。 これにより、一致する秘密キーを持つユーザーだけが暗号化を解除して、ダンプの内容にアクセスできるようになります。 この機能は、保護されたファブリックで利用されています。
注: ダンプの暗号化を構成する場合は、Windows エラー報告も無効にします。 WER は、暗号化されたクラッシュダンプを読み取ることができません。

## <a name="configuring-dump-encryption"></a>ダンプ暗号化の構成
### <a name="manual-configuration"></a>手動構成
レジストリを使用してダンプ暗号化を有効にするには、次のレジストリ値を構成し `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl`

| ［値の名前］ | 種類 | 値 |
| ---------- | ---- | ----- |
| DumpEncryptionEnabled | DWORD | ダンプの暗号化を有効にする場合は1、ダンプの暗号化を無効にする場合は0。 |
| Encryptionublickey::P | Binary | ダンプの暗号化に使用する公開キー (RSA、2048ビット)。 これは[BCRYPT_RSAKEY_BLOB](https://msdn.microsoft.com/library/windows/desktop/aa375531(v=vs.85).aspx)として書式設定する必要があります。 |
| Encryption-1:: Thumbprint | String | クラッシュダンプの暗号化を解除するときに、ローカルの証明書ストアで秘密キーを自動的に検索できるようにする証明書の拇印。 |


### <a name="configuration-using-script"></a>スクリプトを使用した構成
構成を簡単にするために、[サンプルスクリプト](https://github.com/Microsoft/Virtualization-Documentation/tree/live/hyperv-tools/DumpEncryption)を使用して、証明書の公開キーに基づくダンプ暗号化を有効にすることができます。

1. 信頼された環境では、2048ビット RSA キーを使用して証明書を作成し、公開証明書をエクスポートします。
2. ターゲットホスト: ローカル証明書ストアにパブリック証明書をインポートします。
3. サンプル構成スクリプトを実行する 
    ```
    .\Set-DumpEncryptionConfiguration.ps1 -Certificate (Cert:\CurrentUser\My\093568AB328DF385544FAFD57EE53D73EFAAF519) -Force
    ```

## <a name="decrypting-encrypted-dumps"></a>暗号化されたダンプの復号化
既存の暗号化されたダンプファイルの暗号化を解除するには、Windows 用デバッグツールをダウンロードしてインストールする必要があります。 このツールセットには、暗号化されたダンプファイルの暗号化を解除するために使用できる KernelDumpDecrypt が含まれています。
秘密キーを含む証明書が現在のユーザーの証明書ストアに存在する場合は、を呼び出すことによってダンプファイルの暗号化を解除できます。

```
    KernelDumpDecrypt.exe memory.dmp memory_decr.dmp
```
暗号化を解除すると、WinDbg などのツールが、復号化されたダンプファイルを開くことができます。

## <a name="troubleshooting-dump-encryption"></a>ダンプの暗号化のトラブルシューティング
システムでダンプ暗号化が有効になっていても、ダンプが生成されていない場合は、システムの `System` イベントログで `Kernel-IO` イベント1207を確認してください。 ダンプ暗号化を初期化できない場合、このイベントが作成され、ダンプは無効になります。

| 詳細なエラーメッセージ | 軽減の手順 |
| ---------------------- | ----------------- |
| 公開キーまたは拇印レジストリが見つかりません | 両方のレジストリ値が想定される場所に存在するかどうかを確認します。 |
| 無効な公開キー | PublicKey レジストリ値に格納されている公開キーが[BCRYPT_RSAKEY_BLOB](https://msdn.microsoft.com/library/windows/desktop/aa375531(v=vs.85).aspx)として格納されていることを確認します。 |
| サポートされていない公開キーのサイズ | 現時点では、2048ビットの RSA キーのみがサポートされています。 この要件に一致するキーを構成する |

また、`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled` の `GuardedHost` 値が0以外の値に設定されているかどうかも確認します。 これにより、クラッシュダンプが完全に無効になります。 この場合は、0に設定します。
