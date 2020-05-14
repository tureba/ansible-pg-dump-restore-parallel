# Migração

Este é um repositório com playbooks e scripts de migração de PostgreSQL em
paralelo. A razão principal dele existir é o fato de que mesmo o
pg\_dump/pg\_restore paralelo (-j) usa apenas uma conexão para tabelas grandes.
É possível que essa restrição não exista no futuro [1], mas por enquanto a
solução seria exportar tabelas grandes com COPYs diferentes.

Exemplo de execução da playbook paralela:

> ansible-playbook -f 3 -i inventory.yml limpa.yml migra-paralelo.yml

1. [Parallel COPY, planejado para PG v14](https://www.postgresql.org/message-id/CAA4eK1%2BkpddvvLxWm4BuG_AhVvYz8mKAEa7osxp_X0d4ZEiV%3Dg%40mail.gmail.com)

TODO:

* melhorar amarração com o inventário e variáveis
* mover o async\_status dos dumps para antes dos respectivos restores, assim o
restore inicia enquanto os dumps de outras partes ainda estão em andamento

