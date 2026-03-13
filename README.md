# Teste de Performance - BlazeDemo

## Objetivo

O objetivo deste teste é avaliar o comportamento da aplicação disponível em:

https://www.blazedemo.com

O cenário simulado consiste no fluxo completo de compra de uma passagem aérea.

## Cenário Testado

O fluxo automatizado simula um usuário realizando:

1. Acesso à página inicial
2. Busca por voos disponíveis
3. Compra de uma passagem aérea

Esse fluxo representa o processo completo de compra de passagem no sistema.

---

# Ferramenta Utilizada

Os testes foram desenvolvidos utilizando:

Apache JMeter 5.6.3

A ferramenta foi escolhida por permitir simular múltiplos usuários simultâneos e coletar métricas importantes de performance como:

- Throughput
- Tempo médio de resposta
- Taxa de erro
- Percentis
- Latência

---

# Estrutura do Script

O plano de teste foi dividido em dois tipos de teste:

- **Load Test**
- **Spike Test**

Cada um com um objetivo específico de análise de comportamento do sistema.

---

# Configuração do Load Test

O Load Test foi configurado para atingir aproximadamente **250 requisições por segundo**, conforme solicitado no critério de aceitação.

Para garantir essa taxa foi utilizado o elemento:

**Constant Throughput Timer**

Configuração:

| Parâmetro | Valor |
|----------|------|
| Usuários Virtuais | 300 |
| Ramp-up | 5 segundos |
| Loop | 50 |
| Throughput alvo | 15000 requisições/minuto (~250 req/s) |

---

## Resultado do Load Test

Resumo da execução:

| Métrica | Valor |
|-------|------|
| Total de requisições | 61.500 |
| Throughput | 260.8 req/s |
| Tempo médio de resposta | 504 ms |
| Tempo máximo | 9089 ms |
| Taxa de erro | 0% |

Tempo médio por operação:

| Requisição | Tempo médio |
|-----------|------------|
| Open Home | 511 ms |
| Search Flights | 501 ms |
| Purchase Flight | 501 ms |

### Análise

O sistema apresentou estabilidade durante toda a execução do teste.

Observações:

- Throughput superior ao requisito mínimo de **250 requisições por segundo**
- Tempo médio de resposta inferior a **1 segundo**
- Nenhuma ocorrência de erro durante a execução

Portanto, **o critério de aceitação foi atendido no Load Test**.

---

# Spike Test

O Spike Test tem como objetivo avaliar o comportamento do sistema diante de um aumento repentino de carga.

Diferente do Load Test, onde a carga cresce gradualmente, no Spike Test os usuários são iniciados praticamente ao mesmo tempo, simulando picos inesperados de acesso.

Exemplos reais desse cenário incluem:

- campanhas promocionais
- horários de pico
- eventos que geram acesso simultâneo massivo

## Configuração do Spike Test

| Parâmetro | Valor |
|----------|------|
| Usuários Virtuais | 500 |
| Ramp-up | 1 segundo |
| Loop | 5 |

Neste teste **não foi utilizado controle de throughput**, permitindo que o sistema recebesse uma carga repentina.

---

## Resultado do Spike Test

Resumo da execução:

| Métrica | Valor |
|-------|------|
| Total de requisições | 7.500 |
| Throughput | 258.7 req/s |
| Tempo médio de resposta | 1416 ms |
| Tempo máximo | 7832 ms |
| Taxa de erro | 0% |

Tempo médio por operação:

| Requisição | Tempo médio |
|-----------|------------|
| Open Home | 1461 ms |
| Search Flights | 1397 ms |
| Purchase Flight | 1390 ms |

### Análise

Durante o Spike Test o sistema recebeu um aumento abrupto de carga.

Observações:

- Throughput manteve-se próximo de **250 req/s**
- Tempo médio de resposta aumentou em relação ao Load Test
- Nenhuma falha ou erro foi registrado

Isso indica que o sistema possui **boa capacidade de absorver picos de tráfego sem falhas**, embora com aumento natural no tempo de resposta.

---

# Conclusão

Com base nos resultados obtidos:

### Load Test
✔ Critério de aceitação atingido  
✔ Throughput acima de 250 req/s  
✔ Tempo médio abaixo de 1 segundo  
✔ Nenhum erro registrado  

### Spike Test
✔ Sistema suportou aumento repentino de carga  
✔ Nenhum erro registrado  
✔ Houve aumento no tempo de resposta, comportamento esperado em cenários de pico  

De forma geral, o sistema demonstrou **boa estabilidade e capacidade de processamento sob carga e picos de acesso**.

---

# Como Executar o Teste

1. Instalar o Apache JMeter  
https://jmeter.apache.org

2. Abrir o script:
File → Open → agibank_teste_performance.jmx

3. Executar o teste:
Clique no botão "Start"

4. Visualizar resultados em:

- Summary Report
- Aggregate Report

---

# Estrutura do Repositório
blazedemo-performance-test
│
├── README.md
├── agibank_teste_performance.jmx
└── images
     ├── load_test.png
     └── spike_test.png


---

# Considerações Finais

A combinação de **Load Test** e **Spike Test** permite obter uma visão mais completa sobre o comportamento do sistema sob diferentes padrões de tráfego, avaliando tanto sua capacidade de processamento contínuo quanto sua resiliência a picos de acesso.

## Resultados

### Load Test

![Load Test](images/load_test.png)

### Spike Test

![Spike Test](images/spike_test.png)