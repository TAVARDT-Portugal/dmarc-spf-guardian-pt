# Guardião DMARC, SPF e DKIM

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Auditoria Tecnica](https://img.shields.io/badge/TAVARDT-Seguranca%20Correio-5b3cf5.svg)](https://tools.tavardt.com/pt/verificador-dmarc-email/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)

Auditoria de registos DNS de correio para prevenção de spoofing, phishing e conformidade técnica com o Quadro Nacional do CNCS e RGPD.

Desenvolvido e mantido pela divisao de seguranca de infraestruturas da **TAVARDT Portugal**.

***

## Recursos e Verificacoes

* **Validacao de Politica DMARC**: Inspeção das diretivas de protecao (reject, quarantine e none), alinhamento de subdominios (sp) e taxa percentual de aplicacao (pct).
* **Auditoria de Registos SPF**: Verificacao de mecanismos autorizados, limites de consultas DNS e qualificadores estritos (-all vs ~all).
* **Verificacao de Assinatura DKIM**: Validacao de chaves publicas em seletores DNS especificos.
* **Mecanismos de Relatorios**: Verificacao de parametros de reporte agregado e forense (rua e ruf).
* **Alinhamento Normativo**: Estruturado em conformidade com o Quadro Nacional de Cibersegurança do CNCS e Regulamento Geral sobre a Proteção de Dados (RGPD / CNPD).

***

## Instalação e Execucao

Requer apenas Python 3.8 ou superior, utilizando exclusivamente a biblioteca padrao sem dependencias externas.

```bash
git clone https://github.com/TAVARDT-Portugal/dmarc-spf-guardian-pt.git
cd dmarc-spf-guardian-pt
python guardian.py empresa.pt
```

Para inspecionar um seletor DKIM customizado ou gerar dados estruturados em JSON:

```bash
python guardian.py empresa.pt -selector mail -json
```

***

## Diagnostico Completo na Web

Para auditorias continuas e diagnosticos avancados, consulte a ferramenta oficial:

* **Verificador DMARC e Autenticacao de Correio**
* **[Portal Corporativo TAVARDT](https://ag.tavardt.com/pt/)**

***

## Suporte e Consultoria Especializada

Para projetos corporativos de ciberseguranca e governanca tecnica em Portugal, contacte a equipa da **TAVARDT Portugal**.

***

## Links Úteis

* **Portal Corporativo:** https://ag.tavardt.com/pt/
* **Suíte de Diagnósticos:** https://tools.tavardt.com/pt/
* **Contacto Técnico:** https://ag.tavardt.com/pt/contacto/

***

### Licença
Distribuído sob a Licença MIT. Consulte o ficheiro [LICENSE](LICENSE) para obter detalhes completos.

***

© 2026 TAVARDT Portugal. Todos os direitos reservados. Soberania e Defesa de Infraestrutura.
