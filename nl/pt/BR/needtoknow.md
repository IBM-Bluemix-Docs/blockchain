---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-18"

keywords: IBM Blockchain offerings, Linux Foundation, Hyperledger Fabric, open source, community contribution

subcollection: blockchain

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:note: .note}
{:important: .important}
{:tip: .tip}
{:external: target="_blank" .external}

# Renúncia de Responsabilidade
{: #disclaimer}

**ATENÇÃO:** deve-se revisar as informações a seguir antes de usar qualquer plano do {{site.data.keyword.blockchainfull}}.

## Instrução de suporte da {{site.data.keyword.IBM_notm}}
{: #disclaimer-support-statement}

O longo histórico de liderança da {{site.data.keyword.IBM_notm}} em inovação continua com as ofertas do {{site.data.keyword.blockchainfull_notm}} Platform no {{site.data.keyword.cloud_notm}}. Blockchain é uma tecnologia de progressão rápida que é projetada para revolucionar a indústria financeira, as cadeias de suprimento local e global e o suporte logístico em qualquer número de espaços de negócios. Por meio de vários programas de adoção antecipada, os clientes e parceiros de negócios {{site.data.keyword.IBM_notm}} têm conduzido ativamente o blockchain como uma solução industrial. O {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} é um desses programas. **Como com qualquer nova tecnologia, os usuários do {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} devem estar cientes do potencial para uma mudança rápida e fundamental**.
{:shortdesc}

A arquitetura por trás do {{site.data.keyword.blockchainfull_notm}} é o projeto Hyperledger Fabric da Linux Foundation. Cada contribuição da comunidade de software livre melhora o Hyperledger Fabric, mas pode apresentar desafios de adoção. A ** {{site.data.keyword.IBM_notm}} adverte com relação à definição ou troca de ativos financeiros<!--, or any assets of value,--> diretamente em qualquer rede de blockchain do Hyperledger Fabric**.

A {{site.data.keyword.IBM_notm}} não fornece suporte para redes que usam o Hyperledger Composer na produção, incluindo a CLI do Composer, as APIs de JavaScript, o servidor REST e o Web Playground.
{:note}

## Instrução de software livre
{: #disclaimer-open-source-statement}

Os planos de oferta do {{site.data.keyword.blockchainfull_notm}} no {{site.data.keyword.cloud_notm}} são construídos com base na pilha de Hyperledger Fabric do Linux Foundation. Os membros do Projeto Hyperledger, incluindo a {{site.data.keyword.IBM_notm}}, continuam a contribuir com vários subprojetos sob a cobertura do Hyperledger.  Todas as contribuições são revisadas, avaliadas e testadas pela comunidade.

## Instrução de suporte de chaincode
{: #disclaimer-chaincode-support-statement}

As práticas de codificação a seguir NÃO são suportadas em redes do {{site.data.keyword.blockchainfull_notm}}:

1. Usando matrizes associativas com iteração (a ordem é aleatória em Go).
2. Lendo uma lista de itens a partir de uma tabela de KVS (a ordem não é garantida).
3. Gravando chaincode inseguro para encadeamento (consulta e chamada podem ser chamadas em paralelo).
4. Substituir memória ou armazenamento em cache global para variáveis de estado do livro-razão no chaincode.
5. Acessando serviços externos, como bancos de dados, diretamente a partir de chaincode.
6. Usando bibliotecas ou variáveis globais que podem introduzir o não determinismo (como usar "aleatório" ou "tempo").

Além disso, não é recomendado gravar chaincode não determinístico, o que apresenta risco à consistência e à integridade dos dados. Observe que a arquitetura do Hyperledger Fabric foi projetada para combater o chaincode não determinístico por meio de uma série de verificações de endosso e validação. No entanto, ainda é altamente recomendável que você codifique funções determinísticas que não são dependentes de variáveis globais não estáticas, por exemplo, tempo.
