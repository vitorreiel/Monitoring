# Monitoramento com Zabbix, Prometheus, Grafana e Node Exporter

Este projeto configura um ambiente de monitoramento utilizando **Docker** e **Docker Compose**. Ele inclui os seguintes serviços:

## Requisitos

- **Sistema Operacional**: Linux (preferencialmente com terminal Bash).
- **Docker** ([Guia de instalação](https://docs.docker.com/get-docker/)).
- **Docker Compose** ([Guia de instalação](https://docs.docker.com/compose/install/)).

## Serviços

1. **MySQL**
   - Banco de dados para o servidor Zabbix.
   - Exposição das portas: `3306`, `33060`.

2. **Zabbix Server**
   - Coleta dados de monitoramento enviados pelos agentes Zabbix.
   - Porta: `10051`.

3. **Zabbix Agent**
   - Instalado nos hosts monitorados para enviar métricas ao servidor Zabbix.

4. **Interface Web do Zabbix (Nginx)**
   - Fornece uma interface gráfica para gerenciar e visualizar os dados de monitoramento.
   - Portas: `80`, `443`.

5. **Grafana**
   - Dashboard para visualização de dados de monitoramento.
   - Inclui o plugin Zabbix.
   - Porta: `3000`.

6. **Prometheus**
   - Coleta e armazena métricas de diversos serviços.
   - Configurado para monitorar o Zabbix Agent, MySQL e Node Exporter.
   - Porta: `9090`.

7. **Node Exporter**
   - Fornece métricas do sistema operacional do host.
   - Porta: `9100`.

## Configuração de Rede

- Todos os serviços estão conectados a uma rede Docker personalizada (`zabbix-network`), com endereços IP estáticos atribuídos a cada container.

## Volumes

- A persistência dos dados é garantida utilizando volumes Docker:
  - `mysql_data`: Armazena os dados do MySQL.
  - `grafana_data`: Armazena as configurações do Grafana.
  - `prometheus_data`: Armazena as configurações do Prometheus.

## Arquivo `.env`

- O projeto utiliza um arquivo `.env` para configurar variáveis de ambiente como credenciais de banco de dados, configurações do Zabbix e outros valores importantes.
- Um exemplo de arquivo `.env` já está incluído no repositório com valores ajustados para facilitar a configuração inicial.
- Todos os valores podem ser personalizados de acordo com suas necessidades específicas. Certifique-se de revisar e ajustar as variáveis conforme necessário antes de iniciar os serviços.

## Como Usar

1. Clone este repositório:
  ```bash
   git clone https://github.com/vitorreiel/Monitoring.git
   cd Monitoring
   docker compose up -d
  ```
2. Importar o dashboard para o Grafana:
    - Acesse o Grafana através da interface web `<seu-ip:3000>` e faça login com as credenciais padrão:
        - **Login:** `admin`
        - **Password:** `admin`
    - Localize o arquivo `dashboard.json` dentro da pasta `prometheus` no repositório.
    - Importe o dashboard no Grafana:
        - No menu principal, vá até **Dashboards** > **Import**.
        - Faça o upload do arquivo `dashboard.json` ou copie e cole o conteúdo do arquivo na área de texto disponibilizada.
        - Clique em **Load** e configure as opções conforme necessário.
<br>
3. Configuração na interface do Zabbix:
    - Pode ser necessário configurar manualmente o IP do container Zabbix Agent na interface web do Zabbix.
    - Acesse a interface web do Zabbix em `<seu-ip:80>` e faça login com as credenciais padrão:
        - **Login:** `Admin`
        - **Password:** `zabbix`   
    - Configure o IP do agente:
        - Navegue até **Monitoring** > **Hosts**.
        - Localize e clique em **Zabbix server**.
        - Em **Hosts**, no campo **Interfaces**, localize o tipo **Agent**.
        - No campo **IP address**, insira o IP do container do Zabbix Agent (no exemplo, `172.22.0.5`).
        - Clique em **Update** para salvar as alterações.
---

<div style="display: inline_block;">

   ![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge)

</div>
<div style="display: inline_block;">
   <img height="30" width="30" hspace="7" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mysql/mysql-original.svg" />
   <img height="34" width="34" hspace="7" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-plain-wordmark.svg" />
   <img height="34" width="30" hspace="7" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/grafana/grafana-original.svg" />
   <img height="34" width="30" hspace="7" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/prometheus/prometheus-original.svg" />
</div>