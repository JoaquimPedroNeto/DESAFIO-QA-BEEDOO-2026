# DESAFIO-QA-BEEDOO-2026
Esse e meu DESAFIO-QA-BEEDOO-2026 

• Exploração inicial da aplicação do link: https://creative-sherbet-a51eac.netlify.app/

-> Trata-se de uma página para a apresentação da 'Lista de Cursos' e a realização do 'Cadastrar Curso', com duas principais funções apresentadas na tela inicial da aplicação. 

• As funcionalidades apresentadas na aplicação são 02: 
- 01° Função botão 'LISTAR CURSOS' - botão para a listagem de cursos que serão cadastrados na aplicação;
- 02° Função botão 'CADASTRAR CURSO' - botão para realizar o cadastramento dos cursos que serão apresentados ao realizar o click no botão 01 - 'LISTAR CURSOS'.

---------------

**Aplicação testada**: [Cadastro e Listagem de Cursos](https://creative-sherbet-a51eac.netlify.app/)  
**Período de teste**: 08/03/2026  
**Ambiente**: Chrome v122, Windows 11, 1920x1080  
**Ferramentas**: Google Sheets, DevTools, OBS (gravações)

## 1. Análise inicial da aplicação

Aplicação web simples com 2 fluxos principais:
- **Página inicial**: Botões "Listar Cursos" e "Cadastrar Curso" 
- **Cadastro (/new-course)**: Formulário com campos Nome, Descrição, Data Inicial, Data Final, Número de Vagas
- **Listagem**: Tabela com cursos cadastrados + botão "Excluir" por curso

**Riscos identificados**: Validação de dados inconsistente, persistência local frágil, UX com mensagens que não condizem com a função desejada, sem a real execução da função solicitada e desejada.

## 2. Estratégia de testes

**Priorização**: Fluxo crítico (cadastro → listagem → exclusão) → Validações → Casos extremos  
**Cobertura**: 100% dos fluxos principais, 4 bugs críticos encontrados  
**Tipos aplicados**: Funcionais, validação de dados, usabilidade, exploratórios

**[Planilha de Casos de Teste](https://docs.google.com/spreadsheets/d/SEU_LINK_AQUI/edit?usp=sharing)**

## 3. Bugs encontrados (resumo)

| ID | Título | Severidade | Impacto |
|----|--------|------------|---------|
| BUG-001 | Aceita Data Inicial > Data Final | **Crítica** | Dados incoerentes |
| BUG-002 | Permite Vagas = 0 ou vazias | **Alta** | Gestão de vagas falha |
| BUG-003 | Exclusão mostra sucesso mas não remove | **Crítica** | Dados fantasmas |
| BUG-004 | Cadastro sem nenhum campo preenchido | **Crítica** | Integridade zero |

**[Evidências completas](https://drive.google.com/drive/folders/SEU_LINK_DRIVE?usp=sharing)**

## 4. Uso de IA no desafio

Utilizei IA como apoio para:
- Estruturar documentação (README, tabelas)
- Validar cobertura de cenários com a utilização de boas práticas QA
- Padronizar nomenclatura de bugs

**Minha análise pessoal**: Executei todos os testes manualmente, onde identifiquei os 4 bugs reais da aplicação e defini severidades baseado no impacto de negócio. Ajustei sugestões da IA para refletir comportamentos específicos observados.

## 5. Lições aprendidas

Foco em qualidade > quantidade de testes. Validações de negócio (datas, vagas) são mais críticas que validações genéricas de formato.

