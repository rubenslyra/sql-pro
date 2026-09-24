# 🏢 1. Domínio Corporativo / Geral (Core)

| Termo em inglês | Tradução | Uso típico |
|---|---|---|
| `Company` | Empresa (matriz) | Tabela raiz multi-tenant |
| `Branch` / `BranchOffice` | Filial / unidade | Filiais da empresa |
| `Department` | Departamento | RH/estrutura organizacional |
| `Division` | Divisão | Grande unidade de negócio |
| `BusinessUnit` | Unidade de negócio | BUs em corporações |
| `CostCenter` | Centro de custo | Contabilidade/controladoria |
| `ProfitCenter` | Centro de resultado | Controladoria |
| `Address` | Endereço | Tabela auxiliar (1:N) |
| `Contact` | Contato | Dados de contato genéricos |
| `Document` | Documento | CPF/CNPJ/passaporte |
| `Note` / `Comment` | Observação | Tabela de anotações |
| `Attachment` / `File` | Anexo / arquivo | Uploads |
| `AuditLog` / `AuditTrail` | Log de auditoria | Quem alterou o quê |
| `Setting` / `Config` | Configuração | Parâmetros do sistema |
| `Currency` | Moeda | BRL, USD, EUR |
| `ExchangeRate` | Taxa de câmbio | Conversão monetária |
| `Country` / `State` / `City` | País / Estado / Cidade | Tabelas de domínio |
| `Region` / `Territory` | Região / território | Vendas/representação |

---

## 👥 2. RH / Pessoas (Human Resources)

| Termo | Tradução | Uso |
|---|---|---|
| `Employee` | Funcionário/colaborador | Tabela principal de RH |
| `EmployeeHistory` | Histórico funcional | Promoções/mudanças de cargo |
| `Position` / `JobTitle` | Cargo / função | Catálogo de cargos |
| `JobLevel` / `Grade` | Nível / grau | Júnior, pleno, sênior |
| `Manager` / `Supervisor` | Gestor / supervisor | Auto-relacionamento em Employee |
| `Subordinate` / `Report` | Subordinado / liderado | Relação hierárquica |
| `Payroll` | Folha de pagamento | Cabeçalho da folha |
| `PayrollItem` | Item da folha | Verbas (salário, hora extra) |
| `Salary` / `Compensation` | Salário / remuneração | Histórico salarial |
| `Benefit` | Benefício | VR, VT, plano de saúde |
| `Dependent` | Dependente | Para IR/benefícios |
| `Attendance` | Frequência / ponto | Batidas de ponto |
| `Timesheet` | Apontamento de horas | Horas trabalhadas |
| `Leave` / `TimeOff` | Afastamento / licença | Férias, licenças |
| `LeaveRequest` | Solicitação de afastamento | Workflow de aprovação |
| `Vacation` | Férias | Período aquisitivo/gozo |
| `Overtime` | Hora extra | Cálculo de horas |
| `Shift` | Turno | Escala de trabalho |
| `Schedule` / `Roster` | Escala / horário | Escalas de equipe |
| `Recruitment` / `Hiring` | Recrutamento / admissão | Processo seletivo |
| `Candidate` / `Applicant` | Candidato | Vagas de emprego |
| `JobOpening` / `Vacancy` | Vaga de emprego | Oportunidades abertas |
| `Interview` | Entrevista | Etapa seletiva |
| `Resume` / `CV` | Currículo | Documento do candidato |
| `Termination` / `Resignation` | Demissão / desligamento | Desligamentos |
| `Training` / `Course` | Treinamento / curso | Desenvolvimento |
| `Certificate` | Certificado | Certificações |
| `Skill` | Competência / habilidade | Matriz de skills |
| `PerformanceReview` / `Appraisal` | Avaliação de desempenho | PDR/performance |
| `DisciplinaryAction` | Medida disciplinar | Advertências |
| `Union` / `LaborUnion` | Sindicato | Convenção coletiva |
| `Contract` | Contrato de trabalho | CTPS / PJ |

---

## 🤝 3. CRM / Relacionamento com Cliente

| Termo | Tradução | Uso |
|---|---|---|
| `Customer` | Cliente | Tabela principal (B2C/B2B) |
| `Consumer` | Consumidor | Pessoa física final |
| `Client` | Cliente (B2B/serviços) | Sinônimo de Customer |
| `Prospect` | Prospect | Potencial cliente |
| `Lead` | Lead | Contato qualificado |
| `Contact` | Contato | Pessoa dentro da empresa |
| `Account` | Conta (B2B) | Empresa cliente |
| `Opportunity` | Oportunidade | Negócio em aberto |
| `Deal` | Negócio | Sinônimo de Opportunity |
| `Pipeline` | Funil de vendas | Estágios do funil |
| `Stage` / `PipelineStage` | Etapa do funil | Prospecção → fechamento |
| `Campaign` | Campanha | Marketing |
| `LeadSource` | Origem do lead | Origem (Google, indicação) |
| `Industry` / `Sector` | Segmento / ramo | Setor de atuação |
| `CustomerSegment` | Segmento de cliente | Classificação |
| `CustomerTier` / `CustomerLevel` | Nível do cliente | Ouro, prata, bronze |
| `Loyalty` / `LoyaltyProgram` | Fidelidade / programa de pontos | Pontos e recompensas |
| `Points` / `PointsBalance` | Pontos / saldo de pontos | Fidelidade |
| `Reward` / `Redemption` | Recompensa / resgate | Troca de pontos |
| `Referral` | Indicação | Indicação de cliente |
| `Ticket` / `SupportTicket` | Chamado de suporte | Atendimento |
| `Case` | Caso (atendimento) | Sinônimo de Ticket (Salesforce) |
| `Interaction` / `Touchpoint` | Interação / ponto de contato | Histórico de contato |
| `CommunicationLog` | Registro de comunicação | E-mails, ligações |
| `CallLog` | Registro de ligações | Telefonia |
| `EmailLog` | Registro de e-mails | Disparos |
| `SLA` (Service Level Agreement) | Acordo de nível de serviço | Prazos de atendimento |
| `Survey` / `Feedback` | Pesquisa / feedback | NPS, CSAT |
| `NPS` (Net Promoter Score) | NPS | Satisfação |
| `Churn` | Evasão / cancelamento | Perda de cliente |
| `CustomerLifetimeValue` (CLV/LTV) | Valor de vida do cliente | Métrica |

---

## 🛒 4. Vendas / Comercial (Sales)

| Termo | Tradução | Uso |
|---|---|---|
| `SalesOrder` / `Order` | Pedido de venda | Cabeçalho do pedido |
| `OrderItem` / `OrderLine` | Item do pedido | Itens (1:N) |
| `Quote` / `Quotation` | Cotação / orçamento | Proposta comercial |
| `Proposal` | Proposta | Sinônimo de Quote |
| `Invoice` | Nota fiscal / fatura | Faturamento |
| `InvoiceItem` | Item da nota/fatura | Itens faturados |
| `Billing` | Faturamento | Processo/registro |
| `Receipt` | Recibo | Comprovante |
| `Return` / `SalesReturn` | Devolução de venda | Devoluções |
| `Refund` | Reembolso | Devolução de dinheiro |
| `Exchange` | Troca | Troca de mercadoria |
| `Discount` | Desconto | Por valor/percentual |
| `Coupon` / `Voucher` | Cupom / vale | Promoções |
| `Promotion` / `Promo` | Promoção | Regras promocionais |
| `Bundle` / `Kit` | Combo / kit | Produtos agrupados |
| `GiftCard` | Vale-presente | Cartão presente |
| `Wishlist` | Lista de desejos | E-commerce |
| `Cart` / `ShoppingCart` | Carrinho de compras | Sessão de compra |
| `CartItem` | Item do carrinho | Itens temporários |
| `Checkout` | Finalização de compra | Etapa de pagamento |
| `Salesperson` / `SalesRep` | Vendedor / representante | Responsável pela venda |
| `SalesTeam` | Equipe de vendas | Grupo de vendedores |
| `Commission` | Comissão | Cálculo de comissão |
| `Target` / `Quota` | Meta / cota | Metas de vendas |
| `PriceList` | Tabela de preços | Preços por segmento |
| `Price` / `UnitPrice` | Preço / preço unitário | Coluna em itens |
| `Tax` / `TaxAmount` | Imposto / valor do imposto | Coluna fiscal |
| `Subtotal` | Subtotal | Soma dos itens |
| `Total` / `GrandTotal` | Total / total geral | Valor final |
| `ShippingCost` / `Freight` | Frete | Custo de envio |
| `PaymentTerm` | Condição de pagamento | Prazo (à vista, 30/60/90) |
| `Installment` / `Parcel` | Parcela | Parcelas |
| `CreditLimit` | Limite de crédito | Limite do cliente B2B |
| `CreditCheck` | Análise de crédito | Consulta SPC/Serasa |
| `Backorder` | Pedido pendente (sem estoque) | Entrega futura |
| `Cancellation` | Cancelamento | Pedidos cancelados |

---

## 📦 5. Estoque / Produtos (Inventory & Catalog)

| Termo | Tradução | Uso |
|---|---|---|
| `Product` | Produto | Cadastro principal |
| `Service` | Serviço | Item intangível |
| `SKU` (Stock Keeping Unit) | Código do produto / SKU | Identificador único |
| `UPC` / `EAN` / `Barcode` | Código de barras | GTIN/EAN-13 |
| `Category` | Categoria | Classificação |
| `Subcategory` | Subcategoria | Nível abaixo |
| `Brand` / `Manufacturer` | Marca / fabricante | Fabricante |
| `Model` | Modelo | Versão do produto |
| `Variant` | Variação | Cor, tamanho (e-commerce) |
| `Attribute` / `Specification` | Atributo / especificação | Características técnicas |
| `UnitOfMeasure` (UOM) | Unidade de medida | UN, KG, MT, LT |
| `Weight` / `Dimension` | Peso / dimensões | Cubagem/frete |
| `Warehouse` | Depósito / almoxarifado | Local de estoque |
| `Location` / `Bin` / `Shelf` | Posição / endereço / gaveta | Endereçamento (rua, módulo, nível) |
| `Stock` / `Inventory` | Estoque | Saldo atual |
| `StockLevel` | Nível de estoque | Quantidade |
| `InventoryMovement` / `StockMovement` | Movimentação de estoque | Entradas/saídas |
| `StockAdjustment` | Ajuste de estoque | Inventário |
| `StockCount` / `InventoryCount` | Contagem de estoque | Inventário físico |
| `ReorderPoint` | Ponto de reposição | Estoque mínimo |
| `SafetyStock` | Estoque de segurança | Buffer |
| `MinimumStock` / `MaximumStock` | Estoque mínimo / máximo | Parâmetros |
| `Lot` / `Batch` | Lote | Controle de lote |
| `SerialNumber` | Número de série | Rastreabilidade unitária |
| `ExpirationDate` / `ExpiryDate` | Data de validade | Produtos perecíveis |
| `ManufacturingDate` | Data de fabricação | Lote |
| `GoodsReceipt` | Entrada de mercadoria | Recebimento de compra |
| `GoodsIssue` | Saída de mercadoria | Baixa de estoque |
| `Transfer` / `StockTransfer` | Transferência de estoque | Entre depósitos |
| `Reservation` | Reserva de estoque | Pedido reservado |
| `Allocation` | Alocação | Separação de estoque |
| `Picking` | Separação (de pedido) | Etapa do armazém |
| `Packing` | Embalagem | Etapa do armazém |
| `Putaway` | Endereçamento/guarda | Guarda no estoque |
| `CycleCount` | Contagem cíclica | Inventário rotativo |
| `Shrinkage` | Quebra / perda | Perda de estoque |
| `DamagedGoods` | Mercadoria avariada | Itens danificados |
| `Assembly` / `KitAssembly` | Montagem / kit | Produto composto |
| `BillOfMaterials` (BOM) | Lista de materiais | Estrutura do produto |

---

## 🚚 6. Compras / Suprimentos (Procurement)

| Termo | Tradução | Uso |
|---|---|---|
| `Supplier` / `Vendor` | Fornecedor | Cadastro |
| `PurchaseOrder` (PO) | Pedido de compra | Cabeçalho |
| `PurchaseOrderItem` | Item do pedido de compra | Itens |
| `PurchaseRequisition` | Requisição de compra | Solicitação interna |
| `RequestForQuotation` (RFQ) | Pedido de cotação | Cotação com fornecedores |
| `PurchaseInvoice` | Nota fiscal de entrada | Entrada fiscal |
| `GoodsReceiptNote` (GRN) | Nota de recebimento | Conferência de entrega |
| `ThreeWayMatch` | Conferência tripartite | PO × NF × recebimento |
| `Contract` / `SupplyAgreement` | Contrato de fornecimento | Acordo comercial |
| `BlanketOrder` / `FrameworkOrder` | Contrato aberto | Pedidos programados |
| `DropShipment` | Remessa direta | Fornecedor envia direto ao cliente |
| `Consignment` | Consignação | Estoque do fornecedor |
| `Procurement` | Aquisição / suprimentos | Processo |
| `Sourcing` | Sourcing / seleção de fornecedores | Estratégia de compras |
| `VendorRating` / `SupplierScorecard` | Avaliação de fornecedor | Qualidade/prazo |

---

## 🚛 7. Logística / Entregas (Logistics & Shipping)

| Termo | Tradução | Uso |
|---|---|---|
| `Shipment` | Remessa / envio | **Tabela central** de envios |
| `ShipmentItem` | Item da remessa | Itens enviados |
| `Shipping` | Envio / expedição | Processo |
| `Carrier` / `ShippingCompany` | Transportadora | Prestadora de serviço |
| `FreightForwarder` | Despachante / agente de carga | Intermediário |
| `Delivery` | Entrega | Entrega ao destinatário |
| `DeliveryNote` / `DeliveryOrder` | Romaneio / nota de entrega | Documento de entrega |
| `Tracking` / `TrackingNumber` | Rastreamento / código de rastreio | Código da transportadora |
| `TrackingEvent` | Evento de rastreio | Histórico (postado, em trânsito, entregue) |
| `Status` / `ShipmentStatus` | Status do envio | Coluna de estado |
| `Waybill` / `AirWaybill` (AWB) | Conhecimento de transporte | CT-e / AWB aéreo |
| `Manifest` | Manifesto de carga | Lista de CTe |
| `Route` / `RoutePlanning` | Rota / planejamento de rotas | Otimização |
| `Stop` / `DeliveryStop` | Parada de entrega | Pontos na rota |
| `Driver` | Motorista | Cadastro |
| `Vehicle` / `Truck` | Veículo / caminhão | Frota |
| `Fleet` | Frota | Conjunto de veículos |
| `Package` / `Parcel` | Pacote / encomenda | Volume |
| `Box` / `Carton` | Caixa | Embalagem |
| `Pallet` | Palete | Unitização |
| `Dimension` / `Volume` | Dimensão / volume | Cubagem |
| `GrossWeight` / `NetWeight` | Peso bruto / peso líquido | Cubagem |
| `Freight` / `ShippingFee` | Frete | Custo |
| `Insurance` / `CargoInsurance` | Seguro / seguro de carga | Avaria/perda |
| `Origin` / `Destination` | Origem / destino | Endereços do envio |
| `Sender` / `Recipient` / `Consignee` | Remetente / destinatário | Partes |
| `Pickup` | Coleta / retirada | Retirada no local |
| `Dispatch` | Expedição / despacho | Saída do centro |
| `InTransit` | Em trânsito | Status |
| `OutForDelivery` | Saiu para entrega | Status final |
| `Delivered` | Entregue | Status final |
| `FailedDelivery` / `DeliveryAttempt` | Tentativa de entrega / falha | Reentrega |
| `ReturnShipment` / `ReverseLogistics` | Devolução / logística reversa | Volta do produto |
| `WarehouseManagementSystem` (WMS) | Sistema de gestão de armazém | Sistema |
| `TransportationManagementSystem` (TMS) | Sistema de gestão de transporte | Sistema |
| `CrossDocking` | Cross docking | Transbordo sem estoque |
| `LastMile` | Última milha | Entrega final |
| `Incoterms` | Incoterms | Termos de comércio exterior (FOB, CIF, EXW) |

---

## 💰 8. Financeiro / Contábil (Finance & Accounting)

| Termo | Tradução | Uso |
|---|---|---|
| `Account` | Conta (contábil/bancária) | Plano de contas |
| `ChartOfAccounts` | Plano de contas | Estrutura contábil |
| `Ledger` / `GeneralLedger` (GL) | Livro razão | Lançamentos contábeis |
| `JournalEntry` | Lançamento contábil | Débito/crédito |
| `Debit` / `Credit` | Débito / crédito | Partidas dobradas |
| `Transaction` | Transação | Movimento financeiro |
| `Payment` | Pagamento | Saída/entrada de dinheiro |
| `Receipt` | Recebimento | Entrada de dinheiro |
| `AccountReceivable` (AR) | Contas a receber | Título de cliente |
| `AccountPayable` (AP) | Contas a pagar | Título de fornecedor |
| `Invoice` | Fatura / título | Contas a receber/pagar |
| `Billing` | Cobrança / faturamento | Emissão de títulos |
| `Statement` / `AccountStatement` | Extrato | Extrato de conta |
| `Balance` | Saldo | Valor atual |
| `Reconciliation` / `BankReconciliation` | Conciliação bancária | Conferência extrato × sistema |
| `Deposit` | Depósito | Entrada em conta |
| `Withdrawal` | Saque | Retirada |
| `Transfer` | Transferência | Entre contas |
| `Refund` | Reembolso | Devolução de valor |
| `Chargeback` | Chargeback | Contestação de cartão |
| `Fee` / `ServiceCharge` | Taxa / tarifa | Tarifas bancárias |
| `Interest` / `Fine` / `Penalty` | Juros / multa | Mora |
| `Discount` | Desconto | Desconto financeiro |
| `DueDate` / `MaturityDate` | Data de vencimento | Vencimento do título |
| `IssueDate` | Data de emissão | Emissão |
| `Overdue` | Atrasado | Status do título |
| `WriteOff` | Baixa / prejuízo | Título irrecoverável |
| `Dunning` / `Collection` | Cobrança / inadimplência | Processo de cobrança |
| `Installment` / `Parcel` | Parcela | Parcelas do título |
| `PaymentMethod` | Forma de pagamento | Boleto, cartão, Pix, TED |
| `PaymentGateway` | Gateway de pagamento | Integração (Stripe, Pagar.me) |
| `TransactionFee` / `MerchantFee` | Taxa de transação / intercâmbio | Maquininha/gateway |
| `Wallet` | Carteira digital | Saldo virtual |
| `BalanceSheet` | Balanço patrimonial | Relatório |
| `IncomeStatement` / `P&L` | DRE (Resultado) | Relatório |
| `CashFlow` | Fluxo de caixa | Relatório |
| `Budget` / `Forecast` | Orçamento / previsão | Planejamento |
| `Cost` / `Expense` | Custo / despesa | Natureza do gasto |
| `Revenue` / `Income` | Receita | Faturamento |
| `Profit` / `Loss` | Lucro / prejuízo | Resultado |
| `Asset` / `Liability` / `Equity` | Ativo / passivo / patrimônio | Balanço |
| `Depreciation` / `Amortization` | Depreciação / amortização | Ativo imobilizado |
| `Tax` / `TaxRate` | Imposto / alíquota | Fiscal |
| `TaxReturn` | Declaração de imposto | IR/ICMS |
| `WithholdingTax` | Imposto retido na fonte | Retenção |
| `InvoiceNumber` | Número da nota/fatura | Identificador |
| `PurchaseInvoice` / `SalesInvoice` | NF de entrada / saída | Fiscal |

---

## 🧾 9. Fiscal / Tributário (no Brasil, mapeado)

| Termo em inglês | Equivalente PT | Uso |
|---|---|---|
| `Tax` / `Taxation` | Imposto / tributação | Geral |
| `TaxRate` | Alíquota | % do imposto |
| `TaxBase` / `Basis` | Base de cálculo | Valor base |
| `TaxAmount` | Valor do imposto | Coluna |
| `TaxJurisdiction` | Jurisdição tributária | Município/UF/país |
| `TaxExemption` | Isenção | Benefício fiscal |
| `TaxIncentive` | Incentivo fiscal | Zona Franca, Simples |
| `Withholding` | Retenção na fonte | IRRF, INSS, PIS/COFINS |
| `FiscalNote` / `ElectronicInvoice` | Nota fiscal eletrônica | NF-e / NFS-e |
| `InvoiceSeries` | Série da nota | Série |
| `AccessKey` | Chave de acesso | Chave 44 dígitos |
| `Validation` / `Authorization` | Validação / autorização | SEFAZ |
| `Cancellation` | Cancelamento | Cancelamento de NF |
| `CorrectionLetter` | Carta de correção | CC-e |
| `TaxRegime` | Regime tributário | Lucro Real/Presumido/Simples |
| `ICMS` / `IPI` / `PIS` / `COFINS` / `ISS` | (mantidos em PT) | Impostos brasileiros — **não traduzir** |
| `CFOP` | CFOP | Código fiscal de operações |
| `NCM` | NCM | Nomenclatura comum do Mercosul |
| `CEST` | CEST | Substituição tributária |

> 💡 **Dica de arquitetura:** no Brasil, colunas de impostos específicos (ICMS, IPI, PIS, COFINS, ISS, CFOP, NCM) costumam **ficar em português** ou como siglas, pois são conceitos legais locais. O resto do modelo (tabelas e colunas genéricas) em inglês.

---

## 🏭 10. Produção / Manufatura (Manufacturing)

| Termo | Tradução | Uso |
|---|---|---|
| `WorkOrder` / `ProductionOrder` | Ordem de produção | Cabeçalho |
| `ProductionPlan` | Plano de produção | Planejamento |
| `BillOfMaterials` (BOM) | Lista de materiais / estrutura | Componentes |
| `Routing` / `ProcessRoute` | Roteiro de produção | Sequência de operações |
| `Operation` / `Step` | Operação / etapa | Etapa do roteiro |
| `WorkCenter` / `Machine` | Centro de trabalho / máquina | Recurso produtivo |
| `Capacity` | Capacidade | Carga da máquina |
| `Scheduling` | Agendamento / programação | Sequenciamento |
| `RawMaterial` | Matéria-prima | Insumo |
| `SemiFinishedGoods` | Produto semi-acabado | Intermediário |
| `FinishedGoods` | Produto acabado | Final |
| `Scrap` / `Waste` | Refugo / perda | Perda na produção |
| `Yield` | Rendimento | Aproveitamento |
| `QualityControl` (QC) / `QualityAssurance` (QA) | Controle/garantia da qualidade | Inspeção |
| `Inspection` | Inspeção | Verificação |
| `Defect` | Defeito | Não conformidade |
| `Maintenance` / `MaintenanceOrder` | Manutenção / ordem de manutenção | Preventiva/corretiva |
| `Downtime` | Parada / inatividade | Tempo parado |
| `OEE` (Overall Equipment Effectiveness) | Eficiência global do equipamento | Métrica |
| `MRP` (Material Requirements Planning) | Planejamento de necessidades de materiais | Sistema |
| `MES` (Manufacturing Execution System) | Sistema de execução da manufatura | Sistema |

---

## 📊 11. Projetos / Serviços (Project & Professional Services)

| Termo | Tradução | Uso |
|---|---|---|
| `Project` | Projeto | Cabeçalho |
| `Task` / `Activity` | Tarefa / atividade | Itens do projeto |
| `Subtask` | Subtarefa | Nível abaixo |
| `Milestone` | Marco / milestone | Entrega importante |
| `Sprint` | Sprint | Scrum |
| `Epic` / `Story` / `Feature` | Épico / história / funcionalidade | Backlog |
| `Bug` / `Issue` | Bug / demanda | Ticketing |
| `Timesheet` | Apontamento de horas | Horas trabalhadas |
| `TimeEntry` | Lançamento de hora | Item do timesheet |
| `Resource` | Recurso (pessoa/equipamento) | Alocação |
| `Allocation` | Alocação | Recurso no projeto |
| `Budget` | Orçamento do projeto | Custos |
| `Expense` | Despesa do projeto | Reembolsáveis |
| `Deliverable` | Entregável | Produto do projeto |
| `ChangeRequest` | Solicitação de mudança | Escopo |
| `Risk` / `IssueLog` | Risco / registro de problemas | Gestão de riscos |
| `Phase` / `Stage` | Fase / etapa | Waterfall |
| `Gantt` | Diagrama de Gantt | Cronograma |
| `WorkBreakdownStructure` (WBS) | Estrutura analítica do projeto | EAP |
| `StatementOfWork` (SOW) | Declaração de trabalho | Escopo contratual |

---

## 💳 12. SaaS / Assinaturas / Plataformas

| Termo | Tradução | Uso |
|---|---|---|
| `Subscription` | Assinatura | Recorrência |
| `Plan` / `Tier` | Plano / camada | Free, Pro, Enterprise |
| `Feature` / `Capability` | Funcionalidade | Recursos do plano |
| `PlanFeature` | Funcionalidade do plano | Tabela N:N |
| `Usage` / `Consumption` | Uso / consumo | Uso de API/armazenamento |
| `Quota` / `Limit` | Cota / limite | Limites do plano |
| `BillingCycle` | Ciclo de cobrança | Mensal/anual |
| `Renewal` | Renovação | Renovação de assinatura |
| `Trial` / `FreeTrial` | Período de teste | Trial |
| `Upgrade` / `Downgrade` | Upgrade / downgrade | Mudança de plano |
| `Invoice` / `Billing` | Fatura / cobrança | Recorrente |
| `Proration` | Proporcional | Cálculo de mudança de plano |
| `Tenant` | Tenancy / inquilino | Multi-tenant (SaaS) |
| `Workspace` / `Organization` | Workspace / organização | Grupo de usuários |
| `Member` / `Membership` | Membro / associação | Usuário no workspace |
| `Invitation` | Convite | Convite de usuário |
| `APIKey` / `Token` | Chave de API / token | Acesso programático |
| `Webhook` | Webhook | Notificação de evento |
| `Event` / `EventLog` | Evento / log de eventos | Auditoria/event sourcing |
| `Metric` / `Analytics` | Métrica / analítico | BI |
| `Dashboard` | Painel / dashboard | Visualização |
| `Report` | Relatório | Exportável |
| `Notification` | Notificação | Push/e-mail/in-app |
| `Preference` / `UserPreference` | Preferência do usuário | Configurações pessoais |

---

## 🔐 13. Autenticação / Segurança / Sistema (transversal a todos)

| Termo | Tradução | Uso |
|---|---|---|
| `User` | Usuário | Tabela principal |
| `Account` | Conta de usuário | Sinônimo |
| `Role` | Perfil / papel | RBAC |
| `Permission` / `Privilege` | Permissão / privilégio | Acesso |
| `RolePermission` | Permissão do perfil | Tabela N:N |
| `UserRole` | Perfil do usuário | Tabela N:N |
| `Group` | Grupo | Agrupamento de usuários |
| `AccessControlList` (ACL) | Lista de controle de acesso | Permissões granulares |
| `Policy` | Política | Regra de acesso (IAM) |
| `Session` | Sessão | Login ativo |
| `Token` / `RefreshToken` | Token / token de renovação | JWT |
| `PasswordHash` | Hash de senha | Coluna |
| `PasswordReset` | Redefinição de senha | Token temporário |
| `TwoFactor` / `MFA` | 2FA / autenticação multifator | Segurança |
| `LoginAttempt` | Tentativa de login | Brute-force |
| `Lockout` | Bloqueio de conta | Tentativas inválidas |
| `AuditLog` / `ActivityLog` | Log de auditoria / atividade | Quem fez o quê |
| `AccessLog` | Log de acesso | Entradas no sistema |
| `Blacklist` / `Whitelist` | Lista negra / branca | Controle |
| `EncryptionKey` | Chave de criptografia | Segurança |
| `DataSubject` / `DataProcessing` | Titular / tratamento de dados | LGPD/GDPR |
| `Consent` | Consentimento | LGPD |
| `DataBreach` | Vazamento de dados | Incidente |
| `Backup` / `Restore` | Backup / restauração | Operacional |

---

## 🔑 14. Campos Padrão (presentes em quase toda tabela)

| Coluna | Tradução | Uso |
|---|---|---|
| `Id` / `ID` | Identificador | PK (GUID/int) |
| `Code` / `Number` | Código / número | Código legível (pedido, NF) |
| `Name` / `Description` | Nome / descrição | Texto |
| `Status` | Status | Estado (enum) |
| `Type` / `Category` | Tipo / categoria | Discriminador |
| `IsActive` / `Active` | Ativo | Soft delete flag |
| `IsDeleted` / `Deleted` | Excluído | Soft delete |
| `CreatedAt` / `CreationDate` | Data de criação | Auditoria |
| `CreatedBy` / `CreatedById` | Criado por | Auditoria |
| `UpdatedAt` / `LastModifiedDate` | Última alteração | Auditoria |
| `UpdatedBy` / `ModifiedBy` | Alterado por | Auditoria |
| `DeletedAt` | Data de exclusão | Soft delete |
| `Version` / `RowVersion` | Versão do registro | Concorrência otimista |
| `Notes` / `Observation` | Observações | Campo texto livre |
| `ExternalId` | Identificador externo | Integração (ERP legado) |
| `TenantId` / `CompanyId` | Id do inquilino/empresa | Multi-tenant |
| `Amount` / `Value` | Valor / montante | Decimal |
| `Quantity` / `Qty` | Quantidade | Decimal/int |
| `UnitPrice` | Preço unitário | Decimal |
| `Total` | Total | Decimal |
| `Date` / `DateTime` | Data / data-hora | Evento |
| `DueDate` | Vencimento | Prazo |
| `StartDate` / `EndDate` | Início / fim | Vigência |
| `Reference` | Referência | Campo livre de integração |

---

## 📐 15. Padrões de nomenclatura (escolha do arquiteto)

| Convenção | Exemplo | Onde é comum |
|---|---|---|
| **snake_case** (tudo minúsculo) | `sales_order`, `employee_id` | PostgreSQL, MySQL, Python/Django |
| **PascalCase** (singular) | `SalesOrder`, `EmployeeId` | SQL Server, C#/.NET, Entity Framework |
| **UPPER_SNAKE** | `SALES_ORDER` | Oracle legado |
| **Prefixos** | `TB_`, `VW_`, `SP_`, `FN_` | Oracle/SQL Server legado (evite em novos projetos) |
| **Tabelas no singular** | `Order`, `Customer` | EF Core, DDD moderno |
| **Tabelas no plural** | `Orders`, `Customers` | Rails, Django, convenção antiga |
| **FK = `<tabela>Id`** | `CustomerId`, `ProductId` | Quase universal hoje |
| **Tabelas de junção N:N** | `UserRole`, `OrderProduct` | Nome composto |
| **Views prefixadas** | `vwSalesSummary` | SQL Server |
| **Stored procedures** | `usp_` / `sp_` | SQL Server (evite `sp_` — reservado à Microsoft) |

> ✅ **Recomendação para seu stack (.NET + SQL Server):** PascalCase, tabelas no **singular**, PK `Id`, FK `NomeTabelaId`, colunas de auditoria `CreatedAt/CreatedBy/UpdatedAt/UpdatedBy`, e `IsDeleted` + `DeletedAt` para soft delete.

---

## 🧠 Bônus — Termos de arquitetura/engenharia que você vai ouvir no dia a dia

- **Ubiquitous Language** — linguagem onipresente (DDD)
- **Bounded Context** — contexto delimitado (DDD)
- **Aggregate / Aggregate Root** — agregado / raiz do agregado
- **Entity vs Value Object** — entidade vs objeto de valor
- **Domain Event** — evento de domínio
- **Repository / Unit of Work** — padrões de persistência
- **CQRS / Event Sourcing** — separação leitura/escrita
- **ACID** — atomicidade, consistência, isolamento, durabilidade
- **Normalization / Denormalization** — normalização/desnormalização
- **Index (clustered / non-clustered)** — índice clusterizado/não clusterizado
- **Foreign Key (FK) / Primary Key (PK) / Composite Key** — chaves
- **Schema** — esquema (agrupador de tabelas: `Sales.`, `HR.`)
- **View / Stored Procedure / Trigger / Function** — objetos de BD
- **Migration** — migração de esquema (EF Core)
- **Seed** — dados iniciais
- **ETL / ELT / Data Warehouse / OLAP / OLTP** — BI
- **Replication / Sharding / Partitioning** — escalabilidade
- **Read Replica** — réplica de leitura
- **Connection String / Connection Pool** — string de conexão / pool
- **Transaction / Savepoint / Rollback / Commit** — transação
- **Deadlock / Race Condition** — impasse / condição de corrida
- **N+1 Query** — problema clássico de performance
- **Migration / Backfill** — migração / preenchimento retroativo

---

