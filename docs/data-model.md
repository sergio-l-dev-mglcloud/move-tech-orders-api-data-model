# Modelo de Dados

## Tabela: `orders`
Armazena o cabeçalho e o estado dos pedidos da aplicação.

| Coluna | Tipo de Dado | Restrições | Descrição |
| :--- | :--- | :--- | :--- |
| `id` | VARCHAR | PRIMARY KEY | Identificador único do pedido (UUID) |
| `customer` | VARCHAR | NOT NULL | Nome do cliente |
| `status` | VARCHAR | DEFAULT 'open' | Status atual do pedido |
| `created_at` | TIMESTAMP WITH TIME ZONE | DEFAULT NOW() | Data e hora da criação |

---

## Tabela: `items`
Armazena os itens vinculados a um pedido.

| Coluna | Tipo de Dado | Restrições | Descrição |
| :--- | :--- | :--- | :--- |
| `id` | VARCHAR | PRIMARY KEY | Identificador único do item (UUID) |
| `order_id` | VARCHAR | FOREIGN KEY (`orders.id`), NOT NULL | Vínculo com a tabela de pedidos |
| `sku` | VARCHAR | NOT NULL | Código do produto |
| `description` | VARCHAR | NOT NULL | Descrição do produto |
| `quantity` | INTEGER | NOT NULL | Quantidade do item |

---

## Relacionamentos e Regras

- **1:N (orders → items):** Um pedido pode possuir múltiplos itens. Cada item pertence obrigatoriamente a um único pedido.
- **Cascata:** A deleção de um registro na tabela `orders` remove automaticamente todos os registros correspondentes na tabela `items` (cascade="all, delete-orphan").