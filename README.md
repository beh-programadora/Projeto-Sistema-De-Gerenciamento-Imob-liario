# Projeto Imobiliária

Este projeto é um sistema de gerenciamento para uma imobiliária, implementado usando MySQL. O banco de dados é estruturado para armazenar informações sobre propriedades, clientes, agentes e transações de compra e aluguel.

## Estrutura do Banco de Dados

O banco de dados `ImobiliariaDB` contém as seguintes tabelas:

1. **Propriedades**
   - `id_propriedade`: ID da propriedade (chave primária)
   - `endereco`: Endereço da propriedade
   - `tipo`: Tipo de propriedade (Casa, Apartamento, Terreno)
   - `valor`: Valor da propriedade
   - `status`: Status da propriedade (Disponível, Vendido, Alugado)

2. **Clientes**
   - `id_cliente`: ID do cliente (chave primária)
   - `nome`: Nome do cliente
   - `telefone`: Telefone do cliente
   - `email`: Email do cliente
   - `tipo_interesse`: Tipo de interesse do cliente (Compra, Aluguel)

3. **Agentes**
   - `id_agente`: ID do agente (chave primária)
   - `nome`: Nome do agente
   - `telefone`: Telefone do agente
   - `email`: Email do agente

4. **Transações**
   - `id_transacao`: ID da transação (chave primária)
   - `id_cliente`: ID do cliente (chave estrangeira)
   - `id_propriedade`: ID da propriedade (chave estrangeira)
   - `id_agente`: ID do agente (chave estrangeira)
   - `data_transacao`: Data da transação
   - `tipo_transacao`: Tipo de transação (Compra, Aluguel)
   - `valor`: Valor da transação

## Consultas Exemplos

- Listar todas as propriedades disponíveis:
  ```sql
  SELECT 
      id_propriedade AS ID_Propriedade,
      endereco AS Endereco,
      tipo AS Tipo,
      valor AS Valor,
      status AS Status
  FROM 
      Propriedades
  WHERE 
      status = 'Disponível';
  
Listar todas as transações de compras:
SELECT 
    t.id_transacao AS ID_Transacao,
    c.nome AS Nome_Cliente,
    p.endereco AS Endereco_Propriedade,
    a.nome AS Nome_Agente,
    t.data_transacao AS Data_Transacao,
    t.valor AS Valor
FROM 
    Transacoes t
JOIN 
    Clientes c ON t.id_cliente = c.id_cliente
JOIN 
    Propriedades p ON t.id_propriedade = p.id_propriedade
JOIN 
    Agentes a ON t.id_agente = a.id_agente
WHERE 
    t.tipo_transacao = 'Compra';
    
Consultar detalhes completos de uma transação específica:
SELECT 
    t.id_transacao AS ID_Transacao,
    c.nome AS Nome_Cliente,
    p.endereco AS Endereco_Propriedade,
    a.nome AS Nome_Agente,
    t.data_transacao AS Data_Transacao,
    t.tipo_transacao AS Tipo_Transacao,
    t.valor AS Valor
FROM 
    Transacoes t
JOIN 
    Clientes c ON t.id_cliente = c.id_cliente
JOIN 
    Propriedades p ON t.id_propriedade = p.id_propriedade
JOIN 
    Agentes a ON t.id_agente = a.id_agente
WHERE 
    t.id_transacao = 1;  -- Substitua 1 pelo ID da transação desejada
    
Atualizações e Exclusões

Alterar o status de uma propriedade para 'Vendido':
UPDATE Propriedades
SET status = 'Vendido'
WHERE id_propriedade = <id_propriedade>;  -- Substitua <id_propriedade> pelo ID da propriedade

Atualizar o telefone de um cliente:
UPDATE Clientes
SET telefone = '9999-8888'
WHERE id_cliente = <id_cliente>;  -- Substitua <id_cliente> pelo ID do cliente

Excluir um cliente:
DELETE FROM Clientes
WHERE id_cliente = <id_cliente>;  -- Substitua <id_cliente> pelo ID do cliente

Instalação
1. Clone este repositório:

git clone https://github.com/usuario/imobiliariadb.git

2. Importe o script SQL no seu servidor MySQL.

3. Execute as consultas SQL fornecidas para popular e manipular o banco de dados.

   Licença
Este projeto está licenciado sob a Licença MIT.


