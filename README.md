# Modelagem Dimensional de uma Universidade

Projeto de modelagem dimensional desenvolvido para representar atividades acadêmicas de uma universidade, com foco na atuação dos professores.

O projeto transforma um modelo relacional em um **Star Schema**, permitindo análises relacionadas a professores, departamentos, cursos, disciplinas e períodos acadêmicos.

## Objetivo do projeto

Desenvolver um Data Warehouse simplificado, composto por:

- Uma tabela fato relacionada à oferta de disciplinas pelos professores;
- Tabelas de dimensão para professores, departamentos, cursos, disciplinas e datas;
- Um modelo estrela documentado;
- Scripts em MySQL para criação das tabelas e dos relacionamentos;
- Uma estrutura adequada para futuras análises e dashboards.

## Contexto analítico

O modelo foi criado para apoiar perguntas como:

- Quais disciplinas são ministradas por cada professor?
- Em quais cursos cada professor atua?
- Como os professores estão distribuídos entre os departamentos?
- Como as atividades acadêmicas evoluem ao longo do tempo?
- Quais professores atuam em múltiplos cursos ou disciplinas?
- Qual é a carga horária associada a cada professor?
- Como as atividades se distribuem entre os campi?

## Modelo relacional de origem

O modelo operacional da universidade contém as seguintes entidades principais:

- `Professor (id_professor, id_departamento)`
- `Departamento (id_departamento, nome, campus, id_professor)`
- `Curso (id_curso, id_departamento)`
- `Disciplina (id_disciplina, id_professor)`
- `DisciplinaCurso (id_disciplina, id_curso)`
- `Aluno (id_aluno)`
- `Matriculado (id_aluno, id_disciplina)`
- `PreRequisitoDisciplina (id_disciplina, id_prerequisito)`
- `PreRequisito (id_prerequisito)`

## Star Schema

### Granularidade

A granularidade representa o nível de detalhamento de cada registro da tabela fato.

Neste projeto, foi definida como:

**Uma linha de fato por professor × disciplina × curso × departamento × data.**

Essa definição permite relacionar a atuação de um professor a uma disciplina, a um curso, a um departamento e a um período específico.

## Dimensões

O modelo contém as seguintes dimensões:

- `DIM_PROFESSOR`: informações dos professores;
- `DIM_DEPARTAMENTO`: informações dos departamentos;
- `DIM_DISCIPLINA`: informações das disciplinas;
- `DIM_CURSO`: informações dos cursos;
- `DIM_DATA`: informações de tempo e calendário.

## Tabela fato

A tabela `FATO_PROFESSOR` centraliza as referências às dimensões e as medidas relacionadas às atividades dos professores.

Ela relaciona:

- Professor;
- Departamento;
- Curso;
- Disciplina;
- Data.

## Diagrama lógico

```text
                    DIM_PROFESSOR
                          |
DIM_CURSO ----- FATO_PROFESSOR ----- DIM_DISCIPLINA
                          |
                  DIM_DEPARTAMENTO
                          |
                       DIM_DATA
```

O diagrama detalhado do projeto está disponível na pasta `imagens`.

## Estrutura do repositório

```text
universidade-star_schema-sql/
├── docs/
├── imagens/
├── sql/
│   └── professor_star_schema.sql
└── README.md
```

### `docs`

Contém materiais complementares e documentação do projeto.

### `imagens`

Contém o diagrama utilizado para representar visualmente o Star Schema.

### `sql`

Contém os scripts MySQL utilizados para criar as tabelas de dimensão, a tabela fato, as chaves e os relacionamentos.

## Scripts MySQL

O arquivo principal está localizado em:

`sql/professor_star_schema.sql`

O script contempla:

- Criação das tabelas de dimensão;
- Criação da tabela fato;
- Definição das chaves primárias;
- Definição das chaves estrangeiras;
- Criação dos relacionamentos entre a tabela fato e as dimensões.

## Dicionário resumido das dimensões

### `DIM_DATA`

Dimensão utilizada para análises temporais.

Principais atributos:

- Data completa;
- Ano;
- Semestre;
- Trimestre;
- Mês;
- Nome do mês;
- Dia da semana;
- Indicador de feriado;
- Período acadêmico.

### `DIM_CURSO`

Dimensão originada da entidade Curso.

Principais atributos:

- `nome_curso`;
- `tipo_curso`;
- `modalidade`;
- `carga_horaria_total`;
- `data_criacao`.

### `DIM_DISCIPLINA`

Dimensão originada da entidade Disciplina.

Principais atributos:

- `nome_disciplina`;
- `codigo_disciplina`;
- `carga_horaria`;
- `creditos`;
- `tipo_disciplina`;
- `nivel`;
- `possui_prerequisito`;
- `data_criacao`.

### `DIM_DEPARTAMENTO`

Dimensão originada da entidade Departamento.

Principais atributos:

- `nome_departamento`;
- `campus`;
- `sigla`;
- `data_criacao`.

### `DIM_PROFESSOR`

Dimensão originada da entidade Professor.

Principais atributos:

- `nome_professor`;
- `titulacao`;
- `ano_ingresso`;
- `status`;
- `data_criacao`.

## Estrutura da tabela `FATO_PROFESSOR`

### Chave primária

- `id_fato`: identificador único da tabela fato, definido como `AUTO_INCREMENT`.

### Chaves estrangeiras

- `id_professor` → `DIM_PROFESSOR`;
- `id_departamento` → `DIM_DEPARTAMENTO`;
- `id_curso` → `DIM_CURSO`;
- `id_disciplina` → `DIM_DISCIPLINA`;
- `id_data` → `DIM_DATA`.

### Medidas e indicadores

- `qtd_disciplinas_ministradas`;
- `qtd_cursos_envolvidos`;
- `qtd_prerequisitos_ministrados`;
- `indicador_coordenador`.

## Análises possíveis

A partir desse modelo, podem ser construídas análises como:

- Carga horária por professor;
- Quantidade de professores por departamento;
- Evolução temporal das atividades acadêmicas;
- Ranking de professores por carga horária;
- Identificação de professores multidisciplinares;
- Análise de pré-requisitos por professor;
- Comparação entre departamentos;
- Distribuição das atividades por campus;
- Quantidade de cursos associados a cada professor;
- Participação dos professores ao longo dos períodos acadêmicos.

## Tecnologias utilizadas

- MySQL;
- SQL;
- Modelagem dimensional;
- Star Schema;
- Git;
- GitHub.

## Competências demonstradas

Este projeto demonstra conhecimentos em:

- Modelagem de dados;
- Conversão de um modelo relacional para dimensional;
- Definição de granularidade;
- Criação de tabelas fato e dimensão;
- Definição de chaves primárias e estrangeiras;
- Integridade referencial;
- Organização de scripts SQL;
- Documentação técnica;
- Estruturação de dados para Business Intelligence.

## Como executar

1. Faça o download ou clone este repositório.
2. Abra o MySQL Workbench ou outro cliente compatível com MySQL.
3. Localize o script na pasta `sql`.
4. Execute o script de criação do modelo dimensional.
5. Confira as tabelas e os relacionamentos criados.
6. Consulte o diagrama da pasta `imagens` para visualizar a estrutura do modelo.

## Próximas melhorias

- Adicionar dados fictícios para testes;
- Criar consultas analíticas;
- Desenvolver views para indicadores recorrentes;
- Adicionar índices para otimização;
- Validar as medidas da tabela fato;
- Construir um dashboard no Power BI;
- Documentar exemplos de resultados obtidos;
- Incluir um diagrama atualizado no início do README.

## Origem do projeto

Projeto desenvolvido como parte de um desafio de modelagem dimensional, organizado e documentado para composição de portfólio profissional.

## Autor

**Roddy Ramos Gonzáles**

- [GitHub](https://github.com/RoddyRamosG)
- [LinkedIn](https://www.linkedin.com/in/roddy-ramos-g-38483a1a/)
