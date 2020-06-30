---
title: Permissões de usuários Protocolo
description: Descrição das permissões de usuários do sistema Protocolo
published: true
date: 2020-06-30T14:30:33.391Z
tags: protocolo, permissões, usuários
---

# Permissões de Usuários no PROTOCOLO

#### <center>Permissões para Nível de Suporte (32) / Administrador (16)</center> 

* | Operação | Classe e Método | Nível Critico
:------|:------|:------:|:------:| :------:
1 | Modo leitura | Usuário Suporte/Administrador não acessa modo leitura | -
2 | Processa Relatório | ProcessoRelatorioControllerinit() | <span style="color:green">1</span>
3 | Copia processos | SessionControllerisCopiaProcessos()| <span style="color:green">1</span>
4 | Recepciona guia de remessa | SessionControllerisRecepcionaGuiaDeRemessa() | <span style="color:red">5</span>
5  |  Cadastra Processo Interno  |  SessionController isCadastraProcessoInterno()  |  <span style="color:orange">3</span>
6  |  Cadastra Processo Externo  |  SessionController isCadastraProcessoExterno()  |  <span style="color:orange">3</span>
7  |  Lista todos os protocolos  |  SessionController montaPermissoesDoUsuario()  |  <span style="color:green">1</span>
8  |  Exclusão de Guia Remessa criada por outro usuário  |  GuiaRemessaService autorizaExcusaoGuiaRemessa()  |  <span style="color:red">5</span>
9  |  Excluir Andamento de Processo  |  ProcessoAndamentoService removerAndamentoManual()  |  <span style="color:red">5</span>
10  |  Pesquisa Avançada de Processo (Retorna apenas os processos onde o usuário possui acesso, desconsiderando o usuário do tipo suporte e administrador)  |  ProcessoService pesquisaAvancadaProcessoSomente- OndeUsuarioPossuiAcesso()  |  <span style="color:orange">3</span>
11  |  Permite editar andamento  |  ProcessoService permitiEditarAndamento()  |  <span style="color:orange">3</span>
12  |  Deletar Anexo do Processo  |  ProcessoService permitiDeletarAnexo()  |  <span style="color:red">5</span>
13  |  Permite visualizar Processo  |  ProcessoService permiteVisualizarProcesso()  |  <span style="color:green">1</span>
14  |  Verifica andamento sigiloso  |  ProcessoService verificarAndamentoSigiloso()  |  <span style="color:orange">3</span>
15  |  Permite estornar guia recebida  |  GuiaRemessaController estornarRecepcao()  |  <span style="color:orange">3</span>
16  |  Habilita cadastro de Processos  |  ProcessoController habilitaCadastroDeProcessos()  |  <span style="color:green">1</span>

<br/>

### <center> Permissões de Telas </center> 
<center>*Se o usuário tiver perfil Administrador, todas as telas são liberadas</center>

ID | Tela | Descrição | Nível Critico
:------| :------: | :------: | :------: | :------: |
35  |  Agendamentos  |  Agendamento de Sincronismo – Não está funcionando  |  -
40  |  AndamentoPeloProcesso  |  Ao entrar no Processo é possível dar um novo andamento  |  <span style="color:orange">3</span>
23  |  Assunto  |  Cadastro/Alteração/Exclusão/Visualização de Assuntos do Processo  |  <span style="color:green">1</span>
6  |  Auditoria  |  Auditoria de ações (inclusão, alteração, exclusão) realizadas no sistema  |  <span style="color:green">1</span>
9  |  Bairro  |  Cadastro/Alteração/Exclusão/Visualização de Bairro  |  <span style="color:green">1</span>
1  |  Cidade  |  Cadastro/Alteração/Exclusão/Visualização de Cidade  |  <span style="color:green">1</span>
7  |  Cliente  |  Dados do Cliente que está acessando (Ex: Três Lagoas)  |  <span style="color:green">1</span>
30  |  ConsultaGuiaRemessaEnviada  |  Consulta de guias de Remessas Enviadas  |  <span style="color:green">1</span>
31  |  ConsultaGuiaRemessaRecebida  |  Consulta de guias Recebidas  |  <span style="color:green">1</span>
29  |  ConsultaProcessos  |  Consulta de Processos (Interno e Externo)  |  <span style="color:green">1</span>
22  |  Documento Requerido  |  Cadastro/Alteração/Exclusão/Visualização de documentos requeridos no processo  |  <span style="color:green">1</span>
20  |  documentoTipo  |  Cadastro/Alteração/Exclusão/Visualização de Tipos de Documentos  |  <span style="color:green">1</span>
2  |  Estado  |  Cadastro/Alteração/Exclusão/Visualização de Estado  |  <span style="color:green">1</span>
18  |  FaixaSequencial  |  Cadastro anualmente (Processos abertos durante o ano)  |  <span style="color:green">1</span>
39  |  GerenciarPessoas  |  Gerenciar Processos e Pessoas (Transferência de Processos e exclusão de Pessoas)  |  <span style="color:orange">3</span>
26  |  guiaRemessa  |  Incluir no cadastro de processo uma guia de Remessa  |  <span style="color:green">1</span>
17  |  Imposto  |  Cadastro/Alteração/Exclusão/Visualização de taxas existentes no SAT  |  <span style="color:green">1</span>
16  |  local  |  Cadastro/Alteração/Exclusão/Visualização de local “Secretaria”  |  <span style="color:green">1</span>
24  |  LocalFisico  |  Cadastro/Alteração/Exclusão/Visualização local físico “Setor”  |  <span style="color:green">1</span>
10  |  Logradouro  |  Cadastro/Alteração/Exclusão/Visualização de Logradouro  |  <span style="color:green">1</span>
32  |  ModeloDocumento  |  Cadastro/Alteração/Exclusão/Visualização de Modelo de Documento  |  <span style="color:green">1</span>
21  |  ModeloDocumentoTipo  |  Cadastro/Alteração/Exclusão/Visualização de Modelo de Tipo de Documento  |  <span style="color:green">1</span>
14  |  Modo Administrador  |  Habilita o Modo de Administrador  |  <span style="color:red">5</span>
13  |  Nacionalidade  |  Cadastro/Alteração/Exclusão/Visualização de Nacionalidade  |  <span style="color:green">1</span>
37  |  NotificacaoCollor  |  Protocolo de Obras – Status do Processo muda de cor (Controle de Notificação)  |  <span style="color:green">1</span>
37  |  NotificacaoCollor  |  Protocolo de Obras – Status do Processo muda de cor (Controle de Notificação)  |  <span style="color:green">1</span>
12  |  País  |  Cadastro/Alteração/Exclusão/Visualização de País  |  <span style="color:green">1</span>
34  |  Parametros  |  Alteração de parâmetros no sistema, Ex: Endereço do servidor SAT  |  <span style="color:red">5</span>
3  |  Perfil  |  Cadastro/Alteração/Exclusão/Visualização de Perfil  |  <span style="color:orange">3</span>
28  |  PermissaoAcessoProtocolo  |  Configurar Permissão de Acesso ao sistema  |  <span style="color:green">1</span>
4  |  Permissões  |  Relatório de Permissões de Acesso  |  <span style="color:green">1</span>
33  |  Pessoa  |  Cadastro/Alteração/Exclusão/Visualização de Pessoas que são requerentes ou parte interessada dos processos  |  <span style="color:orange">3</span>
19  |  Procedimento  |  Relatório de Assuntos que possuem Procedimentos  |  <span style="color:green">1</span>
15  |  Processo  |  Relatórios de Andamentos, Processo, Por Usuários etc.  |  <span style="color:green">1</span>
27  |  ProcessoAndamento  |  Trâmite de Processo  |  <span style="color:red">5</span>
25  |  Protocolo  |  Relatório de Protocolos ativos no sistema  |  <span style="color:green">1</span>
8  |  Tipo Bairro  |  Cadastro/Alteração/Exclusão/Visualização de Tipo de Bairro  |  <span style="color:green">1</span>
11  |  Tipo Logradouro  |  Cadastro/Alteração/Exclusão/Visualização de Tipo de Logradouro  |  <span style="color:green">1</span>
36  |  TransferenciaProcessos  |  Gerenciar Processos e Pessoas (Transferência de Processos e exclusão de Pessoas)  |  <span style="color:orange">3</span>
5  |  Usuário  |  Cadastro/Alteração/Exclusão/Visualização de Usuário  |  <span style="color:green">1</span>