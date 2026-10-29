# APK Android – Controle Equipamentos

Ao abrir o app pela primeira vez, ele mostra uma tela para você digitar **IP (ou domínio) e porta** do servidor
(padrão 8765). Pode ser IP interno, IP externo ou domínio. O endereço fica salvo e nas próximas aberturas o app
conecta sozinho.

- **Servidor bloqueado após o primeiro cadastro:** o aplicativo não oferece opção de editar ou trocar o endereço salvo, mesmo sem conexão. A tela de erro orienta verificar a conexão e reiniciar o celular, com opção apenas para tentar novamente.
- **Cadastrar outro servidor:** é necessário limpar os dados/armazenamento do aplicativo Android nas configurações do aparelho. Isso apaga a configuração local e permite cadastrar um servidor novamente. Limpar somente o cache temporário pode não apagar o armazenamento local em todos os aparelhos.
- **Câmera:** o app pede a permissão do Android na primeira conexão (ou no botão "Permitir câmera").
  O usuário libera sozinho; se negar, pode liberar depois em Configurações > Apps > Controle Equipamentos > Permissões.
- **HTTP liberado:** o app aceita `http://IP:8765` (sem HTTPS). Marque "Usar HTTPS" só se o servidor tiver certificado válido.

## Gerar e instalar o APK atualizado pelo GitHub (sem Android Studio)
1. Crie um repositório e envie **o conteúdo desta pasta `apk-android`** na raiz do repositório
   (`package.json`, `capacitor.config.json`, `www/`, `scripts/`, `.github/`).
2. No GitHub: aba **Actions** > **Gerar APK** > **Run workflow**.
3. Quando terminar (alguns minutos), abra a execução e baixe **controle-equipamentos-apk** em *Artifacts*.
   Dentro está o `app-debug.apk`; instale no celular (permita "instalar apps desconhecidos").

O workflow roda `npx cap add android`, aplica as permissões de câmera/internet/HTTP com `scripts/patch-android.js`
e compila com `./gradlew assembleDebug`.

## Ícone (opcional)
Depois de gerar o projeto Android (local ou no workflow), troque os arquivos em `android/app/src/main/res/mipmap-*`.

## Observações
- Pelo IP externo em HTTP, a senha de administrador trafega sem criptografia. Para uso pela internet, prefira HTTPS
  (Caddy + domínio, ver LEIA-ME do servidor).
- O servidor precisa estar liberado no firewall e redirecionado no roteador (TCP 8765).
\n\n**Correção da tela offline:** a nova tela de erro exibe somente “Tentar novamente”; não possui botão “Alterar servidor”. O workflow incrementa o versionCode para 2 para facilitar a atualização do APK instalado.\n
## Identidade visual Newline
- A pasta `assets/` contém a marca Newline, o ícone do aplicativo e a arte da tela de abertura.
- O workflow gera automaticamente os ícones Android e os recursos de splash antes da compilação.
- O nome exibido no launcher Android passa a ser `Newline Controle`.

### Correção do ícone Android
O workflow copia `assets/icon.png` diretamente para os recursos `mipmap-*` e aponta o AndroidManifest para esses recursos, removendo os XMLs adaptativos padrão que poderiam continuar exibindo o ícone Android genérico. O nome exibido é `Newline Controle`.
