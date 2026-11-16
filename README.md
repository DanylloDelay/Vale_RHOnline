# Amigo Secreto — Firebase Web App (versão simples)

## O que faz
- Cadastro de participantes e geração de códigos individuais.
- Sorteio único, sem autoatribuição e sem repetição (ciclo aleatório).
- Revelação por código e registro de quem revelou.
- Interface responsiva em um arquivo HTML.

## Configuração no Firebase
1. O aplicativo web já está configurado em `index.html` para o projeto `rh-online-vale`.
2. Ative **Authentication > Sign-in method > Anonymous** (o usuário já confirmou essa etapa).
3. No **Realtime Database > Rules**, cole o conteúdo de `database.rules.json` e publique. As regras permitem leitura e escrita apenas no nó `amigoSecretoV1` para usuários autenticados anonimamente; os demais nós continuam bloqueados. **Qualquer visitante consegue obter autenticação anônima, portanto essas regras NÃO tornam os dados privados.**
4. Para publicar: instale Node.js e o Firebase CLI (`npm install -g firebase-tools`), rode `firebase login` e `firebase init hosting`. Selecione o projeto `rh-online-vale`, use `.` como pasta pública (ou copie `index.html` para a pasta pública escolhida), responda `No` para single-page app e `No` para sobrescrever o index.html. Rode `firebase deploy --only hosting`.
5. Alternativa: hospede `index.html` no GitHub Pages; o banco continuará no Firebase. Adicione o domínio em Authentication > Settings > Authorized domains se a autenticação exigir.

## Observações importantes
- **Não é um sistema seguro de amigo secreto:** qualquer pessoa com o link pode abrir a aba Organizar, ver todos os códigos e alterar o sorteio; também pode acessar o nó com o SDK Firebase. Não use com dados corporativos ou sensíveis.
- O administrador vê nomes, códigos e status na interface, mas o banco armazena as atribuições. Não há separação real de privilégios.
- Para evitar custos, confira que seu projeto está no plano Spark. Firebase Hosting tradicional, Realtime Database e Authentication anônima têm limites gratuitos.
- Não abra as regras do banco na raiz (`.read: true`, `.write: true`). O projeto `rh-online-vale` pode conter outros dados.
- Regras não expiram automaticamente, então remova ou restrinja o nó após o evento.
