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
**Ferramentas**: Google Sheets, DevTools, OBS (Print de telas)

## 1. Análise inicial da aplicação

Aplicação web simples com 2 fluxos principais:
- **Página inicial**: Botões "Listar Cursos" e "Cadastrar Curso" 
- **Cadastro (/new-course)**: Formulário com campos Nome, Descrição, Data Inicial, Data Final, Número de Vagas, tipo de curso onde dependendo do tipo: online/presencial abre o campo de cadastro para link(online) ou endereço(presencial.
- 
- **Listagem**: Tabela com cursos cadastrados + botão "Excluir" por curso

**Riscos identificados**: Validação de dados inconsistente (tipos, ranges, obrigatoriedade), persistência local inconsistente, UX com mensagens que não condizem com a função desejada, sem a real execução da função solicitada e desejada.

## 2. Estratégia de testes

**Priorização**: Fluxo end-to-end → Validações (tipos, ranges, vazios) → Persistência  
**Cobertura**: 100% fluxos + **5 bugs críticos** encontrados  
**Tipos**: Funcionais, validação dados, usabilidade, exploratorios

## Casos de Teste - Cobertura Completa

**Total**: 11 casos | **Positivos**: 5 | **Negativos**: 6 | **Exploratórios**: 1  
**Taxa de Falha**: 63.64% (7 falhas em 11 casos)

### Resumo Executivo por Módulo

| Módulo | Total | Pass | Fail | Cobertura |
|--------|-------|------|------|-----------|
| Inicial/Navegação | 2 | 2 | 0 | 100% ✅ |
| Cadastro (Positivo) | 1 | 1 | 0 | 100% ✅ |
| Cadastro (Validações) | 5 | 0 | 5 | 0% ❌ |
| Listagem | 2 | 2 | 0 | 100% ✅ |
| Exclusão | 1 | 0 | 1 | 0% ❌ |
| Persistência | 1 | 1 | 0 | 100% ✅ |
| **TOTAL** | **11** | **6** | **7** | **63.64%** |

### Detalhe de Cada Caso de Teste

#### **CT-001: Carregar Aplicação**
- **Tipo**: Positivo
- **Módulo**: Inicial
- **Objetivo**: Validar carregamento básico
- **Resultado**: ✅ PASS

#### **CT-002: Acessar Formulário Cadastro**
- **Tipo**: Positivo
- **Módulo**: Navegação
- **Objetivo**: Verificar rota /new-course
- **Resultado**: ✅ PASS

#### **CT-003: Cadastro Completo Válido**
- **Tipo**: Positivo
- **Módulo**: Cadastro
- **Objetivo**: Fluxo feliz com dados válidos
- **Pré-condição**: Formulário carregado
- **Dados**: Nome: "React Avançado" | Desc: "Curso 40h" | Ini: 01/04/26 | Fim: 30/04/26 | Vagas: 30
- **Resultado Esperado**: Salva e redireciona para listagem
- **Resultado Obtido**: ✅ PASS - Salvou corretamente
- **Status**: ✅ PASS

#### **CT-004: Data Inicial Maior que Final**
- **Tipo**: Negativo
- **Módulo**: Cadastro - Validação
- **Objetivo**: Rejeitar datas incoerentes
- **Dados**: DataInicial: 15/04/26 | DataFinal: 10/04/26
- **Resultado Esperado**: Bloqueia; exibe erro "Data inválida"
- **Resultado Obtido**: ❌ FAIL - Salvou curso com datas trocadas
- **Status**: ❌ FAIL → BUG-001
- **Severity**: Crítica

#### **CT-005: Número de Vagas Igual a Zero**
- **Tipo**: Negativo
- **Módulo**: Cadastro - Validação
- **Objetivo**: Garantir mínimo 1 vaga
- **Dados**: Vagas: 0
- **Resultado Esperado**: Rejeita; "Mínimo 1 vaga obrigatório"
- **Resultado Obtido**: ❌ FAIL - Salvou com 0 vagas
- **Status**: ❌ FAIL → BUG-002
- **Severity**: Alta

#### **CT-006: Cadastro Totalmente Vazio**
- **Tipo**: Negativo
- **Módulo**: Cadastro - Validação
- **Objetivo**: Validar campos obrigatórios
- **Dados**: Todos vazios
- **Resultado Esperado**: Bloqueia; lista campos obrigatórios
- **Resultado Obtido**: ❌ FAIL - Criou curso vazio
- **Status**: ❌ FAIL → BUG-004
- **Severity**: Crítica

#### **CT-007: Listagem Após Cadastro**
- **Tipo**: Positivo
- **Módulo**: Listagem
- **Objetivo**: Novo curso aparece na tabela
- **Pré-condição**: Curso salvo em CT-003
- **Resultado Esperado**: Cursos aparecem com dados corretos
- **Resultado Obtido**: ✅ PASS - Lista atualizada
- **Status**: ✅ PASS

#### **CT-008: Excluir Curso Existente**
- **Tipo**: Positivo
- **Módulo**: Exclusão
- **Objetivo**: Remover curso da lista
- **Pré-condição**: Curso listado
- **Passos**: (1) Clicar botão Excluir; (2) Confirmar
- **Resultado Esperado**: Mensagem sucesso; curso remove-se da tabela
- **Resultado Obtido**: ❌ FAIL - Mensagem OK mas curso permanece
- **Status**: ❌ FAIL → BUG-003
- **Severity**: Crítica

#### **CT-009: Persistência Após Refresh**
- **Tipo**: Positivo
- **Módulo**: Persistência
- **Objetivo**: Dados sobrevivem F5
- **Passos**: (1) Cadastrar; (2) F5; (3) Verificar
- **Resultado Esperado**: Cursos permanecem; excluídos removem-se
- **Resultado Obtido**: ⚠️ PARCIAL - Cadastros OK; exclusões não removem
- **Status**: ⚠️ PARCIAL (conectado ao BUG-003)

#### **CT-010: Tipos campos inválido**
- **Tipo**: Negativo
- **Módulo**: Listagem
- **Objetivo**: Testar aceitação de caracteres alfanumericos nos campos
- **Pré-condição**: modulo de cadastro de cursos
- **Resultado Esperado**: Não aceitação de numeros nos cadastros de nomes
- **Resultado Obtido**:❌ FAIL - BUG-005
- **Status**: ❌ FAIL

#### **CT-011: Responsividade Mobile**
- **Tipo**: Exploratório
- **Módulo**: Usabilidade
- **Objetivo**: Testar tela 320px
- **Passos**: Redimensionar browser 320x568
- **Resultado Esperado**: Layout fluido, sem overflow
- **Resultado Obtido**: ✅ PASS - Responsivo OK
- **Status**: ✅ PASS




**[Planilha de Casos de Teste]([https://docs.google.com/spreadsheets/d/SEU_LINK_AQUI/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1hY-h1qCrzDtnJo0FyNS_NcEBM9FM_cwVTNtuejv_cKQ/edit?usp=sharing))**


## 3. Bugs encontrados (resumo)

| ID | Título | Severidade | Impacto |
|----|--------|------------|---------|
| BUG-001 | Aceita Data Inicial > Data Final | **Crítica** | Dados incoerentes |
| BUG-002 | Permite Vagas = 0 ou vazias | **Alta** | Gestão de vagas falha |
| BUG-003 | Exclusão mostra sucesso mas não remove | **Crítica** | Dados fantasmas |
| BUG-004 | Cadastro sem nenhum campo preenchido | **Crítica** | Integridade zero |
| BUG-005 | Sem validação tipo campos | **Alta** | Dados Poluidos |


**Impacto do BUG-005 na análise**
Este bug reforça padrão: validação inexistente. Dados poluídos (números em nomes, texto em vagas) quebram relatórios, buscas futuras e UX. Severidade Alta por afetar integridade a longo-prazo da aplicação.

**[Evidências completas](https://drive.google.com/drive/folders/14zFOtVxGqfOiIofbeFvcHhpaEazZ9N2M?usp=drive_link)**

## 4. Uso de IA no desafio

Utilizada  IA como apoio para:
- Estruturar documentação (README, tabelas)
- Validar cobertura de cenários com a utilização de boas práticas QA
- Padronizar nomenclatura de bugs

**Minha análise pessoal**: Executei todos os testes manualmente, onde identifiquei os 05 bugs reais da aplicação e defini severidades baseado no impacto de negócio. Ajustei sugestões da IA para refletir comportamentos específicos observados, ajustando sugestões para a realidade da aplicação.

## 5. Lições aprendidas

Foco em qualidade > quantidade de testes. Validações de negócio (datas, vagas) são mais críticas que validações genéricas de formato.

