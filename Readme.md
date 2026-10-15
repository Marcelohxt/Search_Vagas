RH-Search: agente pessoal de busca de vagas
Busca vagas o dia todo, ranqueia pela sua aderência, ajusta currículo e carta por vaga com o Claude e prepara respostas a recrutadores no Gmail. Você aprova antes de qualquer envio.

Arquitetura
fontes (Remotive, Greenhouse, Lever, links do LinkedIn)
        │  buscar
        ▼
SQLite data/vagas.db ── ranker (palavras-chave + Claude, nota 0-100)
        │  preparar
        ▼
output/<vaga>/curriculo.md + carta.md   (Claude, sem inventar experiência)
        │  revisar
        ▼
fila de aprovação no terminal → abre a vaga → você aplica → marca "aplicada"
Gmail (OAuth) ── emails → rascunho de resposta no Gmail (envio automático opcional)
Status de cada vaga: nova → pontuada → preparada → aplicada | descartada.

Por que não faz login/candidatura automática no LinkedIn
Automação de login, scraping e candidatura viola os termos de uso do LinkedIn e costuma levar a bloqueio da conta. Aqui o LinkedIn entra por links que você cola em data/linkedin_links.txt (ex.: dos alertas de vaga por e-mail), e a candidatura é feita por você a partir da fila, com currículo e carta já prontos.

Instalação (no seu computador)
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env             # coloque sua ANTHROPIC_API_KEY
cp profile.example.yaml profile.yaml   # cargos, locais, salário, remoto
# salve seu currículo em data/curriculo_base.md
Gmail (opcional): no Google Cloud Console, ative a Gmail API, crie um OAuth Client do tipo "Desktop app", baixe como credentials.json na raiz. Na primeira vez abre o navegador para autorizar.

Senhas e chaves nunca vão no código nem no chat: ficam só no .env (já no .gitignore).