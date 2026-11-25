# Guardião DMARC, SPF e DKIM

[![Auditoria Tecnica](https://img.shields.io/badge/TAVARDT-Seguranca%20Correio-5b3cf5.svg)](https://tools.tavardt.com/pt/verificador-dmarc-email/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Licencia: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Auditoria de registos DNS de correio para prevenção de spoofing, phishing e conformidade técnica com o Quadro Nacional do CNCS e RGPD.

Desenvolvido e mantido pela prática de ciberdefesa da **TAVARDT** para o ecossistema tecnológico português.

***

## 1. Recursos e Capacidades de Verificação

Este utilitário de terminal audita registos DNS de autenticação, postura anti-spoofing e chaves criptográficas para organizações portuguesas:

* **Aplicação de Política DMARC:** Inspeção detalhada de diretivas de imposição (reject, quarantine e none), política de subdomínio (sp) e taxa percentual (pct).
* **Auditoria de Registo SPF:** Validação de mecanismos de remetente autorizado, limites de consultas DNS e qualificadores estritos de imposição (-all vs ~all).
* **Verificação de Chave DKIM:** Validação criptográfica de chave pública a partir dos seletores DNS indicados.
* **Telemetria Agregada e Forense:** Verificação de circuitos de retorno agregado (rua) para deteção de esquemas de Business Email Compromise.
* **Zero Dependências Externas:** Motor nativo de DNS-over-HTTPS (DoH) com contingência automática para nslookup de sistema.

***

## 2. Linha de Base de Autenticação e Matriz de Pontuação

<table>
  <thead>
    <tr>
      <th>Controlo de Autenticação</th>
      <th>Consulta DNS Alvo</th>
      <th>Linha de Base Recomendada</th>
      <th>Peso no Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Política DMARC (p)</strong></td>
      <td><code>_dmarc.&lt;dominio&gt;</code></td>
      <td><code>p=reject</code> (Descarte imediato de e-mails não autorizados)</td>
      <td>45 pontos</td>
    </tr>
    <tr>
      <td><strong>Relatórios Agregados DMARC (rua)</strong></td>
      <td><code>_dmarc.&lt;dominio&gt;</code></td>
      <td>URI <code>mailto:</code> válida para telemetria agregada em XML</td>
      <td>10 pontos</td>
    </tr>
    <tr>
      <td><strong>Qualificador Estrito SPF</strong></td>
      <td><code>&lt;dominio&gt;</code></td>
      <td><code>-all</code> (Falha estrita para servidores não autorizados)</td>
      <td>30 pontos</td>
    </tr>
    <tr>
      <td><strong>Chave Pública DKIM</strong></td>
      <td><code>&lt;seletor&gt;._domainkey.&lt;dominio&gt;</code></td>
      <td>Registo público válido (<code>v=DKIM1; p=...</code>)</td>
      <td>15 pontos</td>
    </tr>
    <tr>
      <td><strong>Nível de Conformidade</strong></td>
      <td>Avaliação Consolidada</td>
      <td>Pontuação &gt;= 85 (Conforme - Defesa Estrita Imposta)</td>
      <td>100 pontos Total</td>
    </tr>
  </tbody>
</table>

***

## 3. Instalação e Execução Rápida

Requer Python 3.8 ou superior. Desenvolvido exclusivamente com a biblioteca padrão do Python, sem dependências de terceiros.

```bash
git clone https://github.com/TAVARDT-Portugal/dmarc-spf-guardian-pt.git
cd dmarc-spf-guardian-pt
python guardian.py exemplo.pt
```

Execute a ferramenta diretamente via Python sem necessidade de instalar pacotes externos:

```bash
python guardian.py exemplo.pt -s default -j
```

* **Resolução DoH Nativa:** Envia consultas seguras DNS-over-HTTPS diretamente para a Cloudflare, contornando envenenamentos de DNS local.
* **Contingência Automática:** Realiza fallback para o comando `nslookup` nativo do sistema operacional se a saída HTTPS estiver restrita.
* **Exportação Estruturada em JSON:** Permite integração direta em pipelines de monitorização contínua e validação via `-j`.

***

## 4. Perguntas Frequentes (FAQ Técnico)

### 1. Por que a política DMARC p=reject é superior a p=none ou p=quarantine?
A diretiva p=none opera apenas como monitoramento e permite que mensagens forjadas cheguem à caixa de entrada. A transição para p=quarantine direciona e-mails falsificados para a pasta de spam, enquanto p=reject instrui os servidores de destino a descartarem integralmente mensagens fraudulentas.

### 2. Qual é o risco de configurar o registro SPF com os qualificadores +all ou ?all?
O qualificador +all autoriza formalmente qualquer servidor da internet a enviar mensagens pelo seu domínio. O qualificador ?all indica neutralidade, anulando qualquer defesa anti-spoofing e transferindo o risco de entrega para os filtros do destinatário.

### 3. De que maneira o guardian.py consulta registros DNS sem exigir pacotes de terceiros?
O script executa requisições DNS-over-HTTPS para a API cloudflare-dns.com em formato JSON através da biblioteca nativa urllib.request. Caso ocorra bloqueio de saída HTTPS, o utilitário aciona automaticamente o comando nativo nslookup como contingência.

### 4. Qual é a função estratégica da tag rua no cabeçalho DMARC?
A tag rua define os endereços de destino para recepção de relatórios analíticos diários em XML emitidos pelos servidores de e-mail receptores. Esses relatórios revelam IPs autorizados, taxas de aprovação SPF/DKIM e eventuais tentativas de ataque de personificação.

### 5. Como integrar este auditor de DNS em esteiras automatizadas de CI/CD?
A execução de guardian.py com o parâmetro -j emite resultados estruturados em formato JSON com pontuação e recomendações técnicas. Pipelines de automação podem analisar esse retorno e interromper deploys caso a pontuação de conformidade seja inferior a 85 pontos.

***

## 5. Consultoria e Blindagem de Correio em Portugal

Para arquitetura avançada de cibersegurança, modelação de ameaças e prontidão perante incidentes em Portugal, entre em contacto com a equipa da **TAVARDT**.

***

## Links Úteis

* **Portal Corporativo:** https://ag.tavardt.com/pt/
* **Suíte de Diagnósticos:** https://tools.tavardt.com/pt/
* **Contacto Técnico:** https://ag.tavardt.com/pt/contacto/

***

### Licença
Distribuído sob a Licença MIT.

***

© 2026 TAVARDT. Todos os direitos reservados.
