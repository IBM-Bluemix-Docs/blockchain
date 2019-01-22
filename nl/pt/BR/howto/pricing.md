---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Precificação


***[Esta página é útil? Diga-nos.](https://www.surveygizmo.com/s3/4501493/IBM-Blockchain-Documentation)***


Este guia ajuda a entender a precificação para os planos de associação do {{site.data.keyword.blockchainfull}} Platform e quanto você pagará à medida em que desenvolver e aumentar a sua rede de blockchain.  
{:shortdesc}

O {{site.data.keyword.blockchainfull}} Platform cobra mensalmente a associação e taxas de peer para organizações que constroem redes de blockchain. As taxas são diferentes dependendo do plano de associação que você escolher e dos recursos de rede que a sua rede usar. A tabela a seguir mostra a visão geral de precificação do {{site.data.keyword.blockchainfull_notm}} Platform.

| Elementos de precificação | Custo por mês do Starter Plan | Custo por mês do Enterprise Plan |
|-----|-----|-----|
| Taxa de associação | US$ 250 | US$ 1.000 |
| Taxa de peer | US$ 125 | US$ 1.000 |

*Figura 1. Visão geral de precificação do {{site.data.keyword.blockchainfull}} Platform*

A taxa mensal é cobrada diariamente rateada. Por exemplo, um membro (taxa de participação associada de U$ 1.000) de dois peers (por taxa peer de U$ 1.000 × 2 peers) precisa pagar U$ 3.000 por mês. Se o mês tiver 30 dias, o membro pagará U$ 100 (U$ 3.000/30) todos os dias. Para obter mais informações sobre como pagar por suas redes, veja [Modo de pagamento](paying_mode.html).

O **{{site.data.keyword.blockchainfull_notm}} Platform Starter Plan oferece a você créditos de avaliação de US$ 500** antes de você ser cobrado. Para obter mais informações, veja [Precificação do Starter Plan](#starter-plan-pricing).


## Componentes básicos de rede

Para entender a precificação, precisamos iniciar com uma introdução aos componentes básicos de uma rede. O {{site.data.keyword.blockchainfull_notm}} Platform permite a criação de uma rede de blockchain que é baseada no Hyperledger Fabric. Em um alto nível, uma rede de blockchain do Fabric consiste nos componentes básicos a seguir:

-	**Organizações** - qualquer entidade que precisa manter uma cópia do livro-razão de blockchain e precisa validar transações. Pode haver múltiplas organizações de blockchain para uma única empresa.
-	**Peers** - O nó associado a uma organização que contém o livro-razão de blockchain e valida transações. Os peers são associados a uma organização de blockchain individual.
-	**Serviço de solicitação** - Composto por um único solicitador (SOLO) ou uma coleção de solicitadores. O serviço de ordenação sequencia transações, cria blocos e envia blocos para os peers para validação.
-	**Autoridade de certificação (CA)** – emite certificados digitais para propósitos de identificação para qualquer componente de rede interativa.

O {{site.data.keyword.blockchainfull_notm}} Platform oferece dois planos de associação, o **Starter Plan** e o **Enterprise Plan**, que é possível escolher no {{site.data.keyword.cloud_notm}}. Ambos os planos permitem criar organizações e fornecem uma autoridade de certificação. Os planos divergem em torno dos peers, das autoridades de certificação e do serviço de pedido.

O Enterprise Plan fornece a você autoridades de certificação e peers altamente disponíveis com um serviço de pedido tolerante a falhas e travamento. O Starter Plan não tem opções de alta disponibilidade e utiliza um serviço de pedido básico, SOLO. Por essa razão, o Starter Plan é projetado para ser o ponto de entrada do {{site.data.keyword.blockchainfull_notm}} Platform para desenvolvimento, teste e ambientes de prova de conceito. O Enterprise Plan é a opção para redes que estão prontas para ambientes pilotos e de produção.

## Elementos chaves de precificação

O Starter Plan e o Enterprise Plan têm dois elementos de precificação:

- **Taxa de associação** – cobre a criação da organização, o acesso ao serviço de pedido e autoridade de certificação e é cobrada em uma base **por instância**. Incluído nesse elemento de precificação, o {{site.data.keyword.blockchainfull_notm}} Platform manipula o serviço de pedido e a autoridade de certificação em nome de sua rede. Essa taxa é necessária para ter acesso a uma rede construída no {{site.data.keyword.blockchainfull_notm}} Platform.

  -	O Starter Plan permite organizações *ilimitadas* por associação e a capacidade de alternar entre organizações no Monitor de rede. Como o Starter Plan é projetado para desenvolvimento, teste e ambientes do POC, é possível simular nos ambientes de múltiplas organizações. **Observe** que o armazenamento de rede total é limitado a 20 GB, incluindo os componentes, o chaincode e os dados de livro-razão. As suas organizações simuladas compartilham o armazenamento de 20 GB na rede de blockchain.

  -	O Enterprise permite uma única organização por associação. Como o Enterprise foi projetado para ambientes pilotos e de produção, você é vinculado à sua organização específica.

-	**Taxa de peer** – abrange os peers de uma organização e é cobrada em uma base **por peer**. Essa taxa será necessária apenas se você quiser ter um peer para manter uma cópia do livro-razão e validar transações.

### Exemplo de taxa de associação

A Figura 2 mostra um exemplo de instâncias de rede, que pode ajudar a entender a taxa de associação. Na figura, a conta do {{site.data.keyword.cloud_notm}} específica provisiona três instâncias de rede: uma instância do Enterprise Plan com o nome de *Blockchain-11* e duas instâncias do Starter Plan com o nome de *Blockchain-cz* e *Blockchain-da*. Cada instância requer o seu próprio serviço de pedido e de autoridade de certificação. Nesse caso, essa conta do {{site.data.keyword.cloud_notm}} específica precisa pagar três taxas de associação, uma para cada instância de rede.

![Instâncias de rede de Blockchain](../images/ibp_instance_example.png "Instâncias de rede de Blockchain")  
*Figura 2. Instâncias de rede de Blockchain*


## Precificação do Starter Plan

As redes do Starter Plan são provisionadas com uma configuração padrão de duas organizações e um peer por organização, para um total de US$ 500 por mês. Com a configuração padrão, não há necessidade imediata de manipular o ambiente para começar. Você pode incluir mais organizações sem encargos e pode incluir mais peers em suas organizações em um encargo de US$ 125 por mês por peer. A sua conta será refletida na Figura 3 se você criar ou se associar a uma rede do Starter Plan com a configuração padrão.

| Componentes de precificação | Custo por mês |
|-----|----------------|
| Taxa de associação | US$ 250 |
| Taxa de peer | US$ 125 |
| Taxa de peer | US$ 125 |
| Fim do encargo do mês | US$ 500 |

*Figura 3. Encargo de uma rede padrão do Starter Plan*

### Precificação do Starter Plan de exemplo

#### Avaliação do Starter Plan
O propósito do Starter Plan é permitir que qualquer pessoa inicie e veja o valor agregado do {{site.data.keyword.blockchainfull_notm}} Platform. Portanto, o {{site.data.keyword.blockchainfull_notm}} Platform oferece US$ 500 em créditos de nuvem destinados a cobrir todos os encargos de novos usuários que seriam acumulados durante um mês com a configuração de rede padrão descrita acima. A sua conta será refletida na Figura 4 se você criar ou se associar a uma rede do Starter Plan pela **primeira vez** com a configuração padrão.

| Componentes de precificação | Custo por mês |
| ----- | ---------------- |
| Rede de taxa de associação 1 | US$ 250 |
| Taxa de peer | US$ 125 |
| Taxa de peer | US$ 125 |
| Total | US$ 500 |
| Créditos | -US$ 500 |
| Fim do primeiro encargo do mês | US$ 0 |

*Figura 4. Encargo de uma rede padrão do Starter Plan com créditos de nuvem*

**Novos usuários precisam inscrever-se para obter créditos de nuvem.** Eles não são aplicados automaticamente. [Inscreva-se ![Ícone de link externo](../images/external_link.svg "Ícone de link externo")](https://www.ibm.com/account/reg/us-en/signup?formid=urx-32798 "Inscreva-se") para solicitar os créditos se ainda não tiver feito isso. Aguarde 24 horas para se certificar de que os créditos estão em sua [conta ![Ícone de link externo](../images/external_link.svg "Ícone de link externo")](https://console.bluemix.net/docs/billing-usage/viewing_usage.html#credits "conta") antes de acessar o Starter Plan. Caso contrário, você poderá ser cobrado antes que os créditos se apliquem.

A oferta fornece créditos vitalício. Os créditos duram desde que você mantenha sua conta do {{site.data.keyword.cloud_notm}}, portanto, não é necessário usá-los no primeiro mês. Os créditos aplicam-se a todos os serviços do {{site.data.keyword.cloud_notm}}. Eles podem ser consumidos por produtos diferentes do {{site.data.keyword.blockchainfull}} Platform usados no {{site.data.keyword.cloud_notm}}.

| Componentes de precificação | Custo por mês |
| ----- | ---------------- |
| Rede de taxa de associação 1 | US$ 250 |
| Taxa de peer | US$ 125 |
| Total | US$ 375 |
| Serviços  {{site.data.keyword.cloud_notm}}  Adicionais | $75 |
| Fim do primeiro encargo do mês | US$ 0 |
| Créditos utilizados | -$450. |
| Créditos remanescentes após o primeiro mês | $50 |

*Figura 5. Usando créditos de avaliação com outros Serviços {{site.data.keyword.cloud_notm}}*

#### Peers adicionais
O Starter Plan não restringe o número de peers que é possível incluir em sua rede. Se você incluir, por exemplo, dois peers na rede padrão do Starter Plan, um para cada uma das suas organizações, aumentará a sua conta em US$ 250 por mês. A sua conta será refletida na Figura 6 se você incluir dois peers adicionais no início do primeiro mês ao criar ou se associar a uma rede do Starter Plan e consumir os créditos de avaliação.

| Componentes de precificação | Custo por mês |
|-----|----------------|
| Rede de taxa de associação 1 | US$ 250 |
| Taxa de peer | US$ 125 |
| Taxa de peer | US$ 125 |
| Taxa de peer | US$ 125 |
| Taxa de peer | US$ 125 |
| Total | US$ 750 |
| Créditos | -US$ 500 |
| Fim do primeiro encargo do mês | US$ 250 |

*Figura 6. Encargo de uma rede padrão do Starter Plan com dois peers adicionais*

#### Redes adicionais
O Starter Plan também não restringe o número de instâncias de rede que é possível provisionar. Se você provisionar uma segunda instância de rede do Starter Plan, será necessário pagar uma segunda taxa de associação e um segundo conjunto de taxas de peer associados à segunda rede. Portanto, você aumenta a sua conta em US$ 500 por mês para usar a configuração de rede padrão. Talvez você se encontre no cenário em que requeira redes Starter adicionais para seus ambientes de desenvolvimento, teste e prova de conceito isolados uns dos outros. Um exemplo seria quando você desejar fornecer a seus engenheiros de qualidade para executarem testes funcionais significativos longe de seu ambiente de desenvolvimento.

A sua conta será refletida na Figura 6 se você incluir uma rede adicional no início do primeiro mês ao criar ou se associar a uma rede do Starter Plan e consumir os créditos de avaliação.

| Componentes de precificação | Custo por mês |
|-----|----------------|
| Rede de taxa de associação 1 | US$ 250 |
| Taxa de peer | US$ 125 |
| Taxa de peer | US$ 125 |
| Rede de taxa de associação 2 | US$ 250 |
| Taxa de peer | US$ 125 |
| Taxa de peer | US$ 125 |
| Total | US$ 1.000 |
| Créditos | -US$ 500 |
| Fim do primeiro encargo do mês | US$ 500 |

*Figura 7. Encargo de duas redes padrão do Starter Plan*

#### Removendo peers
Também é possível remover um peer da configuração de rede padrão do Starter Plan. Nessa situação, o {{site.data.keyword.blockchainfull_notm}} Platform ainda oferece a você créditos de avaliação de Nuvem de US$ 500, mas a sua conta será reduzida em US$ 125 por mês. O resultado são créditos de peer de US$ 125 restantes no final do mês. Você poderá se encontrar nesse cenário quando estiver colaborando com outro membro em seu ambiente do Starter Plan, em que cada um de vocês precisa apenas de um único peer. A sua conta será refletida na Figura 8 se você remover um peer de sua rede do Starter Plan e consumir os créditos de avaliação.

| Componentes de precificação | Custo por mês |
| ----- | ---------------- |
| Rede de taxa de associação 1 | US$ 250 |
| Taxa de peer | US$ 125 |
| Taxa de peer | N/A |
| Total | US$ 375 |
| Créditos | -US$ 500 |
| Fim do primeiro encargo do mês | US$ 0 |
| Créditos de associação restantes | US$ 0 |
| Créditos de peer restantes | US$ 125 |

*Figura 8. Encargo de uma rede padrão do Starter Plan com créditos ampliados*


## Precificação do Enterprise Plan

O {{site.data.keyword.blockchainfull_notm}} Platform não fornece configuração padrão para uma rede do Enterprise Plan. É possível escolher a configuração com a qual você gostaria de começar. Quando você estiver pronto para usar o Enterprise Plan, deverá ter um bom entendimento do que a sua configuração de rede deve ser. Como uma melhor prática de alta disponibilidade, é altamente recomendável um mínimo de dois peers por organização para assegurar que a sua organização não tenha uma indisponibilidade da rede.

Se você estiver em uma rede do Enterprise Plan com o outro membro de rede e cada um de vocês incluir dois peers para a sua organização, cada uma de suas contas será refletida na Figura 8.

| Componentes de precificação | Custo por mês |
|-----|----------------|
| Taxa de associação | US$ 1.000 |
| Taxa de peer | US$ 1.000 |
| Taxa de peer | US$ 1.000 |
| Fim do encargo do mês | US$ 3.000 |

*Figura 9. Encargo de uma rede básica do Enterprise Plan*

### Precificação do Enterprise Plan de exemplo

#### Peers adicionais
{: #additional-peers}

Continue com o exemplo acima, se você incluir outros dois peers em sua organização. A sua conta aumenta em US$ 2.000 por mês. Sua conta está refletida na Figura 10:

| Componentes de precificação | Custo por mês |
|-----|----------------|
| Taxa de associação | US$ 1.000 |
| Taxa de peer | US$ 1.000 |
| Taxa de peer | US$ 1.000 |
| Taxa de peer | US$ 1.000 |
| Taxa de peer | US$ 1.000 |
| Fim do primeiro encargo do mês | US$ 5.000 |

*Figura 10. Encargo de uma rede do Enterprise Plan com quatro peers*

Se o outro membro mantiver a mesma configuração de rede, a conta do membro será a mesma que antes, que será refletida na Figura 8.

#### Redes adicionais
{: #additional-networks}

O Enterprise Plan também não restringe o número de instâncias de rede que é possível provisionar ou se associar. Se você criar uma segunda rede do Enterprise Plan com a mesma configuração básica de rede, ou seja, uma única organização com dois peers, sua conta será refletida na Figura 11. Você poderá se encontrar nesse cenário quando tiver se associado a múltiplas redes, criado múltiplas redes ou uma combinação dos dois.

| Componentes de precificação | Custo por mês |
|-----|----------------|
| Rede de taxa de associação 1 | US$ 1.000 |
| Taxa de peer | US$ 1.000 |
| Taxa de peer | US$ 1.000|
| Rede de taxa de associação 2 | US$ 1.000 |
| Taxa de peer | US$ 1.000 |
| Taxa de peer | US$ 1.000|
| Total | US$ 6.000 |

*Figura 11. Encargo de duas redes do Enterprise Plan com a configuração básica de rede*

Se o outro membro usar apenas uma rede do Enterprise Plan e mantiver a mesma configuração de rede, a conta do membro parecerá igual à anterior, o que é refletido na Figura 9.
