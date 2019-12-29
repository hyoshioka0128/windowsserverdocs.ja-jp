> [!Note] 
> 保護されたファブリックの診断ツール (Get-HgsTrace -RunDiagnostics) を実行しているときに、HTTPS 構成が損傷しているという、正しくないステータスが返されることがあります。この場合、実際には HTTPS 構成は損傷していないか、使用されていないことがあります。 このエラーは、HGS の構成証明モードに関係なく返される場合があります。 考えられる原因は次のとおりです。
>
> - HTTPS が実際に正しく構成されていないか、損傷している<br>
> - 管理者によって信頼された構成証明を使用していて、信頼関係が壊れている<br>
> &nbsp;&nbsp;&nbsp;&nbsp;-これは、HTTPS が適切に構成されているか、正しくないか、またはまったく使用されていないかに関係ありません。<br>
>
> 診断ツールは、Hyper-V ホストをターゲットとしている場合のみ、この正しくないステータスを返すことに注意してください。 診断ツールがホスト ガーディアン サービスをターゲットとしている場合には、ステータスは正しい結果を返します。

<!-- Appears in guarded-fabric-setting-up-the-host-guardian-service-hgs.md and guarded-fabric-troubleshoot-diagnostics.md
-->
