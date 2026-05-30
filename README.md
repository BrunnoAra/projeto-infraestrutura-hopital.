# Projeto de Infraestrutura de TI – UPA (Unidade de Pronto Atendimento)

Simulação de infraestrutura de TI hospitalar com foco em redes, segurança, servidores e continuidade de serviços críticos, seguindo boas práticas de mercado.

## 🧑‍💻 Autor e Informações
* **Autor:** Brunno Araujo dos Santos
* **Curso:** Análise e Desenvolvimento de Sistemas - UNISA
* **Data:** Maio/2025
* **Versão:** 1.0

---

## 🎯 1. Objetivo
Este projeto simula a infraestrutura de TI de uma UPA (Unidade de Pronto Atendimento), com foco em redes, segurança, servidores e continuidade de serviços críticos, seguindo boas práticas de mercado. O sistema foi projetado para garantir disponibilidade, segurança e integridade das informações, assegurando a continuidade dos serviços essenciais da UPA.
![Visão Geral do Projeto](img%20brno.jpeg)
---

## 🏢 2. Estrutura Física
Setores mapeados na planta da UPA:
* Recepção / Espera
* Triagem
* Consultórios Médicos (1, 2 e 3)
* Sala de Enfermagem
* Farmácia
* Radiologia / Imagem
* Administração
* Sala de TI / Data Center

---

## 🌐 3. Arquitetura de Rede
* **Topologia:** Estrela com Switch Core L3 central.
* **Segurança Lógica:** Switches de acesso por setor com VLAN dedicada.
* **Cabeamento:** Estruturado Cat6 - Furukawa.
* **Segurança de Borda:** Firewall perimetral FortiGate 60F.

---

## 🏷️ 4. VLANs e Plano de Endereçamento IP
Toda a rede utiliza a máscara de sub-rede `255.255.255.0` (/24).

| VLAN | Setor | Rede | Gateway | Range DHCP / IPs |
| :---: | :--- | :--- | :--- | :--- |
| **10** | Administração | `192.168.10.0` | `192.168.10.1` | `192.168.10.10 - 192.168.10.200` |
| **20** | Enfermagem | `192.168.20.0` | `192.168.20.1` | `192.168.20.10 - 192.168.20.200` |
| **30** | Consultórios | `192.168.30.0` | `192.168.30.1` | `192.168.30.10 - 192.168.30.200` |
| **40** | Radiologia | `192.168.40.0` | `192.168.40.1` | `192.168.40.10 - 192.168.40.200` |
| **99** | TI / Servidores | `192.168.99.0` | `192.168.99.1` | `192.168.99.10 - 192.168.99.200` |

---

## 🖥️ 5. Servidores e Active Directory
Os servidores estão concentrados na VLAN 99 e utilizam o **Windows Server 2022**.

### Lista de Servidores
* **DC01 (`192.168.99.10`):** AD DS Principal
* **DC02 (`192.168.99.11`):** AD DS Secundário (Redundância)
* **FS01 (`192.168.99.12`):** File Server (Servidor de Arquivos)
* **BK01 (`192.168.99.13`):** Backup Server

### Configurações do Active Directory
* Organização de usuários por setor através de Unidades Organizacionais (OUs).
* Grupos de segurança estruturados por função.
* Políticas de senha e bloqueio de conta aplicadas via GPO.
* Controle de permissões baseado em função (RBAC).

---

## 🛠️ 6. Hardware Principal

| Equipamento | Modelo | Qtd | Função |
| :--- | :--- | :---: | :--- |
| **Firewall** | FortiGate 60F | 1 | Segurança perimetral |
| **Switch Core** | Cisco 2960-X/3560-X | 1 | Roteamento entre VLANs |
| **Switch Acesso** | Cisco 2960-L | 5 | Conexão dos setores |
| **Servidor** | Dell PowerEdge T150 | 4 | Hospedagem do Windows Server 2022 |
| **Nobreak (UPS)** | APC Smart-UPS 3000VA | 1 | Proteção elétrica e continuidade |
| **Rack 19"** | Rittal / Furukawa | 1 | Organização dos equipamentos |
| **Cabeamento** | Cat6 Furukawa | - | Rede estruturada |

---

## 🛡️ 7. Segurança e Continuidade de Serviços
* **Firewall Perimetral:** FortiGate 60F gerenciando acessos externos e internos.
* **Isolamento:** Segmentação de rede rígida via VLANs.
* **Infraestrutura de Energia:** Nobreak APC de 3000VA protegendo o Switch Core, Firewall e Servidores, permitindo desligamento seguro e evitando corrupção de dados.
* **Estratégia de Backup 3-2-1:**
  * **3 cópias** dos dados.
  * **2 mídias** diferentes.
  * **1 cópia off-site** (fora do ambiente físico da UPA).
  * Rotina: Diário incremental e Semanal completo.

---

## ⚖️ 8. Conformidade LGPD
Este projeto adota rigorosamente os critérios de segurança e privacidade exigidos para dados de saúde. 
👉 Para visualizar o mapeamento completo de princípios, artigos e medidas técnicas, acesse o documento exclusivo: [LGPD.md](./LGPD.md).

---

## 📂 9. Estrutura do Repositório
```text
projeto-infraestrutura-upa/
├── docs/
│   ├── 01 Projeto_UPA.pdf
│   ├── 02 Planta UPA.pdf
│   ├── 03 Diagrama Rede.pdf
│   ├── 04 IP_Plan.pdf
│   └── 05 Documentacao_Tecnica.pdf
├── imagens/
│   ├── diagrama_rede.png
│   ├── planta_upa.png
│   └── visao_geral.png
├── configuracoes/
│   ├── vlan_config.txt
│   ├── gpo_politicas.txt
│   └── backup_politicas.txt
├── LGPD.md
├── README.md
└── LICENSE

🛠️ Tecnologias e Conceitos Aplicados
⁠Windows Server 2022⁠ ⁠Active Directory⁠ ⁠VLAN⁠ ⁠Firewall⁠ ⁠Backup 3-2-1⁠ ⁠UPS⁠ ⁠LGPD⁠ ⁠Cisco⁠ ⁠FortiGate⁠ ⁠Git

Conformidade com a LGPD – Lei Geral de Proteção de Dados
Lei 13.709/2018 | Aplicada ao Ambiente Hospitalar  
📑 Contexto
A UPA (Unidade de Pronto Atendimento) lida diariamente com dados sensíveis de saúde de pacientes. De acordo com o Art. 11 da LGPD, essas informações exigem atenção redobrada em sua coleta, armazenamento, acesso e descarte. Este documento descreve as medidas de conformidade integradas ao projeto de infraestrutura de TI.  
⚖️ Princípios da LGPD Aplicados na Infraestrutura
1 Finalidade (Art. 6°, I): Dados coletados e armazenados apenas para fins assistenciais e administrativos da UPA. Acesso estritamente restrito por função via RBAC no Active Directory.  
2 Adequação e Necessidade (Art. 6°, II e III): Segmentação de rede via VLANs garante que os setores de Consultórios, Enfermagem e Radiologia operem de forma isolada, acessando apenas recursos cruciais para suas atividades.  
3 Segurança (Art. 6°, VII): Proteção perimetral com Firewall FortiGate 60F, controle de acessos centralizado por grupos no Active Directory e GPOs corporativas para políticas de senhas complexas e bloqueios de contas.  
4 Prevenção (Art. 6°, VIII): Estratégia de backup 3-2-1 para mitigar perdas de dados, Nobreak (UPS) prevenindo corrupção de arquivos por quedas de energia e Controlador de Domínio secundário (DC02) para alta disponibilidade.  
5 Não Discriminação (Art. 6°, IX): Controle de acesso baseado exclusivamente no perfil técnico/operacional (RBAC) necessário para a função, nunca em identidade pessoal.  
6 Responsabilização (Art. 6°, X): Logs de acesso e auditoria completamente habilitados nos servidores Windows Server 2022, acompanhados desta documentação técnica.  
🛠️ Medidas Técnicas Implementadas
 Controle de acesso: Active Directory com RBAC e grupos por setor.  
 Segmentação de rede: VLANs por setor (Adm, Enfermagem, Consultórios, etc.).  
 Proteção de perímetro: Firewall FortiGate 60F.  
 Continuidade de dados: Backup 3-2-1 + Nobreak APC 3000VA.  
 Redundância: Dois Controladores de Domínio (DC01 e DC02).  
 Políticas de senha: GPO com complexidade e expiração de senha.  
 Auditoria: Logs de acesso nos servidores Windows Server 2022.  
🧬 Dados Sensíveis Identificados (Art. 11)
Os seguintes ativos de informação gerados na UPA entram na categoria de dados sensíveis à saúde:  
 Prontuários médicos e histórico de saúde de pacientes.  
 Resultados de exames (sistemas de Radiologia / Imagem).  
 Informações e registros de prescrição médica (Farmácia).  
 Dados de identificação civil associados aos registros de saúde.  
📈 Recomendações para Ambiente de Produção Real
Para elevar a infraestrutura simulada aos padrões de um hospital real, recomenda-se a futura implementação de:  
 DPO (Data Protection Officer): Nomeação formal de um encarregado pelo tratamento e proteção de dados.  
 Criptografia de Disco: Implementação do BitLocker nos discos rígidos de todos os servidores Dell PowerEdge.  
 Plano de Resposta a Incidentes: Criação de política formal para contenção e mitigação de incidentes de segurança.  
 Cultura Operacional: Realização de treinamentos periódicos com os colaboradores sobre as boas práticas da LGPD.  
 Ciclo de Vida do Dado: Elaboração de uma política formal de retenção e descarte seguro de dados médicos.  
📚 Base Legal de Referência
 Art. 5°: Definições de dados pessoais e dados sensíveis.  
 Art. 6°: Princípios orientadores da LGPD.  
 Art. 11: Regras para tratamento de dados sensíveis de saúde.  
 Art. 46: Medidas de segurança técnicas e administrativas exigidas.  
 Art. 48: Obrigatoriedade de comunicação de incidentes de segurança.
