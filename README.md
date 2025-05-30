# 🧪 Teste DBA MySQL Log Manager

Seja bem-vindo(a) ao nosso desafio técnico para a vaga de **DBA MySQL** na Log Manager!

Aqui, buscamos alguém que saiba lidar com bases de alta volumetria, tuning de performance, análise de planos de execução, reestruturação de modelos e boas práticas de banco de dados em ambientes de missão crítica.

---

## 🎯 Objetivo do Desafio

Neste repositório temos um dump `.sql` com o nome de `banco.zip` com as seguintes coisas:
- **20 mil clientes**
- **200 mil pedidos**
- Dados mal estruturados de propósito
- Entre outas coisas mais

Seu papel é identificar os problemas e aplicar melhorias reais e justificáveis.

---


## 🔍 Sua missão

1. **Importar** o banco de dados em uma instância local
2. **Analisar** os problemas estruturais e de performance
3. **Executar** as queries propostas abaixo
4. **Ajustar** a estrutura do banco, índices, tipos entre outros
5. **Documentar** tudo que foi feito e por quê

---

## 🧪 Queries que você deve otimizar

### 1. Total de pedidos por status e estado do cliente:

```sql
SELECT c.estado, p.status, COUNT(*) AS total
FROM pedidos p
JOIN clientes c ON c.id = p.cliente_id
GROUP BY c.estado, p.status;
```

### 2. Ticket médio por estado nos últimos 12 meses:

```sql
SELECT c.estado, AVG(p.total) AS ticket_medio
FROM pedidos p
JOIN clientes c ON c.id = p.cliente_id
WHERE STR_TO_DATE(p.criado_em, '%d/%m/%Y %H:%i:%s') >= DATE_SUB(NOW(), INTERVAL 12 MONTH)
GROUP BY c.estado;
```

### 3. Listar os 10 clientes que mais compraram:

```sql
SELECT c.nome, SUM(p.total) AS total_gasto
FROM pedidos p
JOIN clientes c ON c.id = p.cliente_id
GROUP BY c.id
ORDER BY total_gasto DESC
LIMIT 10;
```

### 4. Pedidos com observações contendo “atraso”:

```sql
SELECT * FROM pedidos
WHERE observacoes LIKE '%atraso%';
```

## ✅ O que esperamos de você

- Diagnóstico preciso dos gargalos
- Aplicação de melhorias justificadas (alteração de tipos, adição de índices, normalização etc.)
- Clareza na explicação técnica
- Uso de ferramentas como EXPLAIN, SHOW PROFILE, ANALYZE TABLE
- Comparação de antes e depois (opcional: tempo de execução)


- Quais problemas foram encontrados
- Quais soluções foram aplicadas
- Quais os ganhos esperados ou observados

## 🧾 Entrega do Desafio

Ao finalizar o teste:

- Crie um repositório privado no GitHub com os seguintes arquivos:
- O novo .sql contendo as alterações realizadas e melhorias de performance
- Um arquivo .md ou .pdf com a explicação técnica das mudanças implementadas
- Compartilhe o repositório com o usuário do GitHub: grazianilog

Após o compartilhamento, envie o link do repositório por e-mail para: graziani@logmanager.com.br


