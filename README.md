# Bot Currículos Local

Busca de vagas e assistência a candidaturas com Python, regras e Playwright. A execução local do bot não chama modelos de IA e não consome tokens de APIs de IA. Precisa de computador ligado, internet e usuário conectado ao Windows.

## Estado do projeto

Protótipo em desenvolvimento. A persistência de login Gupy foi validada na instalação privada de origem. O envio autônomo completo ainda não foi validado em uma vaga real elegível. Testes simulados e uma candidatura anterior assistida não comprovam esse envio.

## Recursos

- Coleta no Indeed via JobSpy e no Freehire, com limites de tempo por fonte.
- Foco em desenvolvimento júnior, estágio e suporte técnico N1 remoto no Brasil.
- Salário divulgado e requisitos verificáveis como condições de envio.
- Histórico SQLite, prevenção de duplicatas e painel HTML local.
- Adaptador inicial Gupy para telas reconhecidas; perguntas desconhecidas ficam pendentes.
- Respostas exatas configuradas pelo candidato, sem geração de respostas por IA.
- Agendamento opcional pelo Windows.

## Instalação no Windows

Requer Python 3.12 e Google Chrome. A instalação de origem usa Python 3.12.14. Na raiz do projeto, execute em PowerShell:

```powershell
powershell -File scripts/windows/Setup.ps1
```

Se `python` não estiver no PATH, use `-PythonExecutable "CAMINHO_DO_PYTHON"`. O instalador cria `.venv-local`, instala dependências e inicializa a configuração privada. Não substitui configuração existente nem instala agendamento.

1. Edite `.local-jobs/config.json` seguindo [CONFIGURACAO.md](docs/CONFIGURACAO.md).
2. Registre seu perfil e fatos comprovados em `documents/`, ignorado pelo Git.
3. Use `scripts/windows/Testar-Sem-Enviar.cmd` para coletar e avaliar.
4. Configure login e verificação da sessão; confira seu currículo antes de habilitar envios.

O exemplo começa com `auto_apply: false`, `profile_confirmed: false` e sem textos pessoais. Esta pasta não contém currículos, credenciais ou sessões.

## Comandos

```powershell
.venv-local\Scripts\python.exe -m tools.local_jobs.main init
.venv-local\Scripts\python.exe -m tools.local_jobs.main doctor
.venv-local\Scripts\python.exe -m tools.local_jobs.main run --no-submit
.venv-local\Scripts\python.exe -m tools.local_jobs.main report
.venv-local\Scripts\python.exe -m tools.local_jobs.main login-managed
.venv-local\Scripts\python.exe -m tools.local_jobs.main session-check
```

Os atalhos ficam em `scripts/windows/`. O painel gerado fica em `reports/local-jobs/painel.html`.

## Testes e publicação

```powershell
.venv-local\Scripts\python.exe -m unittest discover -s tests -p "test_*.py"
git add .
.venv-local\Scripts\python.exe tools/check_public_files.py
```

A checagem examina o conteúdo preparado para commit; também é executada no CI. Leia [PUBLICACAO.md](docs/PUBLICACAO.md). Não envie um ZIP da instalação privada.

## Limitações

Cobertura parcial dos portais. Apenas o formato Gupy observado possui adaptador de envio. Login vencido, CAPTCHA, perguntas desconhecidas, termos novos, salário ausente e requisitos incertos viram pendências. Não há resolução de CAPTCHA, cópia de sessão do navegador cotidiano ou respostas inventadas. Falha durante envio exige conferência manual antes de repetir. O bot não escolhe nem troca automaticamente PDFs de currículo por função.

Mais detalhes: [arquitetura](docs/ARQUITETURA.md), [uso local](docs/USO_LOCAL.md) e [segurança](SECURITY.md).

## Origem e licença

Desenvolvido a partir de uma instalação personalizada de [ai-job-search](https://github.com/MadsLorentzen/ai-job-search), referenciada pelo [fork utilizado](https://github.com/igorsilvadev01/ai-job-search). Esta distribuição reúne o bot local sem o perfil, documentos e histórico daquela instalação. Os avisos MIT foram preservados. Consulte [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
