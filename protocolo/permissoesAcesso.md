---
title: Permissões de usuários Protocolo
description: Descrição das permissões de usuários do sistema Protocolo
published: true
date: 2020-06-30T13:45:40.320Z
tags: protocolo, permissões, usuários
---

# Permissões de Usuários no PROTOCOLO

* | Operação | Classe e Método | Nível Critico
:------|:------|:------:|:------:| :------:
1 | Modo leitura | Usuário Suporte/Administrador não acessa modo leitura | -
2 | Processa Relatório | ProcessoRelatorioControllerinit() | <span style="color:green">1</span>
3 | Copia processos | SessionControllerisCopiaProcessos()| <span style="color:green">1</span>
4 | Recepciona guia de remessa | SessionControllerisRecepcionaGuiaDeRemessa() | <span style="color:red">5</span>
5  |  Cadastra Processo Interno  |  SessionController isCadastraProcessoInterno()  |  3
6  |  Cadastra Processo Externo  |  SessionController isCadastraProcessoExterno()  |  3
7  |  Lista todos os protocolos  |  SessionController montaPermissoesDoUsuario()  |  1
8  |  Exclusão de Guia Remessa criada por outro usuário  |  GuiaRemessaService autorizaExcusaoGuiaRemessa()  |  5
9  |  Excluir Andamento de Processo  |  ProcessoAndamentoService removerAndamentoManual()  |  5
10  |  Pesquisa Avançada de Processo (Retorna apenas os processos onde o usuário possui acesso, desconsiderando o usuário do tipo suporte e administrador)  |  ProcessoService pesquisaAvancadaProcessoSomente- OndeUsuarioPossuiAcesso()  |  3
11  |  Permite editar andamento  |  ProcessoService permitiEditarAndamento()  |  3
12  |  Deletar Anexo do Processo  |  ProcessoService permitiDeletarAnexo()  |  5
13  |  Permite visualizar Processo  |  ProcessoService permiteVisualizarProcesso()  |  1
14  |  Verifica andamento sigiloso  |  ProcessoService verificarAndamentoSigiloso()  |  3
15  |  Permite estornar guia recebida  |  GuiaRemessaController estornarRecepcao()  |  3
16  |  Habilita cadastro de Processos  |  ProcessoController habilitaCadastroDeProcessos()  |  1

<br/>

### <center> Permissões de Telas </center> 
ID | Tela | Descrição | Nível Critico
:------| :------: | :------: | :------: | :------: |
35  |  Agendamentos  |  Agendamento de Sincronismo – Não está funcionando  |  -
40  |  AndamentoPeloProcesso  |  Ao entrar no Processo é possível dar um novo andamento  |  3
23  |  Assunto  |  Cadastro/Alteração/Exclusão/Visualização de Assuntos do Processo  |  1
6  |  Auditoria  |  Auditoria de ações (inclusão, alteração, exclusão) realizadas no sistema  |  1
9  |  Bairro  |  Cadastro/Alteração/Exclusão/Visualização de Bairro  |  1
1  |  Cidade  |  Cadastro/Alteração/Exclusão/Visualização de Cidade  |  1
7  |  Cliente  |  Dados do Cliente que está acessando (Ex: Três Lagoas)  |  1
30  |  ConsultaGuiaRemessaEnviada  |  Consulta de guias de Remessas Enviadas  |  1
31  |  ConsultaGuiaRemessaRecebida  |  Consulta de guias Recebidas  |  1
29  |  ConsultaProcessos  |  Consulta de Processos (Interno e Externo)  |  1
22  |  Documento Requerido  |  Cadastro/Alteração/Exclusão/Visualização de documentos requeridos no processo  |  1
20  |  documentoTipo  |  Cadastro/Alteração/Exclusão/Visualização de Tipos de Documentos  |  1
2  |  Estado  |  Cadastro/Alteração/Exclusão/Visualização de Estado  |  1
18  |  FaixaSequencial  |  Cadastro anualmente (Processos abertos durante o ano)  |  1
39  |  GerenciarPessoas  |  Gerenciar Processos e Pessoas (Transferência de Processos e exclusão de Pessoas)  |  3
26  |  guiaRemessa  |  Incluir no cadastro de processo uma guia de Remessa  |  1
17  |  Imposto  |  Cadastro/Alteração/Exclusão/Visualização de taxas existentes no SAT  |  1
16  |  local  |  Cadastro/Alteração/Exclusão/Visualização de local “Secretaria”  |  1