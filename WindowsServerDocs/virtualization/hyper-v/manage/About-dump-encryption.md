---
title: ダンプ暗号化の詳細について
description: ダンプ ファイルを暗号化および暗号化をトラブルシューティングする方法について説明します。
ms.prod: windows-server-threshold
manager: dongill
ms.topic: article
author: larsiwer
ms.asset: b78ab493-e7c3-41f5-ab36-29397f086f32
ms.author: kathydav
ms.date: 11/03/2016
ms.openlocfilehash: e0ca8829aa8f93e7543b4183539beade3b4aeb47
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812393"
---
# <a name="about-dump-encryption"></a>ダンプ暗号化の詳細について
クラッシュ ダンプおよびライブのダンプがシステム生成の暗号化には、ダンプ暗号化を使用できます。 ダンプは、各ダンプの生成される対称暗号化キーを使用して暗号化されます。 このキー自体は、ホスト (クラッシュ ダンプ暗号化キーの保護機能) の信頼された管理者が指定した公開キーを使用して暗号化されます。 これにより、対応する秘密キーを持つユーザーだけを復号化され、そのため、ダンプの内容にアクセスします。 保護されたファブリックでは、この機能を利用します。
注:ダンプ暗号化を構成する場合も Windows エラー報告無効にします。 WER は、暗号化されたクラッシュ ダンプを読み取ることができません。

# <a name="configuring-dump-encryption"></a>ダンプ暗号化を構成します。
## <a name="manual-configuration"></a>手動構成
レジストリを使用して、ダンプ暗号化を有効にするには、次のレジストリ値を構成します。 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl`

| ［値の名前］ | 種類 | Value |
| ---------- | ---- | ----- |
| DumpEncryptionEnabled | DWORD | ダンプ暗号化を無効にするには 0、ダンプ暗号化を有効にする 1 |
| EncryptionCertificates\Certificate.1::PublicKey | バイナリ | 公開キー (RSA、2048 ビット) のダンプを暗号化するために使用する必要があります。 として書式設定がこの[先頭に BCRYPT_RSAKEY_BLOB](https://msdn.microsoft.com/library/windows/desktop/aa375531(v=vs.85).aspx)します。 |
| EncryptionCertificates\Certificate.1::Thumbprint | String | クラッシュ ダンプの解読中に、ローカルの証明書ストアに秘密キーの自動検索を許可する証明書の拇印。 |


## <a name="configuration-using-script"></a>スクリプトを使用して構成
構成を簡略化する、[サンプル スクリプト](https://github.com/Microsoft/Virtualization-Documentation/tree/live/hyperv-tools/DumpEncryption)証明書の公開キーに基づくダンプ暗号化を有効にします。

1. 信頼できる環境。2048 ビット RSA キーで証明書の作成し、公開証明書のエクスポート
2. ターゲット ホスト。ローカルの証明書ストアにパブリック証明書のインポート
3. サンプルの構成スクリプトを実行します。 
    ```
    .\Set-DumpEncryptionConfiguration.ps1 -Certificate (Cert:\CurrentUser\My\093568AB328DF385544FAFD57EE53D73EFAAF519) -Force
    ```

# <a name="decrypting-encrypted-dumps"></a>暗号化されたダンプを復号化
既存の暗号化されたダンプ ファイルの暗号化を解除するにはダウンロードして、デバッグ ツールの Windows をインストールする必要があります。 このツール セットには、暗号化されたダンプ ファイルを復号化するために使用できる KernelDumpDecrypt.exe が含まれています。
呼び出すことによって、ダンプ ファイルの暗号化を解除できます秘密キーを含む証明書が現在のユーザーの証明書ストアに存在する場合

```
    KernelDumpDecrypt.exe memory.dmp memory_decr.dmp
```
復号化、後に、WinDbg などのツールは復号化されたダンプ ファイルを開くことができます。

# <a name="troubleshooting-dump-encryption"></a>ダンプ encryption のトラブルシューティング
システムでダンプ暗号化が有効になっている場合は、ダンプが生成されない場合は、システムを確認してください`System`イベント ログを`Kernel-IO`1207 イベント。 ダンプ暗号化を初期化することはできませんと、は、このイベントが作成され、ダンプが無効になっています。

| 詳細なエラー メッセージ | 軽減するための手順 |
| ---------------------- | ----------------- |
| 公開キーまたは拇印レジストリがありません。 | 両方のレジストリ値が予期された場所に存在するかどうかを確認します。 |
| 無効な公開キー | として、公開キーのレジストリ値に格納されている公開キーが格納されていることを確認[先頭に BCRYPT_RSAKEY_BLOB](https://msdn.microsoft.com/library/windows/desktop/aa375531(v=vs.85).aspx)します。 |
| 公開キー サイズがサポートされていません。 | 現時点では、2048 ビット RSA キーののみがサポートされています。 この要件に一致するキーを構成します。 |

場合にもチェック値`GuardedHost` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled` 0 以外の値に設定されます。 クラッシュ ダンプを完全に無効にこれとします。 大文字と小文字の場合は、0 に設定します。
