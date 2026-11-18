# ScoutPlay — plataforma de futebol (MVP público)

O ScoutPlay é um projeto independente. Ele foi inspirado nas **categorias de recursos** comuns em plataformas de descoberta de talentos (perfil esportivo, vídeos, clubes, oportunidades e evolução de habilidades), mas possui nome, identidade visual, estrutura e telas próprias. Não é afiliado ao Footbao.

## O que esta versão inclui

- Interface responsiva com navegação própria para celular e computador.
- Prévia demonstrativa para explorar as telas antes de conectar um banco de dados.
- Cadastro, login e sessão usando Supabase Auth.
- Perfil esportivo: apelido, posição, categoria, pé dominante e apresentação.
- Feed de vídeos aprovados com curtidas e comentários enviados para revisão.
- Busca de atletas com filtros por posição.
- Diretório de clubes que só exibe clubes verificados e ativos.
- Área de oportunidades de clubes verificados.
- Autoavaliação pessoal de 24 habilidades, sem fingir ser avaliação profissional ou análise por IA.
- Upload de vídeos para bucket privado, com revisão antes de aparecer publicamente.
- Regras RLS e políticas de Storage para restringir o acesso aos dados.

## O que ainda depende de configuração/administração

Este ZIP **não é um site publicado** e não possui usuários reais, clubes reais, seletivas reais, avaliação de analistas nem inteligência artificial. A prévia usa atletas, clubes e oportunidades fictícios, claramente identificados como exemplos. Os recursos de conta, publicação e dados partilhados só funcionam depois de configurar o Supabase e hospedar o projeto.

Clubes e oportunidades precisam ser adicionados manualmente no painel administrativo após verificação. O projeto não permite que qualquer pessoa crie um perfil de clube ou publique uma seletiva em nome de uma equipe. A aprovação de responsável (`guardian_approved`) também é uma etapa administrativa que ainda precisa de um processo de verificação real antes de tornar um perfil visível, liberar publicações ou permitir candidaturas.

## Prévia visual

Abra `preview.html` no navegador para explorar a interface com dados fictícios. Essa prévia não cria contas nem publica dados na internet.

## Como configurar com ajuda de um responsável

1. Crie um projeto no Supabase com a ajuda de um responsável.
2. No SQL Editor, execute `supabase/schema.sql`.
3. Em Storage, crie um bucket chamado `football-videos` e mantenha-o **privado**. As políticas para acesso estão no SQL.
4. Copie a URL do projeto e a chave pública `anon` para um arquivo `.env` baseado em `.env.example`.
5. Instale dependências com `npm install` e inicie o projeto com `npm run dev`.
6. Para publicar, conecte o repositório ao Vercel e adicione as mesmas variáveis de ambiente nas configurações do projeto.

Nunca coloque a chave `service_role` no código do navegador, no GitHub ou em mensagens. A chave `anon` só deve ser usada com as políticas RLS corretamente configuradas.

## Segurança de adolescentes

- Não exiba nome completo, data de nascimento, escola, endereço, telefone, rotina ou localização em tempo real.
- Antes de permitir upload, comentários ou candidaturas, implemente verificação válida de responsável e um processo documentado de consentimento.
- Deixe perfis visíveis publicamente somente depois da verificação e aprovação válida do responsável.
- Mantenha vídeos e comentários em revisão antes da publicação.
- Não ofereça mensagens privadas abertas entre adultos desconhecidos e menores.
- Crie política de privacidade, termos, canal de denúncia, regras de moderação e processo de remoção antes de lançar ao público.
- Nunca prometa testes, bolsas, contratos ou oportunidades que não tenham sido confirmados diretamente pelos clubes.

## Estrutura

- `src/main.js` — interface, navegação e integração Supabase.
- `src/style.css` — identidade visual responsiva.
- `preview.html` — prévia local demonstrativa sem conexão com banco.
- `supabase/schema.sql` — tabelas, RLS, funções e políticas de armazenamento.
- `.env.example` — modelo de configuração.
- `vercel.json` — regra de fallback para a aplicação.
