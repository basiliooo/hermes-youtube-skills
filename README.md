# Hermes YouTube Skills 🎥🚀

Este repositório contém uma coleção de **Skills para o Hermes Agent** voltados para a criação, edição, análise e automação de conteúdo para o YouTube e formatos curtos.

## 📦 O que são Skills no Hermes?
Skills são "memórias procedurais" e fluxos de trabalho que ensinam o Hermes Agent (ou bots de perfis específicos) a executar tarefas complexas de maneira previsível. Elas garantem que a IA siga o seu padrão de qualidade, estilo, tom de voz e as restrições que você configurou, sem precisar repetir o prompt inteiro a cada nova conversa.

## 🛠 Skills Inclusas

- **`yt-script`**: Escreve roteiros de vídeos para o YouTube a partir de uma ideia crua, estruturando opções de gancho (Hook), introdução, corpo e CTA.
- **`yt-edit`**: Transforma a transcrição de uma gravação bruta em uma lista de decisões de edição (onde cortar, onde focar), acelerando o trabalho no Premiere/DaVinci.
- **`yt-package`**: Escreve e revisa títulos e fornece ideias de thumbnails voltadas para maximizar a taxa de clique (CTR).
- **`yt-retention`**: Analisa dados exportados de retenção de público do YouTube Studio para encontrar padrões do que segura a audiência e do que causa abandonos.
- **`yt-shorts`**: Identifica e minera os trechos com maior potencial de "Shorts" escondidos dentro de vídeos longos, e escreve as instruções de edição para eles.
- **`yt-viral`**: Analisa o que realmente está funcionando no seu nicho, dissecando padrões de vídeos de alta performance.
- **`youtube-content`**: Reproveita transcrições de vídeos do YouTube para criar resumos, threads e artigos completos.
- **`youtube-knowledge-clipping`**: Captura a "sabedoria" e o conhecimento contido nos vídeos e estrutura de forma indexada para anotações (ex: para o Obsidian).
- **`youtube-thumbnail-design`**: Direcionamento de design visual de thumbnails (foco em composições Tech/IA).
- **`higgsfield-youtube-thumbnail`**: Geração de thumbnails e imagens de alto CTR e banners verticais utilizando integração com IA de imagem da Higgsfield.
- **`edicao-video-viral`**: Guia de diretrizes para edição de vídeos curtos (Reels/Shorts) focados em máxima retenção visual (regra dos 5 segundos de gancho, Efeito Gabriel Saab/Arthur Miller, etc).
- **`youtube-batch-processing`**: Processamento em lote de transcrições do YouTube de forma segura, contornando proteções.
- **`web-extract-youtube-fallback`**: Utilitário de contingência para extração de dados quando as APIs do YouTube ou ferramentas como o `yt-dlp` falham por limite de taxa (erro 429).

## 🚀 Como Instalar e Usar

1. **Clone o repositório**:
   ```bash
   git clone https://github.com/basiliooo/hermes-youtube-skills.git
   ```

2. **Mova para o Hermes**:
   Mova as pastas das skills que deseja utilizar para o diretório global de skills do Hermes, ou para o seu perfil específico:
   ```bash
   cp -r hermes-youtube-skills/* ~/.hermes/skills/
   ```
   *(Se você usa os perfis na barra lateral: `~/.hermes/profiles/NOME_DO_PERFIL/skills/`)*

3. **Invoque no Chat**:
   Sempre que precisar executar um desses fluxos, diga ao Hermes para ativar a skill. Exemplo:
   > *"Vamos começar a usar a skill `yt-script` para escrever um roteiro sobre Inteligência Artificial."*

## 💡 Modificando
Sinta-se livre para entrar no `SKILL.md` de qualquer uma das pastas e alterar o contexto para o seu próprio tom de voz ou regras de edição!

---
*Criado com 🧠 por Nicolas Basílio*