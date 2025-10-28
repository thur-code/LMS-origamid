# 🧩 LMS – Banco de Dados com SQLite (Curso Origamid)

Projeto desenvolvido como parte do curso **[SQLite Fundamentos](https://www.origamid.com/curso/sqlite-fundamentos/)** da Origamid.  
O objetivo foi **criar um banco de dados completo e funcional**, modelando um sistema de aprendizado online (LMS — *Learning Management System*) para praticar os principais conceitos de **SQL** e **SQLite**.

---

## 🗃️ Estrutura do projeto

```
LMS/
├── lms.sql # Script completo com criação de tabelas, índices, views e triggers
├── lms.sqlite # Banco de dados pronto e populado
├── lms.sqlite-shm # Arquivo auxiliar gerado automaticamente pelo SQLite
└── lms.sqlite-wal # Arquivo de log gerado automaticamente
```


O projeto foi desenvolvido e testado utilizando o **Visual Studio Code** com a extensão **SQLite Viewer**, o que permite visualizar tabelas, dados e executar queries diretamente no editor.

---

## 🧱 Modelagem do banco

O banco foi projetado para representar um sistema de **ensino online (LMS)**, com usuários, cursos, aulas, certificados e autenticação.

### 📋 Principais tabelas
| Tabela | Descrição |
|--------|------------|
| `users` | Cadastro de usuários do sistema |
| `sessions` | Sessões de login ativas |
| `resets` | Tokens de recuperação de senha |
| `courses` | Cursos disponíveis na plataforma |
| `lessons` | Aulas pertencentes a cada curso |
| `lessons_completed` | Aulas concluídas por cada usuário |
| `certificates` | Certificados gerados após conclusão de cursos |

---

## 🛠 Tecnologias utilizadas

- **SQLite 3** (estrutura relacional leve)
- **SQL padrão ANSI**
- **VS Code** + *SQLite Viewer Extension*
- **Triggers, Views e Índices**
- **PRAGMA** e otimizações de desempenho

---

## 🎯 Conceitos aplicados

Durante a construção do projeto, foram aplicados:

### 🔹 Estrutura e modelagem
- Criação de tabelas com `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE` e `CHECK`
- Uso de `STRICT` e `WITHOUT ROWID` para maior consistência e performance
- Normalização das entidades (1ª, 2ª e 3ª formas normais)

### 🔹 Consultas SQL (DML)
- `SELECT`, `INSERT`, `UPDATE`, `DELETE`
- Filtros e operadores: `WHERE`, `LIKE`, `IN`, `BETWEEN`
- `JOIN` (INNER, LEFT, CROSS) para unir tabelas relacionadas
- Funções agregadas: `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`

### 🔹 Índices e otimização
- Criação de índices compostos (`CREATE INDEX`)
- Uso de `PRAGMA` para análise e performance (`ANALYZE`, `CACHE_SIZE`, etc.)

### 🔹 Views e Triggers
- Views para consultas complexas (ex.: progresso de cursos, certificados emitidos)
- Triggers automáticas para atualização de datas (`set_users_updated`)

---

## 🧩 Exemplo de estrutura

```sql
CREATE TABLE "users" (
  "id" INTEGER PRIMARY KEY,
  "name" TEXT NOT NULL,
  "password_hash" TEXT NOT NULL,
  "email" TEXT NOT NULL COLLATE NOCASE UNIQUE,
  "username" TEXT NOT NULL COLLATE NOCASE UNIQUE,
  "created" TEXT NOT NULL DEFAULT CURRENT_TIMESTAMP,
  "updated" TEXT NOT NULL DEFAULT CURRENT_TIMESTAMP
) STRICT;

CREATE TABLE "courses" (
  "id" INTEGER PRIMARY KEY,
  "slug" TEXT NOT NULL UNIQUE,
  "title" TEXT NOT NULL,
  "lessons" INTEGER NOT NULL,
  "hours" INTEGER NOT NULL
);
```

---

## Exemplo de consulta

```-- Exibe certificados completos (usuário + curso)
SELECT c.id, u.name, cr.title, c.completed
FROM certificates AS c
JOIN users AS u ON c.user_id = u.id
JOIN courses AS cr ON c.course_id = cr.id;
```

---

## 📂 Status do projeto
✅ Concluído

📦 Banco de dados funcional

🧠 Inclui scripts SQL e banco populado

---

## 📝 Observações

Este projeto foi desenvolvido de forma guiada durante o curso da Origamid.
O foco foi aprender e aplicar os conceitos fundamentais do SQLite, explorando desde a criação do schema até a execução de consultas reais.
O banco segue o modelo proposto pelo instrutor, com melhorias de legibilidade e estrutura.

